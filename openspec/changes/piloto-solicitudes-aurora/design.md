# Design

## Context

El repositorio contiene la configuración de OpenSpec para Codex. El piloto A05 incorpora la primera aplicación y se distribuye como un único HTML local. Se conserva el horizonte de seis semanas de la propuesta y se programa por separado la arquitectura multiusuario de la especificación técnica de referencia.

## Goals / Non-Goals

**Goals**

- Mantener separadas en el mismo archivo la interfaz, las reglas de negocio y las operaciones con archivos.
- Hacer que el flujo completo pueda probarse por doble clic, incluidos los umbrales de tiempo, sin servicios externos.
- Preservar el formato de dominio necesario para una migración posterior de datos.

**Non-Goals**

- Autenticación y autorización de usuarios, base de datos compartida y garantías de auditoría contra la modificación externa de archivos.
- Procesos en segundo plano fuera del navegador, integraciones con ERP y canales, y acceso de clientes.

## Decisions

1. **HTML autocontenido.** Integrar CSS y JavaScript en `index.html` y usar las funciones nativas del navegador. La sesión vive en objetos y arreglos JS. El guardado queda bajo control del usuario mediante el respaldo JSON, lo que permite recuperar una sesión al mover el HTML a otro equipo. Las funciones de dominio se mantendrán separadas del DOM dentro del mismo archivo.
2. **Modelo de datos.** La sesión contiene clientes indexados por NIT, cuatro agentes, solicitudes y eventos por ticket. Guardar una copia del NIT y la razón social en cada solicitud conserva el contexto de su radicación tras una actualización del directorio. El usuario se selecciona en la interfaz para identificar al autor de cada evento. Todas las funciones se mantienen disponibles en la vista, con independencia del autor seleccionado.
3. **Identificación y asignación.** Usar un consecutivo mensual de 0001 a 9999, con el mes calculado para Bogotá. Validar primero la operación y guardar juntos ticket, responsable, evento inicial y avance del turno. Conservar en el respaldo los consecutivos y el siguiente turno, y verificar su consistencia con los registros restaurados.
4. **Reloj y plazos.** Guardar instantes ISO 8601 y calcular las diferencias de tiempo en milisegundos para aplicar los umbrales. Actualizar la bandeja al abrir, restaurar, volver a enfocar la ventana y periódicamente durante la sesión. Generar los ejemplos con fechas relativas a la apertura para que los tres tramos puedan verse de inmediato. Si el reloj del dispositivo indica que la resolución precede a la recepción, informar el error y permitir corregir el reloj antes de resolver.
5. **Archivos.** Leer únicamente archivos seleccionados por el usuario. Aceptar CSV UTF-8 con encabezados y campos entre comillas, y JSON con los campos `nit` y `nombre`. Validar cada archivo en memoria antes de aplicar cambios. Para restaurar, validar versión, unicidad de identificadores, catálogos, coherencia de fechas y referencias. Mostrar el contenido importado como texto.
6. **Prueba de uso.** Usar la página local para las pruebas de aceptación. Durante el piloto, medir como metas de usabilidad la captura manual en menos de 30 segundos y la búsqueda y carga de bandeja en hasta 1,5 segundos con un directorio de prueba de 300 clientes y 600 solicitudes.

## Risks / Trade-offs

- Cerrar la pestaña finaliza la sesión. La interfaz pone a mano la exportación y pide confirmación al sustituir los datos con un respaldo.
- Dos copias abiertas pueden generar el mismo consecutivo en sesiones independientes. El piloto usa un respaldo por sesión y el paso a multiusuario requiere reconciliar los identificadores y centralizar su emisión.
- El reloj del dispositivo y el autor seleccionado sirven para probar el flujo. En la operación compartida se usarán marcas de tiempo del servidor e identidades autenticadas.
- Los plazos pueden dejar de refrescarse temporalmente cuando el navegador suspende una pestaña. El valor se recalcula al volver a la ventana y al consultar o actualizar una solicitud.

## Migration Plan

1. **Piloto local de seis semanas.** Semana 1 para cerrar requisitos y escenarios. Semanas 2 y 3 para registro, asignación y bandeja. Semana 4 para historial, plazos e intercambio de archivos. Semanas 5 y 6 para pruebas con usuarios y ajustes. Cada entrega del HTML se valida por doble clic. Se puede volver al HTML anterior con un respaldo que use un formato compatible.
2. **Operación multiusuario.** Definir un nuevo cambio OpenSpec para una API, base relacional y despliegue por HTTPS. Incorporar cuentas individuales y permisos de agente, coordinador y administrador. La API asignará tickets y responsables en una transacción y conservará un historial de auditoría gestionado en el servidor. Importar únicamente datos autorizados y validados, preservar identificadores y eventos, y resolver duplicados antes de habilitar la escritura compartida. Verificar acceso concurrente de cuatro agentes y un coordinador. Estimar la etapa frente a los topes del proyecto antes del despliegue.
3. **Integraciones y SLA.** Incorporar de forma incremental la ingesta de correos y mensajes, la consulta de clientes y pedidos en el ERP en modo lectura y la evaluación de plazos en el servidor con notificaciones sin depender de que el navegador esté abierto.
4. **Autoservicio y analítica.** Evaluar una consulta externa del estado de atención, análisis de motivos recurrentes y sincronización bidireccional con el ERP una vez validada la integración de lectura.
