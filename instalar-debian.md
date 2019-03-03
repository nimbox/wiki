Hay que utilizar la versión de debian 8.9.0 de 64 bits en inglés que se
puede descargar
[aquí](https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/archive/8.9.0+nonfree/amd64/iso-cd/firmware-8.9.0-amd64-netinst.iso)
Una vez decargada la imagen, y quemada en un cd, se sigue esta secuencia
de pasos hasta completar la instalación. Hay varias consideraciones
importantes:

  - El servidor debe tener ciertas características básicas:
      - Robusto en cuanto a los circuitos, la fuente de poder y la caja
        (no recomendamos un clon de baja calidad)
      - Un procesador Core 2 Duo de 2.0GHz o mejor
      - 4 Gbytes de ram (mas si el volumen transaccional us muy alto)
      - 160 Gbytes de disco duro.
  - El servidor debe estar conectado a una red con
    [`DHCP`](http://es.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)
    y debe tener acceso a internet.
  - Hay que cambiar todos los lugares que dicen `box` por el nombre de
    la instalación que se está realizando. Este nombre debe ser
    entregado por el equipo técnico de .
  - El password del usuario `root` debe ser `root` hasta que se finalice
    el proceso de instalación. Luego se puede cambiar a cualquier otro
    password que se acuerde con el cliente que tendrá el servidor en sus
    premisas.

## Al arrancar el servidor con el CD

![Debian-6.0.3-01.png](Debian-6.0.3-01.png "Debian-6.0.3-01.png")
![Debian-6.0.3-02.png](Debian-6.0.3-02.png "Debian-6.0.3-02.png")

## Al comenzar la instalación en modo experto

![Debian-6.0.3-03.png](Debian-6.0.3-03.png "Debian-6.0.3-03.png")
![Debian-6.0.3-04.png](Debian-6.0.3-04.png "Debian-6.0.3-04.png")
![Debian-6.0.3-05.png](Debian-6.0.3-05.png "Debian-6.0.3-05.png")
![Debian-6.0.3-06.png](Debian-6.0.3-06.png "Debian-6.0.3-06.png")
![Debian-6.0.3-07.png](Debian-6.0.3-07.png "Debian-6.0.3-07.png")
![Debian-6.0.3-08.png](Debian-6.0.3-08.png "Debian-6.0.3-08.png")
![Debian-6.0.3-09.png](Debian-6.0.3-09.png "Debian-6.0.3-09.png")
![Debian-6.0.3-10.png](Debian-6.0.3-10.png "Debian-6.0.3-10.png")
![Debian-6.0.3-11.png](Debian-6.0.3-11.png "Debian-6.0.3-11.png")
![Debian-6.0.3-12.png](Debian-6.0.3-12.png "Debian-6.0.3-12.png")
![Debian-6.0.3-13.png](Debian-6.0.3-13.png "Debian-6.0.3-13.png")
![Debian-6.0.3-14.png](Debian-6.0.3-14.png "Debian-6.0.3-14.png")
![Debian-6.0.3-15.png](Debian-6.0.3-15.png "Debian-6.0.3-15.png")
![Debian-6.0.3-16.png](Debian-6.0.3-16.png "Debian-6.0.3-16.png")
![Debian-6.0.3-17.png](Debian-6.0.3-17.png "Debian-6.0.3-17.png")
![Debian-6.0.3-18.png](Debian-6.0.3-18.png "Debian-6.0.3-18.png")
![Debian-6.0.3-19.png](Debian-6.0.3-19.png "Debian-6.0.3-19.png")
![Debian-6.0.3-20.png](Debian-6.0.3-20.png "Debian-6.0.3-20.png")
![Debian-6.0.3-21.png](Debian-6.0.3-21.png "Debian-6.0.3-21.png")
![Debian-6.0.3-22.png](Debian-6.0.3-22.png "Debian-6.0.3-22.png")
![Debian-6.0.3-23.png](Debian-6.0.3-23.png "Debian-6.0.3-23.png")
![Debian-6.0.3-24.png](Debian-6.0.3-24.png "Debian-6.0.3-24.png")
![Debian-6.0.3-25.png](Debian-6.0.3-25.png "Debian-6.0.3-25.png")
![Debian-6.0.3-26.png](Debian-6.0.3-26.png "Debian-6.0.3-26.png")
![Debian-6.0.3-27.png](Debian-6.0.3-27.png "Debian-6.0.3-27.png")
![Debian-6.0.3-28.png](Debian-6.0.3-28.png "Debian-6.0.3-28.png")
![Debian-6.0.3-29.png](Debian-6.0.3-29.png "Debian-6.0.3-29.png")
![Debian-6.0.3-30.png](Debian-6.0.3-30.png "Debian-6.0.3-30.png")
![Debian-6.0.3-31.png](Debian-6.0.3-31.png "Debian-6.0.3-31.png")
![Debian-6.0.3-32.png](Debian-6.0.3-32.png "Debian-6.0.3-32.png")
![Debian-6.0.3-33.png](Debian-6.0.3-33.png "Debian-6.0.3-33.png")
![Debian-6.0.3-34.png](Debian-6.0.3-34.png "Debian-6.0.3-34.png")
![Debian-6.0.3-35.png](Debian-6.0.3-35.png "Debian-6.0.3-35.png")
![Debian-6.0.3-36.png](Debian-6.0.3-36.png "Debian-6.0.3-36.png")
![Debian-6.0.3-37.png](Debian-6.0.3-37.png "Debian-6.0.3-37.png")
![Debian-6.0.3-38.png](Debian-6.0.3-38.png "Debian-6.0.3-38.png")
![Debian-6.0.3-39.png](Debian-6.0.3-39.png "Debian-6.0.3-39.png")
![Debian-6.0.3-40.png](Debian-6.0.3-40.png "Debian-6.0.3-40.png")
![Debian-6.0.3-41.png](Debian-6.0.3-41.png "Debian-6.0.3-41.png")
![Debian-6.0.3-42.png](Debian-6.0.3-42.png "Debian-6.0.3-42.png")
![Debian-6.0.3-43.png](Debian-6.0.3-43.png "Debian-6.0.3-43.png")
![Debian-6.0.3-44.png](Debian-6.0.3-44.png "Debian-6.0.3-44.png")
![Debian-6.0.3-45.png](Debian-6.0.3-45.png "Debian-6.0.3-45.png")
![Debian-6.0.3-46.png](Debian-6.0.3-46.png "Debian-6.0.3-46.png")
![Debian-6.0.3-47.png](Debian-6.0.3-47.png "Debian-6.0.3-47.png")
![Debian-6.0.3-48.png](Debian-6.0.3-48.png "Debian-6.0.3-48.png")
![Debian-6.0.3-49.png](Debian-6.0.3-49.png "Debian-6.0.3-49.png")
![Debian-6.0.3-50.png](Debian-6.0.3-50.png "Debian-6.0.3-50.png")
![Debian-6.0.3-51.png](Debian-6.0.3-51.png "Debian-6.0.3-51.png")
![Debian-6.0.3-52.png](Debian-6.0.3-52.png "Debian-6.0.3-52.png")
![Debian-6.0.3-53.png](Debian-6.0.3-53.png "Debian-6.0.3-53.png")
![Debian-6.0.3-54.png](Debian-6.0.3-54.png "Debian-6.0.3-54.png")
![Debian-6.0.3-55.png](Debian-6.0.3-55.png "Debian-6.0.3-55.png")
![Debian-6.0.3-56.png](Debian-6.0.3-56.png "Debian-6.0.3-56.png")
![Debian-6.0.3-57.png](Debian-6.0.3-57.png "Debian-6.0.3-57.png")
![Debian-6.0.3-58.png](Debian-6.0.3-58.png "Debian-6.0.3-58.png")
![Debian-6.0.3-59.png](Debian-6.0.3-59.png "Debian-6.0.3-59.png")
![Debian-6.0.3-60.png](Debian-6.0.3-60.png "Debian-6.0.3-60.png")
![Debian-6.0.3-61.png](Debian-6.0.3-61.png "Debian-6.0.3-61.png")
![Debian-6.0.3-62.png](Debian-6.0.3-62.png "Debian-6.0.3-62.png")
![Debian-6.0.3-63.png](Debian-6.0.3-63.png "Debian-6.0.3-63.png")
![Debian-6.0.3-64.png](Debian-6.0.3-64.png "Debian-6.0.3-64.png")
![Debian-6.0.3-65.png](Debian-6.0.3-65.png "Debian-6.0.3-65.png")

## Al culminar la instalación

El servidor deberá reiniciar para que aparezca la siguiente pantalla
indicando que la instalación fue exitosa:

![Debian-6.0.3-66.png](Debian-6.0.3-66.png "Debian-6.0.3-66.png")
