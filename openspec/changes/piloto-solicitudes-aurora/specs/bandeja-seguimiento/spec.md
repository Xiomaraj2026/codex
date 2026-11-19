# Spec Delta

## Purpose

Facilitar la consulta, actualización y trazabilidad de cada solicitud durante todo su ciclo de atención.

## ADDED Requirements

### Requirement: Bandeja con búsqueda y filtros

La aplicación SHALL ofrecer en una sola vista la bandeja y acceso al formulario de radicación y al detalle. La bandeja SHALL permitir buscar por ticket, NIT o razón social y combinar la búsqueda con filtros de estado y agente. El detalle SHALL mostrar los datos de registro, el responsable, el estado y el historial.

#### Scenario: Consulta por cliente y estado
- **WHEN** el usuario busca por nombre o NIT y filtra por estado y agente
- **THEN** la bandeja muestra únicamente las solicitudes que cumplen todos los criterios
- **AND** al seleccionar una fila se puede consultar su detalle y su historial

#### Scenario: Consulta sin coincidencias
- **WHEN** la combinación de búsqueda y filtros no coincide con ninguna solicitud
- **THEN** la aplicación muestra un estado vacío y permite limpiar los criterios

### Requirement: Actualización del estado de atención

La aplicación SHALL permitir cambios entre los estados activos `Nuevo`, `En_Proceso`, `Pendiente_Logistica` y `Pendiente_Ventas`, y permitir resolver desde cualquiera de ellos con una respuesta de fondo. SHALL permitir cerrar únicamente solicitudes en estado `Resuelto` y conservar el resultado de resolución de los casos cerrados.

#### Scenario: Seguimiento hasta el cierre
- **GIVEN** una solicitud en estado `En_Proceso`
- **WHEN** el usuario la marca como `Pendiente_Logistica`, después la resuelve con una respuesta y finalmente la cierra
- **THEN** la solicitud queda en estado `Cerrado` y conserva los datos de resolución

#### Scenario: Actualización inválida
- **WHEN** se intenta cerrar una solicitud activa, resolver sin respuesta o reabrir un caso resuelto o cerrado
- **THEN** la aplicación impide el cambio y conserva su estado e historial

### Requirement: Historial de eventos por solicitud

La aplicación SHALL añadir al historial un evento al registrar una solicitud y al cambiar su estado. Cada evento SHALL conservar un identificador, ticket, fecha ISO 8601, usuario seleccionado, acción y estados anterior y nuevo. SHALL incluir el comentario cuando se ingrese. En el evento inicial, el estado anterior queda vacío. La aplicación SHALL presentar el historial en orden cronológico sin opciones de edición ni eliminación.

#### Scenario: Historial de registro y actualización
- **WHEN** un usuario seleccionado registra una solicitud y luego cambia su estado con un comentario
- **THEN** el detalle muestra el evento de registro seguido del cambio de estado, con su autor, fecha y comentario
- **AND** el responsable asignado se muestra por separado del autor del evento
