Para las instalaciones donde nimbox no está interconectado con Active
Directory es necesario realizar la incorporación de usuarios en dos
lugares.

## Crear el usuario en el servidor nimbox

Modificar el archivo `/etc/nimbox/tomcat/tomcat-users.xml` donde se debe
colocar el usuario, clave y grupo de acceso. De la siguiente forma:

    <?xml version="1.0" encoding="UTF-8"?>
    <tomcat-users>
      <role rolename="Apexer Administrators"/>
      <role rolename="Apexer Users"/>
      <user username="srgerente" password="biendificil" roles="Apexer Administrators"/>
      <user username="srcobrador" password="biendificil" roles="Apexer Users"/>
    </tomcat-users>

La única diferencia entre ambos grupos, `Apexer Administrators` y
`Apexer Users`, es que los usuarios que están en `Apexer Administrators`
pueden:

  - Asignar accesos en nimbox
  - Marcar tareas supervisadas de cualquier usuario.

## Asignar accesos en nimbox

Una vez que el usuario tiene permiso en el servidor, es posible que se
conecte a , sin embargo ese usuario aun no tiene acceso a ninguna de las
aplicaciones o compañias disponibles. Para que lo tenga hay que ir a la
dirección de administración donde <nombre> es típicamente el nombre de
la compañía:

    http://<nombre>.local.nimbox.net/administration

Si el usuario está ya en la lista de usuarios, sólo se le asignan los
accesos. Si no está en la lista de usuarios se presiona el botón de
`Nuevo Usuario` para crearlo, colocando el login y luego asignar los
accesos que se requieran. Los accesos típicos son: AR (para cuentas por
cobrar) y al menos una compañía.

![nimbox.administration.png](nimbox.administration.png
"nimbox.administration.png")
