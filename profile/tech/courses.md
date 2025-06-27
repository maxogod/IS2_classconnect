# Microservicio de courses

[[<] Go back home](../README.md)

## Responsabilidades

Las responsabilidades de este microservicio son las siguientes:

- Manejo de cursos (vistas, creaciones, ediciones).
- Manejo de tareas, examenes, entregas y correcciones.
- Creacion, organizacion y recuperacion de modulos de contenido.
- Administracion de profesores auxiliares por parte del profesor principal y visualizacion de actividades.
- Obtencion de estadisticas del curso como profesor.
- Obtencion de estadisticas de los alumnos.

## Base de datos

Este microservicio, como se menciono en el documento de arquitectura, utiliza una base de datos PostgreSQL hosteada en Supabase. Las tablas presentes en la misma se pueden ver a partir de las migraciones creadas en el [repositorio del servicio](https://github.com/ClassConnect-org/courses-microservice).

A su vez se utilizan tres *buckets* (tambien hosteados en supabase) llamados 'courses-pictures', 'courses-modules', 'courses-assignment-resource', que se utilizan para almacenar imagenes de cursos, recursos para modulos (imagenes, documentos, tablas, etc) y recursos para tareas o trabajos practicos.
