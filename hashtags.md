NiMbox permite que las notas sean agruadas por **Hashtags**. Los
**Hashtags** son mecanismos para categorizar una nota de forma tal que
el texto

Los acceder ciertas de sus funcionalidades a través de servicios web. El
punto de contacto de estos sitios web es la dirección segura
<https://host/direct/items>. Los servicios web disponibles por el
momento son:

## Agregar una nota

Es posible agregar notas a cualquiera de los elementos de datos
representados en NiMbox. Los parámetros son:

  - thingyId:el elemento al cual conectarle la nota. Típicamente este
    elemento es un contacto.  
    contextName (opcional):el nombre del contexto al cual conectarle la
    nota.  
    description:el contenido de la nota.

Para crear una nota

    wget --user=jlopez --password=comic --no-check-certificate -qO- \
      <nowiki>"https://host/direct/items/notes/create?thingyId=24&description=La+nota+se+proceso+exitosamente"</nowiki>

En caso de éxito el resultado será un json parecido a este:
