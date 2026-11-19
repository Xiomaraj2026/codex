# Proposal

## Why

Comercial Aurora atiende a 300 clientes activos, procesa cerca de 1.200 pedidos al mes y recibe unas 600 solicitudes de servicio, de las cuales se pierden alrededor de 60 y unas 180 quedan sin responsable. Un piloto de seis semanas permitirá comprobar si la captura unificada, la asignación automática y el seguimiento de plazos mejoran el control de la atención.

## What Changes

- Entregar un archivo HTML autocontenido, adaptable y listo para abrir con doble clic, con una sola vista funcional y datos ficticios precargados.
- Unificar el registro manual de llamadas, correos y mensajes, con identificación de clientes por NIT, ticket inmutable y asignación rotativa entre cuatro agentes.
- Incorporar búsqueda, filtros, detalle, cambios de estado e historial, con alertas visuales a las 24, 36 y 48 horas corridas y evaluación del plazo al resolver.
- Importar directorios de clientes desde CSV o JSON y exportar y recuperar la sesión completa mediante un respaldo JSON.
- Trazar la evolución hacia la operación multiusuario con datos compartidos, las integraciones y el autoservicio.

## Capabilities

### New Capabilities

- `radicacion-solicitudes` — Captura validada, identificación única y asignación automática.
- `bandeja-seguimiento` — Consulta, cambios de estado e historial.
- `plazos-atencion` — Alertas visuales y medición del plazo al resolver.
- `datos-piloto` — Apertura local, ejemplos e intercambio de archivos.

### Modified Capabilities

## Impact

- Aplicación local para un navegador. La operación simultánea, autenticación, permisos, ERP, webhooks, notificaciones externas y autoservicio corresponden a etapas de la hoja de ruta.
- Metas operativas de referencia, a medir con datos reales en la operación: registro y asignación del 100 %, al menos 90 % de resolución en 48 horas, reducción de 20 a 12 minutos administrativos por solicitud y de COP 800.000 a COP 400.000 mensuales en reprocesos.
- Topes de referencia del proyecto A05: COP 12.000.000 de inversión inicial y COP 300.000 mensuales de operación. Son restricciones para estimar el despliegue.
