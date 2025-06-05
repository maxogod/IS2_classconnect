[**Volver**](../README.md)

# Actualmente en Desarrollo - *Deadline: 5 de Junio*

## Checkpoint 3

Para este checkpoint se tuvo como objetivo tener una version utilizable de la aplicacion, teniendo en cuenta el nucleo de la misma, es decir la posibilidad de unirse a cursos, y que el profesor sea capaz de dar material a los alumnos en el formato de modulos organizables, asi como tambien, pedir tareas y examenes, para que los estudiantes completen, y luego este pueda corregir las entregas. Tambien se apunto a tener un espacio de comunicacion entre alumnos y profesores, con temas y la posibilidad de hacer preguntas y respuestas. Finalmente comenzar a investigar e implementar una prueba de concepto respecto a el microservicio de AI, con el objetivo de confeccionar un chat contextuado especificamente sobre la plataforma (uso, preguntas frecuentes, etc).

### Cambios respecto al anterior checkpoint

1. Se realizo una migracion de todos los microservicios del cluster de kubernetes anterior, a uno nuevo alojado en la misma plataforma, por temas de limites de tiempo de la version gratuita que ofrece **linode**.
2. No se realizo ningun cambio a nivel arquitectura del proyecto.

### Backlog comprometido

El backlog comprometido se puede visualizar [aqui](https://github.com/orgs/ClassConnect-org/projects/1/views/2), este consiste en los siguientes items:

**Usuarios:**
- Activación de Cuenta  ✔️
- Recupero de Contraseña ❌

**Cursos:**
- Creación de Módulos ✔️
- Agregar Recursos a un Módulo✔️
- Edición de Modulos ✔️
- Manejo de Errores en la Creación de Modulos ✔️
- Efectivizar el Criterio de Elegibilidad para Enrolamiento❌

**Mobile-app:**
- Diseño de la edicion y borrado de curso ✔️
- Agregar sistema basico de notificación a todos los servicios  ✔️
- Crear vista de lista de las tareas/examenes para estudiantes y profesores ✔️
- Agregar vista para el recupero de contraseña ✔️
- Agregar vista para la Activacion de Cuenta ✔️
- Agregar sistema de notifiacion Push ✔️
- Recibir y Enviar información del Foro  ✔️
- Mejorar diseño de la vista del foro ✔️
- Crear vista para la creacion y edicion de modulos para los profesores ❌
- Agregar manejo de filtros para la vista de cursos ❌

**Foro:**
- Creación de Preguntas ✔️
- Permitir respuestas a preguntas existentes  ✔️
- Edición y Eliminacion de preguntas y respuestas
- Paginación a la vista del foro  ✔️
- Votación y seleccion de pregunta correcta ✔️
- Filtrado y Busqueda de Contenido ✔️
- Notificaciones de Actividad ❌

**Notificaciones:**
- Envio de Notificaciones Push ✔️

**Admin:**
- Registro de auditoria ✔️ 
- Manejo de Usuarios ❌

**Chat de Asistencia IA:**
- En progreso (chat funcionando pero con contexto pre-definido no dinamico) 🟡

**Backoffice Front:**
- Implementacion general ❌

### Features pendientes para finalizacion de MVP

- Finalizacion de historias pendientes y manejo de casos borde
- Estadisticas de rendimiento estudiantil a nivel curso [OBLIG]
- Gestion de usuarios por parte de un administrador [OBLIG]
- Backoffice frontend integrando administacion [OBLIG]
- Profesores auxiliares [OPT]
- Recupero de contraseña [OPT]
