# Microservicio de Inteligencia Artificial

## Introducción 
Este microservicio fue diseñado con el fin de proveer un chat de asistencia para la plataforma. Se propuso que dicho chat sea capaz de procesar el lenguaje natural humano y que tenga la capacidad de brindar respuestas precisas y rápidas a preguntas puntuales. Además, dichas respuestas deberían poder ser calificadas por los usuarios de forma tal que el chat se vuelva más preciso mientras más usado sea.
Para lograr ese cometido, se decidió usar la API de Gemini.


## Estructura

Se utiliza la arquitectura package by layer, donde los controladores se pueden encontrar en la carpeta api, los servicios en services y los repositorios en db.

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


## Mejora Continua

La técnica empleada para proporcionar mejora continua es Recuperación Aumentada de Generación (RAG), una técnica que mejora la precisión y relevancia de modelos de LLMs al combinarlos con sistemas de recuperación de información externos. Se guardan pares Pregunta-Respuesta que hayan sido considerados como buenos ejemplos por un administrador dentro de la tabla Documents en la base de datos.
Cuando llega una nueva pregunta por parte de un usuario, se utiliza el plugin de Supabase **pgvector** para que busque la pregunta almacenada en Documents que más se parezca a la que hizo el usuario. De esta forma, la carga computacional la tiene Supabase, no el servicio.
Finalmente se busca si la pregunta a la que más se parece la pregunta que hizo el usuario se parece lo suficiente como para ser considerada. Si en efecto se parece lo suficiente, se adjunta la respuesta asociada a la pregunta de Documents al prompt para que Gemini la tenga en cuenta. Sino, no.


## Flujo de Mejora Continua

Cuando un administrador decide hacer uso de la mejora continua, entonces primero se utilizará el Endpoint **GET** **/refine** que devolverá de forma paginada cada una de las filas de la tabla Chats que tenga un voto distinto de 0 (esto es, que hayan recibido alguna calificación). Dicha información es enviada a través de un Json que tiene los siguientes campos:
- id (del chat)
- Pregunta (la pregunta original del usuario junto a su metadata)
- Respuesta (la respuesta devuelta por Gemini)
- Feedback (en caso de que exista)

Por cada una de esas entradas, el administrador tiene 3 opciones:

- **Aceptarla:**
    Se envía un **POST** **/refine** junto con un body en el que se incluya la id del mensaje, la respuesta original y la pregunta original para que sean cargadas en Documents. Debe haber un header con un JWT perteneciente a un administrador.
- **Rechazarla:**
    Se envía un **DELETE** **/chat/:chat_id** para que no vuelva a aparecer
- **Editarla:**
    Cambia la respuesta de Gemini de acuerdo (o no, queda a criterio del administrador) al feedback proporcionado. Tener en cuenta que también se puede editar un chat que fue calificado positivamente.

#### Una vez que hay un chat para subir a Documents
Se utiliza **DataFrame** de **Pandas** acompañado por **Numpy** para representar la pregunta hecha originalmente como un vector de 768 dimensiones. Este vector es el que será usado en las busquedas semanticas.



## Conclusión

En conclusión, este microservicio integra de forma efectiva un LLM de alto rendimiento  con un almacenamiento semántico (Supabase y pgvector) para ofrecer respuestas contextuales y precisas. El sistema es mantenible, escalable y fácilmente extensible. En definitiva, este diseño garantiza equilibrio  entre rendimiento, coste y calidad de las respuestas.


[[<] Go back home](../README.md)
