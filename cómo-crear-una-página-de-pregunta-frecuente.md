Esta es una guía para crear las páginas que responden a preguntas de
nuestros usuarios.

Con respecto al contenido:

  - Seleccionar el título de la página como una pregunta con signo de
    interrogación antes y después.
  - Escribir sólo en mayúscula la primera letra de la primera palabra.
  - Colocar la página en [Ayuda:Ayuda](Ayuda:Ayuda "wikilink") dentro de
    la sección correspondiente.
  - Organizar las secciones con títulos de nivel 2 (`==`) donde cada una
    es una acción; p.ej: crear usuario en directorio activo, asignar
    preferencias, etc. Una persona que entienda cómo funciona NiMbox
    debería saber qué hacer sólo leyendo estos títulos.
  - Referirse a  siempre utilizando {{NiMbox}}.
  - Hacer referencia a urls de la siguiente forma
    `http://demo.local.nimbox.net/ar` en todos los lugares donde se
    requiera. Esto se puede hacer colocando la línea `192.168.128.22
    demo.local.nimbox.net`</core>`  en  `<core>`/etc/hosts`.

Con respecto a las screen shots:

  - Sólo vamos a colocar screen shots de safari para mantener todo
    consistente.
  - El tamaño de la pantalla de safari debe ser exactamente `1280 × 720`
    (hd wide screen format). Para colocar la ventana de safari de ese
    tamaño hay que correr el siguiente [Apple
    Script](¿Cómo_colocar_safari_en_1280x720? "wikilink").
  - La ventana sólo debe mostrar la barra de direcciones y nada mas. Hay
    que ocultar la barra de bookmarks, la barra de tabs y la barra de
    status abajo.
  - La dirección debe siempre mostrar `http://demo.nimbox.com`. Para
    lograr esto se debe cambiar el archivo `/etc/hosts` para hacer la
    redirección correcta.
  - Para hacer el screen shot vamos a utilizar el mecanismo built in de
    Mac OSX de `Command+Shift+4 Space`. Esto guarda en el desktop un
    archivo de la ventana con todo y su sombra alrededor.
  - El formato de este archivo debe ser `.png`. El tamaño de la imagen
    termina siendo `1360 × 800` o `1394 × 834`.
  - El momento de colocar la imagen dentro del archivo hay que escalarla
    a la mitad. Esto se logra
    escribiendo\[\[Archivo:archivo.png|680px\]\] o
    \[\[Archivo:archivo.png|697px\]\].

De requerir hacer zoom:

  - En Photoshop seleccionar la zona a resaltar y crear un Layer via
    Copy
  - En Edit \> Transform \> Scale y darle entre 120% y 150%
  - Colocar el efecto drop shadown 120 grados 5 px y un Stroke de 5 Px
    Negro
