Esta forma de acceder los servicios web ha sido deprecada. Estamos en
proceso de reconvertir toda la plataforma de servicios web a una basada
en tokens. Esta forma permite un desarrollo mucho más sencillo al tiempo
que permite separar los usuarios de los tokens.

NiMbox permite acceder ciertas de sus funcionalidades a través de
servicios web. El punto de contacto de estos sitios web es la dirección
segura <https://host/direct/items>. Los servicios web disponibles por el
momento son:

## Agregar una nota

Es posible agregar notas a cualquiera de los elementos de datos
representados en NiMbox. Los parámetros son:

  - thingyId:el elemento al cual conectarle la nota. Típicamente este
    elemento es un contacto.  
    contextName (opcional):el nombre del contexto al cual conectarle la
    nota.  
    description:el contenido de la nota.

Para crear una nota

    wget --user=jlopez --password=comic --no-check-certificate -qO- \
      <nowiki>"https://host/direct/items/notes/create?thingyId=24&description=La+nota+se+proceso+exitosamente"</nowiki>

En caso de éxito el resultado será un json parecido a este:

    {
      'error' : false,
      'note' : {
        'id' : 34044,
        'description' : "La nota se proceso exitosamente",
        'sortDate' : new Date(2010,11,21,7,5,36),
        'createdOn' : new Date(2010,11,21,7,5,36),
        'createdBy' : "jlopez",
        'updatedOn' : new Date(2010,11,21,7,5,36),
        'updatedBy' : "jlopez"
        'deletedOn' : null,
        'deletedBy' : null,
      }
    }

En caso de error el resultado será un json parecido a este:

    {
      'errors' : {
        'thingyId' : "nota no está relacionada con ningún objeto"
        'description' : "descripción está vacía",
      },
      'error' : true
    }

## Agregar una tarea

## Completar una tarea

## Consultar documentos pendientes por cobrar

