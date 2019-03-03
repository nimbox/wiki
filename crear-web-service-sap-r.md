## Resumen

Para extraer los datos de las tablas de SAP es necesario crear una
función y exponerla en un Web Service.

## Tablas consultadas

### Customer

| columna | descripción                    |
| ------- | ------------------------------ |
| KNB1    | Clientes de una Sociedad.      |
| KNA1    | Name, Region, Address y phone. |
| KNKK    | Credit Amount                  |
| ADR6    | Email.                         |
| KNVP    | Representative from RRHH.      |
| KNVV    | Representative from Sales.     |

### Representative

| columna | descripción                |
| ------- | -------------------------- |
| PA0002  | Representative from RRHH.  |
| TVGRT   | Representative from Sales. |
| KNKK    | Monto de Crédito.          |

### Product

| columna    | descripción |
| ---------- | ----------- |
| MARA       | Product.    |
| MAKT       | Name.       |
| KONP, A004 | Price.      |

### Stock

| columna | descripción |
| ------- | ----------- |
| MARD    | Stock.      |

### Warehouse

| columna | descripción |
| ------- | ----------- |
| T001L   | Warehouse.  |

### Term

| columna | descripción |
| ------- | ----------- |
| T052    | Terms.      |

### Invoice, CreditNote, DebitNote

| columna | descripción                        |
| ------- | ---------------------------------- |
| VBRK    | Billing Document (sales document). |
| VBPA    | Representative from RRHH.          |
| VRKPA   | Representative from Sales.         |
| BSID    | Pending.                           |
| BSAD    | Pending.                           |

## Crear función a exponer

Pasos:

1\. Navegar hasta la transacción SE37 en SAP y copiar el módulo de
funciones RFC\_READ\_TABLE con el nombre ZNIMBOX\_RFC\_READ\_TABLE (debe
ser obligatoriamente este nombre)

2\. En el código fuente de la función, ubicar la sección "ASSIGN WORK TO
CASTING TYPE” cerca de la línea 165 y reemplazarlo con el siguiente
código"

``` 
 DATA: BEGIN OF WORK, BUFFER(30000), END OF WORK.
 
 FIELD-SYMBOLS: <WA> TYPE ANY, <COMP> TYPE ANY.
 " --- begin of modification
 " ASSIGN WORK TO <WA> CASTING TYPE (QUERY_TABLE).
 DATA: tab_ref TYPE REF TO data.
 CREATE DATA tab_ref TYPE (query_table).
 ASSIGN  tab_ref->* TO <wa>.
 " --- end of modification
 IF ROWCOUNT > 0.
   ROWCOUNT = ROWCOUNT + ROWSKIPS.
 ENDIF.
 
 SELECT * FROM (QUERY_TABLE) INTO <WA> WHERE (OPTIONS). 
```

Esta sustitución en el código de la función RFC\_READ\_TABLE permite que
la nueva función pueda leer campos de tipo float.

3\. Guardar y activar la nueva funcion presionando Ctrl + F3

## Exponer función en Web Service

Seguir las indicaciones expuestas en el siguiente documento para exponer
la función y obtener el WSDL que necesitamos:
![ExposeWebService.pdf](ExposeWebService.pdf "ExposeWebService.pdf")

Es importante al momento de escoger el endpoint para la función marcar
el check "Mapping der Namen", este check hace que tanto el endpoint como
la función sean expuestas usando notación CamelCase (XML es case
sensitive y necesitamos que la función sea expuesta a través del web
service tomando eso en cuenta).

## Actualizar el timeout

Cuando hay muchas transacciones es necesario variar el timeout de las
solicitudes que se hacen a SAP. Si bien utilizamos iteradores para
extraer datos en pedazos pequeños, hay veces que el volumen es
demasiado. La solución oficial para cambiar el TIMEOUT es la
siguiente:

  - Timeout:

<http://help.sap.com/saphelp_nw73/helpdata/en/48/88b52977323cb8e10000000a42189d/content.htm>

  - Server
Port:

<http://help.sap.com/saphelp_nw73/helpdata/en/48/3ae05299c172d0e10000000a42189c/content.htm>

Específicamente la parte que nos interesa corregir es:

**Recommendation**

In systems where the standard timeout setting of 60 seconds for the
keep-alive and processing timeouts is not sufficient due to long-running
applications, SAP recommends that both the TIMEOUT and PROCTIMEOUT
parameters are set for the services concerned so that they can be
configured independently of each other. The TIMEOUT value should not be
set unnecessarily high.

We recommend you set this parameter as follows:

`   icm/server_port_0 = PROT=HTTP,PORT=1080,TIMEOUT=60,PROCTIMEOUT=600`

in order to allow a maximum processing time of 10 minutes.

**Recomendamos asignar los valores**

`   "TIMEOUT=120,PROCTIMEOUT=900" `

los cuales han funcionado anteriormente para clientes con un volumen de
datos alto.

## Request para consumir el Web Service

Es importante asegurarnos que el request para consumir el Web Service
cumpla con las siguientes condiciones. Esto es automático si se exporta
el web service desde el ERP pero debe ser configurado específicamente si
la función se exporta desde PI

  - El tag soapenv debe ser de la siguiente manera, atributos deben ser
    así:

<!-- end list -->

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:sap-com:document:sap:soap:functions:mc-style">

  - Al exponer la función ha de quedar con el nombre
    ZnimboxRfcReadTable.

Siendo el tag urn:

    <urn:ZnimboxRfcReadTable>...</urn:ZnimboxRfcReadTable>

  - La mayoría de los tags usan el standard Java, donde la primera letra
    de cada palabra es mayúscula y el resto minúsculas (excepto: item,
    soapenv, urn)

Los tags del request deben quedar de la siguiente manera:

    <soapenv:Header/>

    <Fieldname>...</Fieldname>

    <QueryTable>...</QueryTable>

    <Fields>
      <item>
        <Fieldname>KUNNR</Fieldname>
        <Offset />
        <Length />
        <Type />
        <Fieldtext/>
      </item>
    </Fields>

Los tags del response deben quedar:

``` 

      <ns0:ZnimboxRfcReadTable.Response xmlns:ns0="urn:sap-com:document:sap:rfc:functions">
         <Data>
            <item>
               <Wa/>
            </item>
            <item>
               <Wa></Wa>
            </item>
         </Data>
         <Fields>
            <item>
               <Fieldname></Fieldname>
               <Offset></Offset>
               <Length></Length>
               <Type></Type>
               <Fieldtext></Fieldtext>
            </item>
         </Fields>
         <Options>
            <item>
               <Text/>
            </item>
         </Options>
      </ns0:ZnimboxRfcReadTable.Response>
```
