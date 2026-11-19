# Desarrollo guiado por especificaciones

- Las especificaciones vigentes están en `openspec/specs/` y los cambios activos en `openspec/changes/`.
- Usa las skills de `.agents/skills/` para proponer, actualizar, implementar, sincronizar y archivar cambios. El esquema `spec-driven` organiza cada cambio en propuesta, especificaciones, diseño y tareas.
- En una tarea nueva de Codex Cloud, ejecuta `npm ci` desde la raíz si aún no están instaladas las dependencias de desarrollo. Usa `npm run openspec -- <comando>` para ejecutar la versión local cuando las skills indiquen un comando `openspec`. Por ejemplo, `openspec list --json` se ejecuta como `npm run openspec -- list --json`.
