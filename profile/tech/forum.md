# Microservicio de Foro

[[<] Go back home](../README.md)

Este microservicio fue desarrollado para proporcionar una funcionalidad de foro simple para los cursos dentro de la aplicación ClassConnect. El servicio está implementado en Go utilizando el framework Gin.

| Layer         | Technology  |
|---------------|-------------|
| Language      | [Go](https://go.dev/)          |
| Web Framework | [Gin-Gonic](https://github.com/gin-gonic/gin)   |
| DB Driver     | [MongoGoDriver](https://github.com/mongodb/mongo-go-driver)         |

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

## Creación de preguntas
Los usuarios autenticados pueden crear nuevas preguntas para un curso determinado, especificando título, descripción y etiquetas. La pregunta queda registrada en la base de datos junto con la metadata del autor.## Respuestas a las preguntas.

## Votos a preguntas y respuestas

Cualquier usuario autenticado puede responder a una pregunta ya creada. La respuesta se agrega al array de respuestas de la pregunta correspondiente.

## Seleccionar respuesta como correcta
Los usuarios pueden votar tanto preguntas como respuestas:

 - Voto positivo y voto negativo

 - Un usuario no puede votar más de una vez en el mismo sentido.

 - Se pueden revertir votos.

## Notificar Eventos

Cada vez que ocurre una acción relevante (nueva respuesta a mi pregunta, selección de respuesta correcta, recepción de voto positivo), se genera una notificación de tipo Push utilizando el microservicio de notificaciones.

[[<] Go back home](../README.md)
