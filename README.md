# n8n_moddle_assign_save_grade

Automatización de calificaciones en Moodle utilizando n8n y Web Services.

## 🎯 Objetivo

Este proyecto permite automatizar la asignación de calificaciones en tareas de Moodle a partir de una hoja de cálculo de Google Sheets. El sistema evalúa si los estudiantes han entregado la tarea y asigna:

- ✅ Calificación máxima si hay entrega.
- ❌ Calificación mínima (0) y comentario si no hay entrega.

## 🧩 Componentes del flujo

El escenario está construido en n8n y utiliza los siguientes módulos:

1. **Google Sheets → Formulario de entrada**
   - Campos: URL de la tarea, cmid, wstoken, userid, calificaciones y comentarios.

2. **HTTP Request → Obtener assignmentid**
   - Función: `core_course_get_course_module`
   - Extrae el `assignmentid` desde el `cmid`.

3. **HTTP Request → Obtener entregas**
   - Función: `mod_assign_get_submissions`
   - Obtiene el estado de entrega de cada estudiante.

4. **JavaScript Code → Procesar entregas**
   - Evalúa si cada estudiante entregó o no.
   - Asigna calificación y comentario según el resultado.

5. **HTTP Request → Guardar calificación**
   - Función: `mod_assign_save_grade`
   - Envía la calificación y comentario a Moodle.

## 📦 Requisitos

- Acceso a Moodle con Web Services habilitados.
- Token con permisos para:
  - `core_course_get_course_module`
  - `mod_assign_get_submissions`
  - `mod_assign_save_grade`
- n8n con módulos HTTP y JavaScript habilitados.

## 🛠 Configuración

1. Completa la hoja de cálculo con los siguientes campos:
   - `cmid`: ID del módulo de la tarea.
   - `wstoken`: Token de acceso a Moodle.
   - `userid`: ID del estudiante.
   - `Calificación Máxima`, `Calificación Mínima`
   - `Comentario Calificación Max`, `Comentario Calificación Minima`

2. Ejecuta el escenario en n8n.

3. Verifica los resultados en Moodle.

## 📄 Licencia

Este proyecto está disponible bajo la licencia MIT.

## 🤝 Contribuciones

¡Se aceptan mejoras! Puedes enviar pull requests o abrir issues para sugerencias.