Para consultar los documentos pendientes, en formato separado por comas
[CSV](http://es.wikipedia.org/wiki/CSV), hay que pasar los siguientes
parámetros:

  - days (opcional) : número de días para hacer el corte de los días
    vencidos. Un valor positivo representa documentos vencidos y un
    valor negativo representa documentos por vencer. Al colocar esta
    opción se retornan todos los documentos con vencimiento mayor al
    valor suministrado.

Para realizar una consulta:

    wget --user=jlopez --password=comic --no-check-certificate -qO- \
      <nowiki>"https://host/direct/items/contact-pending"</nowiki>

El resultado retorna los siguientes campos:

  - contactId : el identificador único del contacto dentro de .  
    contactDisplayName : el nombre del contacto.  
    documentCount : cantidad de documentos pendientes.  
    documentTotal : monto total de los documentos pendientes (sin
    incluir ningún pago aplicado).  
    documentPending : monto por cobrar de los documentos pendientes.  
    documentWeightedDays : días promedio ponderados de los documentos
    pendientes.  
    contactPhones : telefonos del contacto formateado como;
    **tipo:numero** y separados por el caracter ';'.

Un ejemplo de este resultado se vería
    así:

    "12590","Organizacion Palo Alto, C.A.","7","503008.76000","376258.75000","332","Work:0212 285 3348;Mobile:04122345678"
    "540","COMUNICACIONES SICA, C.A","1","484.96000","116.48000","6","Mobile:04122345678"
    "406","RUSTI ACCESORIOS CORONA, C.A.","1","4693.92000","4693.92000","1","Home:0212-2345678"
    "12594","DISTRIBUIDORA DE UÑAS L.N. 2008, C.A","2","7694.49000","1680.49000","0","Home:02122853348;Mobile:04122345678"
    "30229","FONDO DE INVERSIONES COMERCIAL AVILA, C.A","1","468.83000","468.83000","48",""
    "30675","VERA ROLDAN FERNANDO ANTONIO","1","890.40000","890.40000","41",""
    "12652","Lior Cosmetics, C.A.","11","150734.90000","150734.90000","466","Mobile:04142345678"
    "12556","EBANO GRUPO MODA, C.A.","1","104.16000","104.16000","468","Mobile:04162345678"
    "1026","ADVENTURE EXTREME 4X4, C.A.","1","7618.24000","7618.24000","52",""
    "31469","TRAVELUSA TOURS VIAJES Y TURISMO C.A","1","97110.72000","39110.72000","49","Mobile:04124545555;Mobile:04122345678"
    "12634","LOYOLA SPORT CLUB","1","29691.23000","26981.23000","510","Mobile:+584122345678"
    "852","AUDIO CAR, C.A.","1","2222.08000","2222.08000","41","Mobile:58-412-2345678"

## Consultar tareas pendientes de un usuario

Para consultar las tareas pendientes, en formato separado por comas
[CSV](http://es.wikipedia.org/wiki/CSV) y ordenado por fecha, hay que
pasar los siguientes parámetros:

  - user (opcional) : usuario sobre el cual se desean conocer las
    tareas. Al colocar esta opción se retornan todos las tareas
    pendientes que pertenecen al usuario especificado.  
    dueBefore (opcional) : fecha máxima de vencimiento de la tarea. Por
    ejemplo si colocas la fecha de mañana, el archivo
    [CSV](http://es.wikipedia.org/wiki/CSV) solo devolverá tareas
    vencidas pendientes, las que se vencen hoy y las tareas que se
    vencen mañana, omitiendo tareas que se vayan a vencer pasado mañana
    en adelante.

Para realizar una consulta:

    wget --user=jlopez --password=comic --no-check-certificate -qO- \
      <nowiki>"https://host/direct/items/task?user=jlopez"</nowiki>

El resultado retorna los siguientes campos:

  - id : El identificador único de la tarea dentro de .  
    description : El contenido de la tarea.  
    due : La fecha en que esta tarea debe ser realizada formateada como
    **dd/mm/yyyy hh:mm**.  
    responsible : Responsable, en caso de ser un usuario este puede
    marcar la tarea como completada.  
    supervisor : Usuario supervisor, puede completar y supervisar la
    tarea.  
    contactId : El identificador único del contacto asociado a la
    tarea.  
    contactDisplayName : el nombre del contacto asociado a la tarea.  
    contactPhones : telefonos del contacto formateado como;
    **tipo:numero** y separados por el caracter ';'.  
    lastContactNote : Contenido de la última nota.  
    documentPending : monto por cobrar de los documentos pendientes.  
    documentWeightedDays : días promedio ponderados de los documentos
    pendientes.

Un ejemplo de este resultado se vería
    así:

    "22","Llamarlo","27/01/2011 13:00","Org Palo Alto","Corfin","12590","Org Palo Alto","Work:02122853348","Le deje un #mensaje de voz","503008.76","7"
    "22596","Actualizar datos","27/01/2011 00:00","540","Corfin","Lorena","COMUNICACIONES SICA, C.A","Mobile:04122345678","#noselocaliza","0.00","0"

## Obtener una lista de clientes

Para solicitar clientes en formato
[CSV](http://es.wikipedia.org/wiki/CSV) que cumplan con condiciones
específicas visitar <https://host/direct/items/customer>

Los parametros de filtro de busqueda pueden ser los siguientes:
businessName lateDaysQuantile totalQuantile

Para definir las columans del csv enviar varios parametros **col**.
Similar a
[TracQuery](http://trac.edgewall.org/wiki/TracQuery#UsingTracLinks)

Ejemplo:

``` 
   http://192.168.128.22/ar/items/customers?businessName=BACA&lateDaysQuantile=4&totalQuantile=4&col=contactId&col=contactDisplayName
```

    "30675","VERA ROLDAN FERNANDO ANTONIO"
    "12652","Lior Cosmetics, C.A."
    "12556","EBANO GRUPO MODA, C.A."
