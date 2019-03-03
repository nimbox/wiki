Instalar **nimbox** es un proceso muy sencillo. Hay que seguir los
siguientes pasos:

## Procurar un servidor

El servidor en el que corre **nimbox** debe estar dedicado
exclusivamente a nimbox.

Para instalaciones pequeñas, con 250 facturas mensuales o menos, se
requiere:

  - 2 núcleo
  - 4 gbytes de ram
  - 80 gbytes de disco duro

Para instalaciones medianas, con 250 a 2.000 facturas mensuales, se
requiere:

  - 4 núcleos
  - 8 gbytes de ram
  - 160 gbytes de disco duro

Para instalaciones grandes, con más de 2.000 facturas mensuales, se
requiere:

  - 4 núcleos
  - 16 o más gbytes de ram
  - 160 gbytes de disco duro.

El servidor puede ser virtual sin ningún problema.

## Instalar Debian

  - Utilizamos la instalación de debian de 64 bits que está localizada
    [aquí](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/archive/8.8.0+nonfree/amd64/iso-cd/firmware-8.8.0-amd64-netinst.iso).
  - Después de decargarla hay que arrancar la máquina con ese cd.
  - En el primer menú hay que presionar ESC para que aparezca un prompt
    que dice **boot**.

![debian-installer.png](debian-installer.png "debian-installer.png")

![debian-installer-boot.png](debian-installer-boot.png
"debian-installer-boot.png")

  - En este prompt hay que colocar la siguiente línea para que debian se
    instale en la forma como lo necesita nimbox.

<!-- end list -->

    boot: auto url=http://repository.nimbox.com/debian/preseed.cfg

![debian-installer-boot-full.png](debian-installer-boot-full.png
"debian-installer-boot-full.png")

  - Luego presionamos enter para que la instalación siga de forma
    automática.

![debian-installer-preseed.png](debian-installer-preseed.png
"debian-installer-preseed.png")

## Llamar al equipo de soporte de nimbox

Para finalizar la instalación hay que contactar al equipo de nimbox para
que realice el resto de la instalación de forma remota.

Es necesario dar al personal de nimbox la dirección IP indicada como
**nimbox pad**

![issue.png](issue.png "issue.png")

En este proceso final se entregan los certificados de seguridad de la
instalación y la interconexión con el sistema administrativo de la
empresa.

Eso es todo\!
