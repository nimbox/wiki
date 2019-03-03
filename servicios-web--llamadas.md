## Introducción

Es posible incorporar llamadas al muro del cliente desde una aplicación
externa a través de este servicio web. El uso típico de este servicio
sería correr un daemon, en algún otro servidor, que con cierta
periodicidad, va creando las llamadas en NiMbox. Las llamadas creadas
tienen una clave única construida con la fecha de la llamada
(`initiated`), el origen de la llamada (`source`) y el destino de la
llamada (`destination`). Sólo puede haber una llamada en un momento, de
un origen, a un destino a la vez. Si se trata de crear una segunda
llamada con los mismos parámetros, esta no sería creada porque ya
existe.

Para comenzar a utilizar el servicio web hay que pasar por los
siguientes pasos:

  - Conseguir un `TOKEN` para poder hacer las llamadas a la plataforma
    de servicios web.
  - Copiar el script de perl, que está más abajo, en el servidor de
    asterisk o la central telefónica que se tenga.
  - Modificar el script para que refleje la instalación donde se está
    corriendo. Es importante realizar la transformación de los números
    de destino para que NiMbox los puede procesar. Por ejemplo, eliminar
    el número 9 al inicio, e incorporar el código de área cuando no está
    presente para llamadas locales. Todo esto ocurre en la función
    `convertDestination` de perl. NiMbox espera recibir números bastante
    completos.
  - Generar un trabajo cron que corra cada hora en modalidad incremental
    (sin proveer el parámetro `-f`) y una vez al día en modalidad full
    (con el parámetro `-f`).
  - Monitorear el proceso de replicación de forma constante

El siguiente trabajo cron corre la versión incremental todas las horas y
corre la versión full a las 11 de la noche (hora
    23).

    #!/bin/sh                                                                            
    HOUR=$(date +"%H")
    if [ $HOUR == '23' ]; then
        /path/to/phonecalls -f
    else
        /path/to/phonecalls 
    fi

## Crear una llamada - /direct/items/phonecalls/create

Para crear una nueva llamada hay que realizar una solicitud a
<https://host/direct/items/phonecalls/create> con los siguientes
parámetros:

  - token: token de autenticación ante el web service  
    initiated: fecha de la llamada en formato ISO8601  
    source: número que origina la llamada  
    destination: número al que se hizo la llamada  
    duration (opcional): duración de la llamada en segundos  
    url (opcional): link para mostrar junto con la llamada que puede
    llevar a mayor detalle de la misma fuera de la aplicación de NiMbox

Para crear una nueva llamada se puede utilziar:

    wget --no-check-certificate -qO- \
      "https://host/direct/items/phonecalls/create?token=12345678&initiated=2012-08-23T12:20:33&source=7222&destination=02122853348&duration=45&url=http..."

En caso de que todo funcione correctamente se recibirá un json parecido
a este:

    {
        "error": false,
        "contactId": 12334,
        "phonecallId": 3241
    }

  - contactId: es el código del contacto al que se le conectó la
    llamada  
    phonecallId: es el código de la llamada

Si algo no funcionó se recibirá un json parecido a este:

    {
        "error": true,
        "errors": {
            "destination": "no se consiguió el número de destino en la base de datos"
        }
    }

## Eliminar llamadas - /direct/items/phonecalls/delete

Para eliminar llamadas hay que realizar una solicitud a
<http://host/direct/items/phonecalls/delete> con los siguientes
parámetros:

  - token: token de autenticación ante el web service  
    from: fecha desde que se debe eliminar, en formato ISO8601  
    to: fecha hasta que se debe debe eliminar, en formato ISO8601

Ambas fechas son exclusivas y no deben tener las horas.

Para eliminar llamadas se puede utilizar:

    wget --no-check-certificate -qO- \
      "https://host/direct/items/phonecalls/delete?token=12345678&from=2012-08-23&to=2012-08-25"

El resultado de esta invocación resulta en un json con un parámetro
`error` que puede ser `true` o `false`.

    {
      "count" : 702,
      "error" : false
    }

  - count: cantidad de llamadas eliminadas

En caso de que ocurra un error se recibirá un json parecido a este:

    {
      "error" : true,
      "errors" : {
      }
    }

## phonecalls script

