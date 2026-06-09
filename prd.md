Adjunto el contenido del archivo PRD_CuadernoProfesor_MVP.md listo para copiar y guardar:

# PRD — Cuaderno del Profesor (MVP)

## 1. Título
Cuaderno del Profesor — MVP

## 2. Objetivo
Proveer una aplicación que simplifique la gestión docente (clases, asistencia, calificaciones, comunicaciones) y ofrezca asistencia asistida por IA para tareas rutinarias (sugerir calificaciones, generar feedback, planificación de clases), reduciendo tiempo administrativo y mejorando la retroalimentación al alumnado.

## 3. Alcance del MVP
Incluye:
- Gestión de cursos y grupos.
- Registro de asistencia por clase.
- Registro y cálculo de calificaciones (rúbricas básicas).
- Generación automática de feedback por alumno (plantillas IA).
- Panel de profesor con lista de tareas y notificaciones.
- Integración básica con CSV de importación/exportación y API REST.

Excluye (post‑MVP):
- Integraciones profundas con LMS (full sync).
- Analítica avanzada por alumno.
- Soporte multiidioma extensivo.
- Modelos de ML personalizados por alumno.

## 4. Usuarios y roles
- Profesor: gestiona cursos, registra asistencia, califica, solicita feedback IA.
- Administrador escolar: gestiona usuarios y cursos.
- Alumno (lectura): consulta calificaciones y feedback.
- Sistema/Agent IA: actor autónomo que sugiere calificaciones, genera feedback y ayuda a planificar.

## 5. Casos de uso principales (User Stories)
1. Como profesor quiero crear un curso para organizar clases y alumnos.  
   Criterio: crear curso, añadir alumnos, ver lista de cursos.

2. Como profesor quiero registrar asistencia por sesión para un grupo.  
   Criterio: marcar presente/ausente/tarde con timestamp; ver reporte por fecha/alumno.

3. Como profesor quiero agregar tareas/actividades y registrar calificaciones según rúbrica.  
   Criterio: crear tarea, definir rúbrica y ponderación, introducir nota por alumno.

4. Como profesor quiero generar feedback automático para un alumno basado en la tarea y rúbrica.  
   Criterio: botón "Generar feedback" que devuelve texto editable; profesor puede guardar/editar.

5. Como profesor quiero ver un panel con próximas tareas pendientes y alertas de entregas atrasadas.  
   Criterio: lista ordenada por prioridad/fecha con filtros.

6. Como administrador quiero importar/exportar listas de alumnos en CSV.  
   Criterio: importar CSV con mapeo de columnas y reporte de errores por fila.

7. Como alumno quiero consultar mis calificaciones y feedback.  
   Criterio: vista read‑only con historial por curso y tarea.

## 6. Requisitos funcionales (RF)
- RF1: CRUD de cursos, sesiones, alumnos, tareas.
- RF2: Registro de asistencia por sesión con timestamp y motivo.
- RF3: Rúbricas: crear criterios y pesos por tarea.
- RF4: Cálculo automático de nota final por alumno por curso según ponderaciones.
- RF5: Endpoint POST /generate-feedback que recibe { student_id, task_id, rubric, teacher_notes } y devuelve texto de feedback.
- RF6: Autenticación y autorización (RBAC para Profesor/Admin/Alumno).
- RF7: Import/Export CSV para alumnos y calificaciones (mapeo de columnas, validación).
- RF8: Panel de profesor con filtros, búsqueda y notificaciones.
- RF9: Auditoría: registrar cambios críticos (creación/edición de calificaciones, generación IA).

## 7. Requisitos no funcionales (NFR)
- NFR1 (Latencia IA): respuesta de generación de feedback < 3s objetivo / < 8s máximo.
- NFR2 (Disponibilidad): 99.5% para endpoints críticos.
- NFR3 (Escalabilidad): soportar ~200 concurrentes por instancia inicial.
- NFR4 (Seguridad): TLS en tránsito; cifrado en reposo para datos sensibles; RBAC.
- NFR5 (Privacidad): manejo mínimo de PII; políticas de retención y anonimización en datasets.
- NFR6 (Auditabilidad): logs inmutables de eventos críticos con trazas de usuario.

## 8. Criterios de aceptación (por feature)
- Curso CRUD: crear/editar/eliminar curso; asignar y listar alumnos correctamente.
- Asistencia: poder registrar asistencia y generar reporte por alumno/fecha.
- Calificaciones: ingresar notas por tarea, aplicar rúbrica y calcular promedio final exacto según fórmula definida.
- Generación de feedback IA: el texto generado debe ser relevante al rubric/nota; editable y salvable; tasa de rechazo humana < 20% en evaluación inicial.
- Import CSV: procesa archivo con ≥95% filas válidas o devuelve reporte con errores por fila.
- Seguridad: accesos no autorizados denegados; datos sensibles cifrados.

## 9. Métricas y KPIs
- Time saved per week per teacher (objetivo 2–4 horas).
- % de tareas donde se usó feedback IA.
- Latencia promedio de /generate-feedback.
- Tasa de aceptación del feedback generado (ediciones/aceptaciones).
- Incidentes críticos / mes (SLA breaches).

## 10. Dependencias
- Proveedor de LLM (API) o infra para modelo local.
- Almacenamiento para artefactos/datasets (S3 u equivalente).
- Sistema de autenticación (OAuth/JWT).
- Vector DB si se requiere RAG/contexto adicional.

## 11. Riesgos y mitigaciones
- Hallucinations en IA → Mitigación: prompt templates estrictos, validación por reglas, HITS (human review).
- Exposición de PII → Mitigación: anonimización, cifrado, políticas de retención.
- Rechazo por parte de docentes → Mitigación: interfaz editable, control completo del profesor sobre contenido final.
- Costos de inferencia altos → Mitigación: caching, límites de uso, modelos optimizados.

## 12. Backlog priorizado (MVP top items)
1. Autenticación y RBAC.  
2. CRUD cursos y gestión de alumnos.  
3. Sesiones y registro de asistencia.  
4. Tareas y definición de rúbricas.  
5. Calificaciones y cálculo automático.  
6. Panel de profesor (tareas y notificaciones).  
7. Endpoint IA /generate-feedback + UI botón.  
8. Import/Export CSV.  
9. Logging/audit trails.  
10. Pruebas automatizadas y despliegue básico.

## 13. Entregables y hitos (ejemplo de plan)
- Hito 1 (2 semanas): Infra básica, auth, CRUD cursos/alumnos.  
- Hito 2 (3 semanas): Sesiones/asistencia, tareas y rúbricas.  
- Hito 3 (3 semanas): Calificaciones, panel y CSV.  
- Hito 4 (2 semanas): IA feedback endpoint + integración UI.  
- Hito 5 (1 semana): QA, correcciones, despliegue MVP.

## 14. Supuestos
- Disponibilidad de ejemplos históricos de feedback para afinamiento y ejemplos few‑shot.
- Profesores estarán de acuerdo en revisar el contenido generado al menos durante la fase inicial.
- Proveedor de LLM con latencias y costes razonables disponibles.

## 15. Notas de implementación IA (resumen)
- Arquitectura IA inicial: LLM API + prompt templates; RAG opcional si se requiere contexto prolongado.  
- Versionar prompts y guardar metadata (prompt_version, input_hash, model_version).  
- Habilitar human‑in‑the‑loop para las primeras 2–4 semanas de uso.  
- Validación automática: reglas que detecten contradicciones, frases inseguras o exposición de PII antes de devolver a UI.

---
