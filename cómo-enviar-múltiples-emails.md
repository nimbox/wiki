El envío de múltiples emails comienza presionando el botón  que está en
la página principal.

![ar-multimemail-1.png](ar-multimemail-1.png "ar-multimemail-1.png")

La próxima página permite realizar la selección de la audiencia a la
cuál se le enviará el mensaje. La audiencia son todos los clientes y
direcciones de correo que cumplen con cierto criterio. En esta primer
ejemplo le enviaremos un email muy amigable a todos los clientes que
tienen facturas con 30 o más días de vencidas. Para lograr esto hay que:

1\. Seleccionar el email de la persona que envía el mensaje (el origen).

2\. Seleccionar la casilla que dice "que tengan facturas con días
vencidos en el rango" y colocar el rango "30 - ".

3\. Escribir el mensaje que se desea enviar, el cual puede incluir
variables de substitución.

![ar-multimemail-2.png](ar-multimemail-2.png "ar-multimemail-2.png")

4\. Presionar el botón  para identificar cuáles serán los clientes y
direcciones de correo a los que se enviará el correo. Esto es importante
para verificar quiénes son los destinatarios seleccionados.

![ar-multimemail-3.png](ar-multimemail-3.png "ar-multimemail-3.png")

5\. Revisar que el mensaje salga de la forma correcta presionando el
pequeño sobre al lado de cada cliente.

![ar-multimemail-4.png](ar-multimemail-4.png "ar-multimemail-4.png")

6\. Presionar el botón  para realizar el envío.

## Estrategia de envíos por exclusión

El proceso anterior permite realizar el envío a todos los clientes que
tienen facturas vencidas en el rango seleccionado; sin embargo, habrán
clientes con facturas vencidas en ese rango los cuáles no desean recibir
los mensajes de notificación. Cuando se usa la estrategia de exclusión
se busca realizar el envío a todos los clientes *excepto* aquellos que
cumplan con cierto criterio. El criterio actualmente es definido en
función de una etiqueta. Utilicemos en este ejemplo la etiqueta  para
marcar aquellos clientes a los que no se les desee enviar el email. Para
etiquetar un cliente hay que seguir las instrucciones sobre [¿Cómo
etiquetar un cliente?](¿Cómo_etiquetar_un_cliente? "wikilink").

Adicionalmente a excluir clientes, se pueden excluir direcciones de
correo dentro de un cliente. Por ejemplo, si se desea enviar la
notificación a un cliente, pero no se desea enviar la notificación a una
dirección en particular (p.ej.: la del gerente general dentro del
cliente), hay que marcar esta dirección con la etiqueta  para que no
reciba las notificaciones. Para etiquetar una dirección de correo hay
que que seguir las instrucciones sobre [¿Cómo etiquetar un elemento de
contacto?](¿Cómo_etiquetar_un_elemento_de_contacto? "wikilink").

Una vez etiquetados los clientes a excluir se pasa por el proceso
anterior, pero seleccionando adicionando las políticas de exclusión:

![ar-multimemail-5.png](ar-multimemail-5.png "ar-multimemail-5.png")

El efecto neto de esta estrategia es que se le envía el email a todos
los clientes, excepto aquellos etiquetados  y a todas las direcciones de
correo dentro de un cliente excepto las etiquetadas .
