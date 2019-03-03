Hay muchas formas de ver los clientes. Estamos experimentando con esta a
ver qué opinan nuestros
usuarios.

## La clasificación de clientes permite separarlos en función de su historia de pagos y de su tamaño en ventas

Para realizar este análisis no se toma en cuenta las facturas pendientes
del cliente, se toma en cuenta el historico de facturas cerradas y sus
pagos.

El cliente puede ser entendido en función de dos dimensiones
importantes: (1) ¿qué tanto se retrasa en los pagos? y (2) ¿qué tan
grande es en función de sus ventas? Estamos mostrando cada una de estas
dimensiones como un [diagrama de lunas](diagrama_de_lunas "wikilink").
La primera luna representa qué tanto se retrasa en los pagos y mientras
se va poniendo más roja significa que tiene mas días de retraso. La
segunda luna representa qué tan grande es el cliente y mientras se va
poniendo más verde significa que tiene mas ventas.

Adicionalmente estamos colocando una información resumida en las lunas
que permiten cuantificar mejor esta relación tal como se explica en la
siguiente figura:

![clasificacion-de-clientes.png](clasificacion-de-clientes.png
"clasificacion-de-clientes.png")

El objetivo es poder visualizar rápidamente si el cliente paga a tiempo
y si es grande. En esta visualización hay que buscar la **menor cantidad
de rojo** en la luna de pagos y la **mayor cantidad de verde** en la
luna de ventas.

Este cálculo se realiza sobre las facturas de los últimos 365 días.

## Este clasificación se realiza en función de quintiles

