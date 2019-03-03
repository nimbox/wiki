## Todas las notas

    SELECT
        Thingy.createdOn AS noteCreatedOn,
        Thingy.createdBy AS noteCreatedBy,
        Note.description AS noteDescription,
        COALESCE(Contact.name, TRIM(CONCAT(Contact.firstName,' ',Contact.lastName))) AS noteReferenceContact  
    FROM 
        Note JOIN Thingy ON Note.id = Thingy.id
             JOIN ThingyRelation ON Note.id = ThingyRelation.fromId AND ThingyRelation.code = '@' 
             JOIN Contact ON ThingyRelation.toId = Contact.id

| campo                | descripción                                   |
| -------------------- | --------------------------------------------- |
| noteCreatedOn        | fecha en que se creó la nota                  |
| noteCreatedBy        | usuario que creó la nota                      |
| noteDescription      | descripción de la nota                        |
| noteReferenceContact | nombre del contacto relacionado con esta nota |

## Todas las tareas

    SELECT
        Thingy.createdOn AS taskCreatedOn,
        Thingy.createdBy AS taskCreatedBy,
        Task.due AS taskDue,
        Task.completed AS taskCompleted,
        Task.supervised AS taskSupervised,
        Task.description AS taskDescription,
        COALESCE(Contact.name, TRIM(CONCAT(Contact.firstName,' ',Contact.lastName))) AS taskReferenceContact
    FROM 
        Task JOIN Thingy ON Task.id = Thingy.id
             JOIN ThingyRelation ON Task.id = ThingyRelation.fromId AND ThingyRelation.code = '@' 
             JOIN Contact ON ThingyRelation.toId = Contact.id

| campo                | descripción                                    |
| -------------------- | ---------------------------------------------- |
| taskCreatedOn        | fecha en que se creó la tarea                  |
| taskCreatedBy        | usuario que creó la tarea                      |
| taskDue              | fecha espera de culminación de la tarea        |
| taskCompleted        | fecha en que realmente se completó la tarea    |
| taskSupervised       | fecha en que realmente se supervisó la tarea   |
| taskDescription      | descripción de la tarea                        |
| taskReferenceContact | nombre del contacto relacionado con esta tarea |
