# Tasks

## 1. Base del piloto

- [x] 1.1 Crear `index.html` con CSS y JavaScript integrados, acciones en una sola vista y una distribución adaptable. Comprobar la apertura local sin red y el acceso al formulario, la bandeja y el detalle a 360 píxeles de ancho.
- [x] 1.2 Definir clientes, usuarios, solicitudes y eventos como objetos y arreglos. Precargar cuatro agentes, clientes ficticios y casos con fechas relativas. Verificar que al abrir el archivo se muestran los tres tramos de alerta, historiales y ejemplos resueltos dentro y fuera del plazo.

## 2. Radicación y seguimiento

- [x] 2.1 Implementar la selección de cliente por NIT y los catálogos del formulario. Probar casos válidos e inválidos, incluida una descripción opcional demasiado corta.
- [x] 2.2 Registrar el ticket, la fecha, el agente y el evento inicial en una sola operación. Verificar cinco altas consecutivas, el cambio de mes en Bogotá, el agotamiento del consecutivo y que un error no avance la rotación.
- [x] 2.3 Implementar búsqueda, filtros combinables y detalle. Comprobar una consulta por cada tipo de dato, una combinación de filtros y el estado sin resultados.
- [x] 2.4 Implementar actualización de estado y registro de eventos con el autor seleccionado. Verificar la resolución con respuesta, el cierre posterior, el rechazo de transiciones inválidas y el orden del historial.

## 3. Plazos y archivos

- [x] 3.1 Calcular y refrescar los tramos de 24, 36 y 48 horas mientras se usa la aplicación. Probar los límites y la actualización al volver a la ventana o restaurar una sesión.
- [x] 3.2 Registrar el tiempo y el resultado al resolver. Probar el cumplimiento a las 48 horas exactas y el incumplimiento un segundo después, y comprobar que el resultado se conserva tras el cierre.
- [x] 3.3 Implementar la importación de clientes desde CSV y JSON. Probar NIT como texto, valores entre comillas, actualización por NIT, conservación de los datos de tickets existentes y rechazo de archivos con errores sin cambios parciales.
- [x] 3.4 Implementar el respaldo JSON versionado y la restauración con confirmación. Verificar con un ciclo de exportación y reapertura que se conservan eventos, solicitudes, consecutivos y rotación, y que la cancelación y los respaldos inválidos conservan la sesión.

## 4. Aceptación del piloto

- [x] 4.1 Ejecutar en el navegador el flujo completo desde el HTML local, desde la primera apertura hasta restaurar el respaldo en una nueva sesión. Registrar el resultado de los escenarios de aceptación.
- [x] 4.2 Medir la captura manual, la carga de bandeja y la búsqueda con 300 clientes y 600 solicitudes ficticias. Registrar los tiempos junto con el navegador y contrastarlos con las metas del diseño.

## Resultados de verificación

- Chromium 156.0.8078.79 ejecutó el contenido de `index.html` sin red, con una vista de 360 píxeles y sin desplazamiento horizontal. Se comprobó el acceso al formulario, la bandeja y el detalle.
- Pasaron las pruebas de cinco altas con rotación, cambio de mes en Bogotá, agotamiento de consecutivos, búsqueda y filtros, cambios de estado e historial. También se comprobó la actualización de alertas sin recarga y la resolución a las 48 horas y un segundo después.
- Pasaron las pruebas de importación CSV y JSON, rechazo de datos inválidos, exportación, cancelación y restauración en una sesión nueva. El respaldo conservó los tickets, los eventos y la posición de la rotación.
- Con 300 clientes y 600 solicitudes ficticias, se observaron 87 ms para renderizar la bandeja, 32 ms para buscar y 2,3 s para una captura con escritura simulada. Las metas son 1,5 s para bandeja y búsqueda y 30 s para captura. La captura con agentes reales corresponde a las sesiones del piloto.
- La prueba automatizada cargó el contenido del HTML en Chromium. El navegador compartido bloqueó la apertura de direcciones locales y la conexión de la vista previa no estuvo disponible.
