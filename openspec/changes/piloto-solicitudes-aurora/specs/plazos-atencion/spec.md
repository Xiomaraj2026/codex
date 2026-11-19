# Spec Delta

## Purpose

Hacer visibles las solicitudes que se acercan al plazo de atención y medir el cumplimiento al resolverlas.

## ADDED Requirements

### Requirement: Alertas de antigüedad durante la atención

La bandeja SHALL mostrar el tramo vigente de las solicitudes activas a las 24, 36 y 48 horas corridas desde su recepción y actualizarlo sin que el usuario recargue la página. El umbral deberá ser identificable por texto. El tiempo en estados pendientes SHALL contar para el plazo.

#### Scenario: Umbrales de las solicitudes activas
- **GIVEN** la aplicación está abierta y hay solicitudes pendientes
- **WHEN** el tiempo transcurrido alcanza 24, 36 o 48 horas
- **THEN** la bandeja indica el tramo de 24 a menos de 36, de 36 a menos de 48, o de 48 horas en adelante, respectivamente
- **AND** antes de 24 horas no muestra alerta

#### Scenario: Recuperación de casos con antigüedad
- **WHEN** se restaura un respaldo con una solicitud activa recibida hace 37 horas
- **THEN** la bandeja muestra el tramo de 36 a menos de 48 horas

### Requirement: Medición del plazo al resolver

Al resolver una solicitud la aplicación SHALL guardar la fecha y hora de resolución, las horas corridas desde la recepción y el indicador de cumplimiento. SHALL marcar cumplimiento cuando el tiempo transcurrido sea menor o igual a 48 horas y evaluar el umbral sobre la duración sin redondear.

#### Scenario: Resolución en el límite
- **WHEN** el usuario resuelve una solicitud exactamente 48 horas después de su recepción
- **THEN** el detalle muestra la fecha de resolución, 48 horas y un resultado de cumplimiento
- **AND** la alerta de solicitud activa desaparece

#### Scenario: Resolución después del límite
- **WHEN** se resuelve la solicitud 48 horas y un segundo después de la recepción
- **THEN** la aplicación registra incumplimiento aunque la duración visible se haya redondeado a 48 horas
- **AND** el resultado se conserva si el caso pasa a `Cerrado`
