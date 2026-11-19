# Spec Delta

## Purpose

Permitir que el piloto se pruebe al abrirlo en un navegador y que sus datos puedan guardarse y recuperarse mediante archivos.

## ADDED Requirements

### Requirement: Apertura local y datos ficticios

La aplicación SHALL distribuirse en un solo archivo HTML con CSS y JavaScript integrados y funcionar al abrirlo con doble clic, incluso sin internet. SHALL presentar una vista adaptable y cargar clientes ficticios, cuatro agentes y solicitudes de ejemplo en cada sesión que se inicie sin cargar un respaldo.

#### Scenario: Prueba inmediata al abrir el archivo
- **WHEN** el usuario abre el HTML local sin conexión
- **THEN** puede registrar y consultar solicitudes con los datos ficticios disponibles
- **AND** la bandeja muestra casos activos en los tres tramos de alerta y el detalle de los ejemplos incluye historial y resultados de cumplimiento dentro y fuera del plazo

#### Scenario: Uso en pantalla estrecha
- **WHEN** el archivo se abre en una ventana de 360 píxeles de ancho
- **THEN** la radicación, la navegación por la bandeja y el detalle siguen disponibles sin desplazamiento horizontal de la página

### Requirement: Importación del directorio de clientes

La aplicación SHALL importar registros con los campos obligatorios `nit` y `nombre` desde un CSV con encabezados o un arreglo JSON. El NIT SHALL tratarse como texto. El directorio SHALL incorporar clientes por NIT y actualizar las coincidencias sin reemplazar los datos de cliente registrados en tickets existentes.

#### Scenario: Importación y actualización por NIT
- **WHEN** se carga un directorio válido con un NIT nuevo y otro que ya existe
- **THEN** ambos clientes están disponibles en el formulario y el existente aparece con la razón social actualizada
- **AND** los tickets existentes conservan la razón social registrada al crearlos

#### Scenario: Directorio inválido
- **WHEN** el archivo tiene un formato incorrecto, campos obligatorios vacíos o un NIT duplicado dentro del archivo
- **THEN** la aplicación informa el problema y conserva todo el directorio anterior

### Requirement: Respaldo y restauración de la sesión

La aplicación SHALL exportar un archivo JSON versionado con clientes, usuarios, solicitudes, historial, consecutivos y posición de la rotación. SHALL validar el formato y las referencias de un respaldo antes de restaurarlo y pedir confirmación para sustituir la sesión en uso. Ante un respaldo inválido o una cancelación, SHALL conservar los datos en uso.

#### Scenario: Reanudar el trabajo desde un respaldo
- **GIVEN** el usuario exportó una sesión con solicitudes y cambios de estado
- **WHEN** reabre el HTML, carga el respaldo y confirma la restauración
- **THEN** se recuperan los datos guardados y la siguiente radicación continúa los consecutivos y la rotación

#### Scenario: Respaldo inválido o incompatible
- **WHEN** se carga un respaldo con JSON inválido, una versión incompatible, tickets duplicados o referencias a agentes inexistentes
- **THEN** la aplicación explica el problema y conserva la sesión anterior

#### Scenario: Restauración cancelada
- **WHEN** el usuario cancela la confirmación de un respaldo válido
- **THEN** la sesión en uso se conserva
