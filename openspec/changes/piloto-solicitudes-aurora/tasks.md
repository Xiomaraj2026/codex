# Tasks

## 1. Base del piloto

- [ ] 1.1 Crear `index.html` con CSS y JavaScript integrados, acciones en una sola vista y una distribución adaptable. Comprobar la apertura local sin red y el acceso al formulario, la bandeja y el detalle a 360 píxeles de ancho.
- [ ] 1.2 Definir clientes, usuarios, solicitudes y eventos como objetos y arreglos. Precargar cuatro agentes, clientes ficticios y casos con fechas relativas. Verificar que al abrir el archivo se muestran los tres tramos de alerta, historiales y ejemplos resueltos dentro y fuera del plazo.

## 2. Radicación y seguimiento

- [ ] 2.1 Implementar la selección de cliente por NIT y los catálogos del formulario. Probar casos válidos e inválidos, incluida una descripción opcional demasiado corta.
- [ ] 2.2 Registrar el ticket, la fecha, el agente y el evento inicial en una sola operación. Verificar cinco altas consecutivas, el cambio de mes en Bogotá, el agotamiento del consecutivo y que un error no avance la rotación.
- [ ] 2.3 Implementar búsqueda, filtros combinables y detalle. Comprobar una consulta por cada tipo de dato, una combinación de filtros y el estado sin resultados.
- [ ] 2.4 Implementar actualización de estado y registro de eventos con el autor seleccionado. Verificar la resolución con respuesta, el cierre posterior, el rechazo de transiciones inválidas y el orden del historial.

## 3. Plazos y archivos

- [ ] 3.1 Calcular y refrescar los tramos de 24, 36 y 48 horas mientras se usa la aplicación. Probar los límites y la actualización al volver a la ventana o restaurar una sesión.
- [ ] 3.2 Registrar el tiempo y el resultado al resolver. Probar el cumplimiento a las 48 horas exactas y el incumplimiento un segundo después, y comprobar que el resultado se conserva tras el cierre.
- [ ] 3.3 Implementar la importación de clientes desde CSV y JSON. Probar NIT como texto, valores entre comillas, actualización por NIT, conservación de los datos de tickets existentes y rechazo de archivos con errores sin cambios parciales.
- [ ] 3.4 Implementar el respaldo JSON versionado y la restauración con confirmación. Verificar con un ciclo de exportación y reapertura que se conservan eventos, solicitudes, consecutivos y rotación, y que la cancelación y los respaldos inválidos conservan la sesión.

## 4. Aceptación del piloto

- [ ] 4.1 Ejecutar en el navegador el flujo completo desde el HTML local, desde la primera apertura hasta restaurar el respaldo en una nueva sesión. Registrar el resultado de los escenarios de aceptación.
- [ ] 4.2 Medir la captura manual, la carga de bandeja y la búsqueda con 300 clientes y 600 solicitudes ficticias. Registrar los tiempos junto con el navegador y contrastarlos con las metas del diseño.
