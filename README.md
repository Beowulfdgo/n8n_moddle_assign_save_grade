n8n Moodle Auto-Grader
Automatización de calificaciones masivas en Moodle mediante web services REST, diseñado para asignar calificaciones automáticas basadas en el estado de entrega de tareas.

🎯 Objetivo
Automatizar el proceso de calificación en Moodle asignando automáticamente:

Calificación máxima + comentario personalizado para estudiantes que sí entregaron la tarea

Calificación mínima + comentario personalizado para estudiantes que no entregaron la tarea

Soporta tanto calificaciones numéricas como escalas personalizadas (ej: Sí/No).

🚀 Características principales
✅ Extracción automática de cmid desde URLs de Moodle

✅ Soporte dual: Escala numérica y escala Sí/No

✅ Procesamiento masivo: Califica a todos los estudiantes de una actividad simultáneamente

✅ Interfaz amigable: Formulario web para configuración fácil

✅ Retroalimentación visual: Resultados claros con HTML personalizado

✅ Manejo de errores: Validaciones y respuestas apropiadas para casos fallidos

🧩 Arquitectura del flujo
1. Formulario de Configuración (form submission Actividad)
URL de la actividad: Se extrae automáticamente el cmid

wstoken: Token de seguridad de Moodle Web Services

Calificaciones: Máxima y mínima a asignar

Comentarios: Retroalimentación personalizada para cada caso

2. Extracción de datos (Code in JavaScript2)
Parseo automático de la URL para obtener el cmid

Estructuración de datos para el procesamiento posterior

3. Obtención del assignmentid (HTTP Request: Obtener assignmentid)
Web Service: core_course_get_course_module

Convierte cmid en assignmentid necesario para Moodle

4. Consulta de entregas (HTTP Request: Obtener entregas)
Web Service: mod_assign_get_submissions

Obtiene el estado de entrega de todos los estudiantes

5. Procesamiento inteligente (Code in JavaScript)
Detección automática de escala: Si Max=1 y Min=0 → escala Sí/No (2=Yes, 1=No)

Asignación de calificaciones: Basada en el estado submitted

Asignación de comentarios: Personalizados por condición

6. Guardado en Moodle (HTTP Request: guardar calificacion)
Web Service: mod_assign_save_grade

Envía calificación, comentario y estado de evaluación

7. Reporte de resultados
Éxito: Muestra cantidad de tareas calificadas

Error: Mensaje descriptivo cuando no se procesan tareas

📦 Requisitos del sistema
Moodle
Web Services habilitados

Token con permisos para:

core_course_get_course_module

mod_assign_get_submissions

mod_assign_save_grade

REST protocol activado

n8n
Módulos requeridos:

n8n-nodes-base.httpRequest

n8n-nodes-base.code (JavaScript)

n8n-nodes-base.formTrigger

n8n-nodes-base.set

n8n-nodes-base.if

n8n-nodes-base.html

🛠 Configuración paso a paso
1. Obtener el wstoken de Moodle
text
Administración del sitio > Servidores > Servicios externos > Tokens
Crear token con permisos para las funciones mencionadas.

2. Configurar el formulario
Ejecutar el workflow en n8n

Acceder al formulario generado

Completar los campos:

Actividad: URL completa de la tarea en Moodle

wstoken: Token obtenido en el paso 1

Calificaciones: Valores máximo y mínimo

Comentarios: Retroalimentación para cada caso

3. Ejecutar la automatización
El sistema extraerá automáticamente el cmid de la URL

Consultará todas las entregas

Asignará calificaciones según el estado

Generará reporte de ejecución

⚙️ Escalas soportadas
Escala Numérica (Ejemplo)
text
Calificación Máxima: 100
Calificación Mínima: 0
Entregado: 100 puntos + comentario máximo

No entregado: 0 puntos + comentario mínimo

Escala Sí/No (Ejemplo)
text
Calificación Máxima: 1
Calificación Mínima: 0
Entregado: 2 (Yes) + comentario máximo

No entregado: 1 (No) + comentario mínimo

🔍 Validaciones incluidas
Extracción robusta del cmid de URLs

Validación de estado de entrega (submitted)

Manejo de errores en llamadas a Web Services

Reporte claro de éxito/fracaso

Estructura de datos consistente

📊 Resultados esperados
Caso exitoso:
text
✅ Proceso ejecutado correctamente
23
Se calificaron 23 tareas
Caso sin entregas:
text
❌ Error al ejecutar el proceso
0
No se pudo calificar ninguna tarea
🚨 Consideraciones importantes
Pruebas en entorno de desarrollo antes de producción

Verificar permisos del token en Moodle

Backup de calificaciones antes de ejecuciones masivas

Validar formato de URL de la actividad

Revisar límites de API de Moodle

🔄 Posibles mejoras futuras
Integración con Google Sheets para listas de estudiantes

Calificaciones parciales basadas en rúbricas

Notificaciones por correo a estudiantes

Panel de control con estadísticas

Soporte para calificaciones decimales

📄 Licencia
Este proyecto está disponible bajo la licencia MIT.

🤝 Contribuciones
¡Contribuciones son bienvenidas! Por favor:

Haz fork del proyecto

Crea una rama para tu funcionalidad

Realiza commits descriptivos

Abre un Pull Request detallado

📞 Soporte
Para problemas o consultas:

Revisar la documentación de Moodle Web Services

Verificar logs de n8n para errores específicos

Consultar issues en el repositorio

⚠️ Nota: Este tool está diseñado para asistir en procesos de evaluación, pero la supervisión docente sigue siendo esencial para garantizar la calidad educativa.
