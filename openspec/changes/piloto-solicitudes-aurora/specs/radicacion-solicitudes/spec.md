# Spec Delta

## Purpose

Estandarizar la entrada de solicitudes de atención y garantizar que cada solicitud registrada tenga un ticket y un agente responsable.

## ADDED Requirements

### Requirement: Captura manual con datos válidos

La aplicación SHALL registrar solicitudes con un cliente del directorio identificado por NIT, un canal y un tipo válidos. La referencia al pedido ERP y la descripción son opcionales. Si se ingresa una descripción, SHALL tener al menos 10 caracteres tras quitar espacios de los extremos.

#### Scenario: Radicación de una solicitud telefónica
- **GIVEN** el directorio contiene al cliente con NIT `900123456`
- **WHEN** el usuario selecciona ese cliente, el canal `Llamada_Telefonica` y el tipo `Inconformidad_Envio` y guarda sin número de pedido
- **THEN** la aplicación registra la solicitud con NIT y razón social, confirma el guardado y la muestra en la bandeja

#### Scenario: Rechazo de una radicación inválida
- **WHEN** se intenta guardar sin cliente, canal o tipo, con un NIT desconocido, con un valor fuera del catálogo o con una descripción ingresada de 1 a 9 caracteres
- **THEN** la aplicación identifica el campo inválido y conserva lo ingresado para que el usuario lo corrija
- **AND** no crea un ticket ni avanza la rotación

### Requirement: Canales y tipos de catálogo

La aplicación SHALL ofrecer los canales `Mensajeria`, `Correo_Electronico` y `Llamada_Telefonica`, y los tipos `Consulta_Stock`, `Estado_Pedido`, `Inconformidad_Envio`, `Facturacion_Cobro` y `Devolucion`.

#### Scenario: Captura guiada
- **WHEN** el usuario abre el formulario de radicación
- **THEN** puede seleccionar los valores de los catálogos sin escribir categorías libres

### Requirement: Identificación y estado inicial

Cada solicitud registrada SHALL recibir un identificador único e inmutable con formato `AUR-YYYYMM-XXXX`, una fecha de recepción ISO 8601 tomada del reloj del dispositivo al guardar y el estado inicial `Nuevo`. El prefijo mensual SHALL corresponder a la fecha de recepción en la zona `America/Bogota`.

#### Scenario: Dos registros en el mismo mes
- **WHEN** se guardan dos solicitudes válidas con el mismo mes de recepción
- **THEN** los tickets comparten el prefijo mensual y tienen sufijos distintos
- **AND** cambiar de estado o restaurar un respaldo conserva el ticket original

#### Scenario: Capacidad agotada en el mes
- **WHEN** se intenta registrar una solicitud y ya se emitió el último consecutivo de cuatro dígitos del mes
- **THEN** la aplicación informa que se agotó el consecutivo y conserva los datos de la solicitud pendientes de guardar

### Requirement: Asignación rotativa al guardar

La aplicación SHALL asignar cada nueva solicitud al siguiente de cuatro agentes en un orden fijo y avanzar la rotación solo al guardar con éxito. La identidad del usuario que registra el caso SHALL ser independiente del responsable asignado.

#### Scenario: Rotación completa
- **WHEN** se guardan cinco solicitudes válidas consecutivas
- **THEN** las primeras cuatro quedan asignadas a cuatro agentes diferentes y la quinta queda asignada al agente de la primera
