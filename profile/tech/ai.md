# Microservicio de Inteligencia Artificial

## Introducción 
Este microservicio fue diseñado con el fin de proveer un chat de asistencia para la plataforma. Se propuso que dicho chat sea capaz de procesar el lenguaje natural humano y que tenga la capacidad de brindar respuestas precisas y rápidas a preguntas puntuales. Además, dichas respuestas deberían poder ser calificadas por los usuarios de forma tal que el chat se vuelva más preciso mientras más usado sea.
Para lograr ese cometido, se decidió usar la API de Gemini.

## La API de Gemini
Se barajaron muchas posibilidades entre las que estaban incluídas APIs de otros LLMs (openAI o alguna open source) o incluso montar un pequeño LLM de forma local.
Por un tema de costos y simplicidad, se terminó eligiendo a Gemini debido a la gran cantidad de preguntas (1.500) que se le puede hacer por día con una suscripción gratuita.
Además, resultaba tentadora la perspectiva del Fine-Tuning para la mejora continua del chat, aunque resultó no ser tan útil como se había previsto.

## La Base de Datos
Se optó por usar Supabase debido a su practicidad y accesibilidad. Dicha base de datos cuenta con dos tablas: 
####  Chats 
Se usa para almacenar los chats y consta de las siguientes columnas:
- ID (del chat)
- Votes (calificación por el usuario)
- feedback del usuario (en caso de tenerlo)
- user_id del usuario que hizo la pregunta

####  Documentos
Se usa para que Gemini pueda comparar semanticamente una pregunta con una que ya le hayan hecho y tenga una respuesta de ejemplo. Consta de las siguientes columnas:
- id del chat
- Title (El prompt que se le pasa a Gemini pasado en limpio. Incluye la pregunta original y la metadata)
- Content (La respuesta modelo al Title)
- Embeddings (Un vector de 768 dimensiones utilizado para comparaciones semánticas)



## El flujo de un chat
Supongamos que un usuario hace una pregunta al chat desde la aplicación móvil. Entonces se hará uso del endpoint **POST** **/chat**, que le enviará al servicio un json en el cual se encuentra incluída la pregunta y un header en el cual se encuentra un JWT con el id del usuario que hizo la pregunta. El servicio procesará la pregunta agregandole un **contexto** en el cual se le explica a gemini su rol de bot junto a detalles estáticos de la aplicación. El id del usuario será usado para consultarle a las APIs de los servicios de Usuarios y Cursos por la **metadata** del usuario. Dicha información incluye información del usuario, junto a cursos a los que esta inscripto y tareas y evaluaciones de dichos cursos con el fin de brindar una respuesta útil.
Finalmente se agrega un pasaje relevante basado en una pregunta que ya le hayan hecho. Esto se aborda en más detalles en el apartado de mejora continua.
Así es como se termina de construir el prompt que será enviado a Gemini mediante su API. 
Una vez que se recibe la respuesta de Gemini, se almacena en la base de datos con un nuevo id y se le envía un Json al usuario con la respuesta y su id.

## Calificación de chats
Una vez que un usuario recibe una respuesta a su pregunta, recibe también la posibilidad de calificarla como buena o mala.

####  Cuando se califica como positivo
Entonces se usa el endpoint **POST** **/upvote/:chat_id**, que le comunicará al servicio que dicho chat fue calificado positivamente. Entonces se actualiza la fila correspondiente y se cambia el campo Votes de 0 a 1.

####  Cuando se califica como negativo
Entonces el sistema ofrece la posibilidad de enviar un feedback explicando por que la respuesta no fue buena. Luego se usa el endpoint **POST** **/downvote/:chat_id**, que le comunicará al servicio que dicho chat fue calificado negativamente y se le incluye el feedback propocionado por el usuario, si es que existe. Entonces se actualiza la fila correspondiente y se cambia el campo Votes de 0 a -1 y el campo Feedback si es que existe.











[[<] Go back home](../README.md)
