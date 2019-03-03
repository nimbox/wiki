## Introducción

Las lunas de cobranza puedes ser muy útiles en otros contextos. Para
obtener las lunas de cobranza se pueden solicitar a través de este
servicio web.

## Obtener las lunas actuales - /direct/items/late-days-total

Para obtener la lista de lunas para todos los clientes hay que hacer una
solicitud a <https://host/direct/items/late-days-total> con los
siguientes parámetros:

  - token: token de autenticación ante el web service  
    businessName (opcional): nombre de la empresa  
    format: el formato en el que se desea el resultado, por ahora sólo
    puede ser `csv`

Para obtener la lista actual se puede
    utilizar:

    https://host/direct/items/late-days-total?token=12345678&businessName=BCOM&format=csv

En el caso en que se solicite un archivo en formato `csv` el resultado
será de la siguiente forma:

    OPA,J308777641,-1,0,-1,0,0
    OPA,1293657971,4,36,2,12096.0000,11
    OPA,1293657972,0,3,2,11088.0000,11
    OPA,1293657973,4,30,4,17808.0000,11
    OPA,1293657974,3,27,3,12115.1000,12
    OPA,1293657975,3,21,3,12235.0100,11
    OPA,1293657976,4,87,0,5040.0000,5

Donde las columnas serán las siguientes:

  - businessName: nombre de la empresa  
    originalId: código del cliente en el sistema administrativo  
    lateDaysQuintile: quintil de días de retraso del 0 al 4, donde 0 es
    el mejor (luna naranja), 4 es el peor (luna roja) y -1 es que no hay
    información  
    lateDaysAverage: promedio de días de retraso  
    totalQuintile: quintil del total de ventas del 0 al 4, donde es el
    más pequeño (luna amarilla), 4 es al más grande (luna verde) y -1
    es que no hay información  
    totalTotal: total de la facturación  
    totalCount: cantidad de facturas

Es importante recordar que el cálculo de las lunas de cobranza se
realiza en función de la historia de los últimos 360 días. Es posible
tener clientes que compraron hace más de 360 días pero que no aparecen
asignados a un quintil.

[Category:Servicios Web](Category:Servicios_Web "wikilink")
