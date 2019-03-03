La información que utiliza  para realizar todos los cálculos y mostrar
todos los análisis, proviene del sistema administrativo. Con la
finalidad de no sobrecargar el sistema administrativo,  obtiene la
información mediante 2 procesos de replicación

## Replicacion incremental

Esta replicación se ejecuta de manera automática cada quince (15)
minutos y solo **obtiene información nueva**. Por ejemplo nuevas
facturas, nuevos cobros, cheques devueltos, entradas o salidas de
mercancía, entre otros. En caso de que un documento haya sido eliminado
este cambio no se verá reflejado en  luego de esta replicación.

Este proceso no puede ser modificado ni ejecutado manualmente.

## Replicación completa

Esta replicación se ejecuta de manera automática 1 vez al día,
generalmente en horas de la madrugada ya que es importante que el uso
del sistema administrativo sea mínimo. Durante la ejecución,  compara
toda la información contra el sistema administrativo, en busca de
eliminaciones y/o modificaciones, con la finalidad de actualizar
completamente ambos sistemas.

Es posible ejecutar manualmente este proceso con el fin de sincronizar
el sistema administrativo con , si deseas conocer como se puede realizar
este proceso haz click aquí.
