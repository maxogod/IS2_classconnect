# Microservicio de Foro

[[<] Go back home](../README.md)

Este microservicio fue desarrollado para proporcionar una funcionalidad de foro simple para los cursos dentro de la aplicación ClassConnect. El servicio está implementado en Go utilizando el framework Gin.

## Estructura

Se utiliza la arquitectura package by layer, donde los controladores se pueden encontrar en la carpeta handlers, los servicios en services y el repositorio en repository.

## Base de Datos

Se decidió utilizar MongoDB como sistema de almacenamiento para el microservicio de foro, por su orientación a documentos, que encaja con la información jerárquica y anidada que maneja esta funcionalidad.

Se creó 1 colección llamada forum para el servicio. esta registra todas las preguntas del sistema y contiene los siguientes campos:

 - ID de la pregunta
 - Título
 - Descripción
 - Tags
 - ID del autor de la pregunta
 - ID del curso
 - Tiempo de Creación
 - Cantidad total de votos
 - Lista de votos positivos
 - Lista de votos negativos
 - ID Respuesta correcta
 - Lista de Respuestas

Cada Respuesta cuenta con los siguientes datos:

 - ID de la respuesta
 - Comentario
 - ID del autor de la respuesta
 - Tiempo de Creación
 - Cantidad total de votos
 - Lista de votos positivos
 - Lista de votos negativos