Es posible modificar este script en perl para extraer las llamadas de la
tabla cdr de asterisk y crearlas en NiMbox. El script generalmente se
debe llamar `phonecalls`.

    #!/usr/bin/perl
    
    use strict;
    use warnings;
    
    use POSIX qw/strftime/;
    
    use Getopt::Long;
    use Pod::Usage;
    
    use DBI;
    use LWP::UserAgent;
    use LWP::ConnCache;
    use URI::Escape;
    use JSON;
    
    # configuration
    
    my $REPLICATION_HOURS = 200;
    my $REPLICATION_DAYS = 360;
    
    my $ASTERISK_HOST = "192.168.128.96";
    my $ASTERISK_USER = "testing";
    my $ASTERISK_PASSWORD = "testing";
    
    my $NIMBOX_HOST = "192.168.1.98:8080";
    my $NIMBOX_USER = "admin";
    my $NIMBOX_PASSWORD = "admin";
    my $NIMBOX_DIRECT_TOKEN = "12345678";
    
    # options
    
    my $full = 0;
    my $verbose = 0;
    GetOptions(
        'full' => \$full,
        'verbose' => \$verbose,
        'help|?' => sub { pod2usage({ -verbose => 1}); },
        'man' => sub { pod2usage({ -verbose => 2, -noperldoc => 1}); }
        ) or pod2usage();
    
    my $startdate;
    if ($full) {
        $startdate = strftime("%Y-%m-%d", 
                  localtime(time - $REPLICATION_DAYS * 24 * 60 * 60));
    } else {
        $startdate = strftime("%Y-%m-%dT%H:%M:%S", 
                  localtime(time - $REPLICATION_HOURS * 60 * 60));
    }
    
    print "processing calls starting $startdate...\n" if ($verbose);
    
    # do the query
    
    my $start = time;
    
    print "querying asterisk database at $ASTERISK_HOST...\n" if ($verbose);
    
    my $handle = DBI->connect(
        "DBI:mysql:asterisk;host=$ASTERISK_HOST", 
        $ASTERISK_USER, 
        $ASTERISK_PASSWORD);
    
    my $sql = <<EOSQL;
    SELECT 
        DATE_FORMAT(calldate, '%Y-%m-%dT%TZ') AS initiated, 
        src AS source, 
        dst AS destination, 
        duration AS duration,
        CONCAT('http://192.168.128.96/recordings/', channel) AS url
    FROM 
        cdr 
    WHERE 
        calldate >= '$startdate' AND LENGTH(dst) >= 7
    EOSQL
    
    my $statement = $handle->prepare($sql);
    $statement->execute();
    
    # send the results
    
    print "sending results to NiMbox at $NIMBOX_HOST...\n" if ($verbose);
    
    my $agent = LWP::UserAgent->new();
    $agent->cookie_jar({});
    my $cache = LWP::ConnCache->new();
    $cache->total_capacity([1]);
    $agent->conn_cache($cache);
    $agent->credentials("$NIMBOX_HOST", "NiMbox", $NIMBOX_USER, $NIMBOX_PASSWORD);
    
    my $count = 0;
    my $lap = time;
    
    while (my $r = $statement->fetchrow_hashref()) {
    
        print "processing $r->{initiated} from $r->{source} to $r->{destination}... " if ($verbose);
    
        # prepare the url
    
        my $url = "http://$NIMBOX_HOST/direct/items/phonecalls/create";
        $url = $url . "?token=$NIMBOX_DIRECT_TOKEN";
        $url = $url . "&initiated=$r->{initiated}";
        $url = $url . "&source=$r->{source}";
        $url = $url . "&destination=" . 
        uri_escape(convertDestination($r->{'destination'}));
        $url = $url . "&duration=$r->{duration}";
        $url = $url . "&url=" . 
        uri_escape($r->{'url'});
    
        my $response = $agent->get($url);
        if ($response->is_success) {
        my $json = decode_json($response->content);
        if ($json->{'error'}) {
            print "ERROR\n" if ($verbose);
        } else {
            print "OK\n" if ($verbose);
        }
        } else {
        print "ERROR (" . $response->status_line . ")\n" if ($verbose);
        }
    
        $count = $count + 1;
        if ($count % 1000 == 0) {
        print "processing $count (total: " . (time - $start) . "s lap: " . (time - $lap) . "s)\n";
        $lap = time;
        }
    
    }
    
    print "finished (total: " . (time - $start) . "s)\n";
    
    exit(0);
    
    
    sub convertDestination {
    
        my ($destination) = @_;
    
        if ($destination =~ /^9/) {
        $destination = substr($destination, 1);
        if (length($destination) == 7) {
            $destination = "0261" . $destination;
        }
        }
    
        return $destination;
    
    }
    
    #
    # documentation
    #
    __END__
    
    =head1 NAME
    
    phonecalls - create phonecall records in nimbox from asterisk database
    
    =head1 SYNOPSIS
    
    B<phonecalls> [-full] [-verbose] [-help] [-man]
    
    =head1 OPTIONS
    
    =over 8
    
    =item B<-full>
    
    perform a full replication, as opposed to an incremental replication if
    this option is not provided
    
    =item B<-verbose>
    
    displays actions being performed
    
    =item B<-help>
    
    displays brief help message and exits
    
    =item B<-man>
    
    displays manual manual page and exits
    
    =back
    
    =head1 DESCRIPTION
    
    Read the cdr records from an asterisk database and create the in a NiMbox
    server.  This process is separated in two stages.  The incremental stage
    only reads the last 2 hours and tries to create the phonecalls in NiMbox.
    The full stage reads the last 360 days.  This script can be run many times
    without creating extra phonecalls.  This happens because there can only be
    one phonecall in NiMbox for a given date, source and destination.
    
    =head1 AUTHOR
    
    Ricardo Marimon (rmarimon@nimbox.com)
    
    =head1 LICENCE AND COPYRIGHT
    
    Copyright (c) 2009-2012 Organización Palo Alto.
    Proprietary and Confidential.  Al rights reserved.
    
    =cut

[Category:Servicios Web](Category:Servicios_Web "wikilink")
