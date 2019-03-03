## ¿Cómo me conecto a NiMbox?

NiMbox es accesible desde diferentes lugares y a través de diferentes
dispositivos. En función del lugar de acceso hay que utilizar una
dirección diferente, la cuál se actualizar de forma automática. Estas
direcciones son:

  - <http://box.local.nimbox.net> (dentro de la oficina)
  - <http://box.nimbox.net> (fuera de la oficina)
  - <http://box.nimbox.net/m> (desde blackberry y otros teléfonos)

Adicionalmente a estas direcciones se crea y mantiene actualizada la
dirección `box.public.nimbox.net` que representa la dirección IP pública
a través de la cual está conectado NiMbox a Internet.

## ¿Cuáles son los usuarios?

NiMbox utiliza la misma plataforma de usuarios que tiene la empresa.
Generalmente es directorio activo. Para conectarse a NiMbox hay que
utilizar el mismo identificador y clave registrados en el directorio
activo.

## ¿Cómo se crea un nuevo usuario?

Un nuevo usuario hay que crearlo en dos lugares. En el directorio activo
y en NiMbox. Hay información mas detallada en
<http://wiki.nimbox.com/wiki/¿Cómo_crear_un_nuevo_usuario%3F>.

### Directorio Activo

Generalmente los usuarios ya están creados en el directorio activo así
que solamente hay que asociarlo a alguno de los dos grupos de seguridad
de NiMbox. Estos grupos son:

  - Apexer Administrators (usuarios con privilegios aumentados)
  - Apexer Users (usuarios regulares)

En general todos los usuarios deberían estar asociados a `Apexer Users`.

### NiMbox

Para crear un usuario en NiMbox hay que ir a la página
<http://box.local.nimbox.net/administration>. Se presiona el botón de
nuevo usuario que está a la derecha, se introduce el identificador del
usuario y luego se le asignan las empresas y aplicaciones a las que
tiene acceso.

## ¿Cómo cambio los accesos de los usuarios?

Los usuarios tienen dos niveles de acceso. El que provee el directorio
activo y el que provee NiMbox. El directorio activo define quién se
puede conectar al servidor, mientras NiMbox permite definir qué puede
hacer ese usuario. Lo que puede hacer está descrito en función de qué
empresas puede ver (en el caso de que sea multi empresa la instalación)
y que aplicaciones puede acceder (en el caso en que hay múltiples
aplicaciones instaladas). Esta definición se hace en
<http://box.local.nimbox.net/administration>.

## ¿Qué hay dentro del servidor?

El servidor es una instalación de la distribución Debian de Linux con
las aplicaciones propietarias de NiMbox. Para acceder al servidor hay
que hacerlo con el usuario `root` con el password suministrado al
momento de la instalación.

## ¿Cómo se prende y apaga el servidor?

En caso que haya que mover o por alguna otra razón, apagar y prender el
servidor hay dos formas para hacerlo. La primera es presionando muy
brevemente el botón de encendido que está en el frente del servidor. Una
vez presionado pasarán unos 30 segundos y el servidor quedará
completamente apagado. La segunda es conectándose con el usuario `root`
y ejecutando el comando `shutdown -h now`.

## ¿Qué browsers soporta?

Las aplicaciones de NiMbox están diseñadas para trabajar exclusivamente
con las versiones mas recientes de todos los browsers. Esto incluye,
Firefox, Google Chrome, Safari y Explorer (versión 9 en adelante). Si
por alguna razón hubiese que utilizar versiones de explorer anteriores a
la 9 hay que instalar en esos browsers el plugin de google chrome frame
que se puede conseguir en <http://code.google.com/chrome/chromeframe/>.
Esta instalación es muy sencilla y NiMbox ya está diseñado para
utilizarlo cuando lo consigue disponible.

## ¿Cómo pido ayuda adicional?

Hay varias fuentes para solicitar ayuda.

  - Nuestro wiki tiene muchas de las preguntas frecuentas que nos hacen
    los clientes. Busca en <http://wiki.nimbox.com/>.
  - La barra de "Feedback" que está en la izquierda de todas las páginas
    NiMbox. Al presionar esta barra se abre un diálogo donde puedes
    colocar preguntas o comentarios que le llegan a nuestro equipo de
    soporte.
  - Llamada directa a nuestras oficinas al teléfono +58(212)285-3348
    durante horario de oficina.