Cada empresa tiene su dinámica de negocio donde los días de retraso y el
tamaño de sus clientes son completamente diferentes. Para poder hacer
comparaciones en estas situaciones utilizamos el concepto de
[quintiles](http://es.wikipedia.org/wiki/Cuantil#Quintiles) para dividir
los clientes en cinco categorías, cada una de igual tamaño. En cada uno
de los quintiles queda el 20% de los clientes.

La mejor forma de entender este concepto es con un ejemplo. Asumamos que
tenemos los siguientes clientes con su promedio de días de retraso y su
total de ventas durante los últimos 365
días.

| Cliente | Retraso | Ventas | Quintil de retraso | Quintil de ventas | Representación                                                                                                                                     |
| ------- | ------- | ------ | ------------------ | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| A       | \-26    | 71546  | 0                  | 3                 | ![delay-days-moon-16-0.png](delay-days-moon-16-0.png "delay-days-moon-16-0.png") ![sales-moon-16-3.png](sales-moon-16-3.png "sales-moon-16-3.png") |
| B       | \-17    | 78464  | 1                  | 4                 | ![delay-days-moon-16-1.png](delay-days-moon-16-1.png "delay-days-moon-16-1.png") ![sales-moon-16-4.png](sales-moon-16-4.png "sales-moon-16-4.png") |
| C       | 18      | 83628  | 1                  | 4                 | ![delay-days-moon-16-1.png](delay-days-moon-16-1.png "delay-days-moon-16-1.png") ![sales-moon-16-4.png](sales-moon-16-4.png "sales-moon-16-4.png") |
| D       | 32      | 25441  | 2                  | 1                 | ![delay-days-moon-16-2.png](delay-days-moon-16-2.png "delay-days-moon-16-2.png") ![sales-moon-16-1.png](sales-moon-16-1.png "sales-moon-16-1.png") |
| E       | 51      | 17787  | 3                  | 0                 | ![delay-days-moon-16-3.png](delay-days-moon-16-3.png "delay-days-moon-16-3.png") ![sales-moon-16-0.png](sales-moon-16-0.png "sales-moon-16-0.png") |
| F       | 27      | 31411  | 2                  | 2                 | ![delay-days-moon-16-2.png](delay-days-moon-16-2.png "delay-days-moon-16-2.png") ![sales-moon-16-2.png](sales-moon-16-2.png "sales-moon-16-2.png") |
| G       | 18      | 45086  | 1                  | 3                 | ![delay-days-moon-16-1.png](delay-days-moon-16-1.png "delay-days-moon-16-1.png") ![sales-moon-16-3.png](sales-moon-16-3.png "sales-moon-16-3.png") |
| H       | 21      | 18135  | 2                  | 1                 | ![delay-days-moon-16-2.png](delay-days-moon-16-2.png "delay-days-moon-16-2.png") ![sales-moon-16-1.png](sales-moon-16-1.png "sales-moon-16-1.png") |
| I       | 105     | 39192  | 4                  | 2                 | ![delay-days-moon-16-4.png](delay-days-moon-16-4.png "delay-days-moon-16-4.png") ![sales-moon-16-2.png](sales-moon-16-2.png "sales-moon-16-2.png") |
| J       | 64      | 84306  | 3                  | 4                 | ![delay-days-moon-16-3.png](delay-days-moon-16-3.png "delay-days-moon-16-3.png") ![sales-moon-16-4.png](sales-moon-16-4.png "sales-moon-16-4.png") |
| K       | 54      | 26003  | 3                  | 2                 | ![delay-days-moon-16-3.png](delay-days-moon-16-3.png "delay-days-moon-16-3.png") ![sales-moon-16-2.png](sales-moon-16-2.png "sales-moon-16-2.png") |
| L       | 80      | 9545   | 4                  | 0                 | ![delay-days-moon-16-4.png](delay-days-moon-16-4.png "delay-days-moon-16-4.png") ![sales-moon-16-0.png](sales-moon-16-0.png "sales-moon-16-0.png") |
| M       | \-22    | 2632   | 0                  | 0                 | ![delay-days-moon-16-0.png](delay-days-moon-16-0.png "delay-days-moon-16-0.png") ![sales-moon-16-0.png](sales-moon-16-0.png "sales-moon-16-0.png") |
| N       | \-27    | 46697  | 0                  | 3                 | ![delay-days-moon-16-0.png](delay-days-moon-16-0.png "delay-days-moon-16-0.png") ![sales-moon-16-3.png](sales-moon-16-3.png "sales-moon-16-3.png") |
| O       | 81      | 19304  | 4                  | 1                 | ![delay-days-moon-16-4.png](delay-days-moon-16-4.png "delay-days-moon-16-4.png") ![sales-moon-16-1.png](sales-moon-16-1.png "sales-moon-16-1.png") |

Si ordenas los clientes por días de retraso de forma creciente (es
posible hacer esto presionando el ícono justo al lado del título de cada
columna) podrás ver que el primer 20% de los clientes queda en el
quintil 0 (que son los que menos se retrasan), el próximo 20% queda en
el quintil 1, y así sucesivamente. De igual forma, si se ordenan los
clientes por ventas tenemos que el primer 20% de los clientes queda en
el quintil 0 (que son los mas pequeños).

Los quintiles están representados por las lunas. La luna que está mitad
llena y mitad vacía representa el quintil 2 y ahí están los clientes
completamente promedio. La mejor forma de interpretar los quintiles es
que los que están el quintil 2 son los clientes promedio y están
representados por una luna. En la medida que comienza a crecer o
decrecer la luna se van haciendo mejores o peores en función de si es
retraso o ventas lo que se está observando.

## Calculo de la luna de retraso

Para calcular el retraso promedio del cliente, consideramos todas las
facturas pagadas del cliente, emitidas en los últimos 365 días. A cada
una de estas facturas le calculamos el retraso ponderado por el monto
del pago. Finalmente promediamos los retrasos ponderados y eso sería el
retraso del cliente.

### Calculo ponderado del retraso de una factura

Para calcular el retraso cuando existen multiples pagos a una factura
utilizamos en retraso ponderado por monto. Podemos ilustrarlo con el
siguiente ejemplo:

Factura de Bs. 1000. Se pago en dos transacciónes: un pago de Bs. 900
con 10 dias de retraso el segundo pago de Bs. 100 con 60 dias de retraso

``` 
 [ (10d * 900Bs.) + (60d * 100Bs.) ] / (900Bs. + 100Bs.) = 15 d 
```

El primer pago pesará más. lo que implica el retraso ponderado será 15
diás
