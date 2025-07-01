# Manual de usuario [Mobile-App]🚧

[[<] Go back home](../README.md)

A continuacion se detalla un manual de uso para la aplicacion mobile para cada parte de la misma.

## Índice

### Inicio:
- [Inicio de sesión & registro](#inicio-de-sesión--registro)
- [Homepage (Mis cursos)](#homepage-mis-cursos)
- [Perfil y opciones](#perfil-y-opciones)
- [Navi (AI Chatbot)](#navi-ai-chatbot)

### Como estudiante:
- [Buscar cursos](#buscar-cursos)
- [Unirse y salir de un curso](#unirse-y-salir-de-un-curso)
- [Ver to-do](#ver-to-do)
- [Completar tareas y exámenes](#completar-tareas-y-exámenes)

### Como profesor:
- [Crear curso](#crear-curso)
- [Crear y organizar módulos](#crear-y-organizar-módulos)
- [Crear y corregir tareas](#crear-y-corregir-tareas)
- [Crear y corregir exámenes](#crear-y-corregir-exámenes)
- [Ver estadísticas del curso](#ver-estadísticas-del-curso)
- [Ver estadísticas de estudiante](#ver-estadísticas-de-estudiante)
- [Ver log de profesores auxiliares](#ver-log-de-profesores-auxiliares)
- [Terminar curso y graduaciones](#terminar-curso-y-graduaciones)

### Misceláneo:
- [Preguntas y respuestas en foro](#preguntas-y-respuestas-en-foro)
- [Notificaciones](#notificaciones)

## Inicio de sesión & registro

Al iniciar la apliación, el usuario se encontrará con la pantalla de inicio de sesión. En dicha vista, tendrá la posibilidad de:

- Registrarse:
    En el caso de no tener cuenta, el usuario puede registrarse completando los campos requeridos. Para activar la cuenta debe ingresar un token enviado a su mail.
- Iniciar sesión:
    El usuario podrá iniciar sesión al ingresar su mail y contraseña. Se provee un botón para poder resetear esta última en el caso de que la contraseña haya sido olvidada.
- Iniciar sesión usando credenciales de Google:
    Se provee la opción de iniciar una sesión usando credenciales de google. Si el mail de dicha cuenta ya está en uso, se ofrece la posibilidad de unir ambas cuentas.

## Homepage (Mis cursos)
Homepage es la vista principal de la aplicación.Arriba a la izquierda se puede encontrar un menú tipo Hamburguesa con los siguientes campos: 
- Home (lleva al Homepage)
- To-Do (lleva a la vista to-do)
- Search Courses (lleva a Buscar Cursos)
- Profile (lleva a Perfil y Opciones)

El usuario verá un listado con los cursos en los cuales está inscripto o es profesor. Al seleccionar uno de dichos cursos podrá ver la información detallada de este.

## Perfil y opciones
El usuario podrá ver su foto de perfil y tendrá la opción de cambiarla.   
También podrá ver los detalles de su cuenta y tendrá la opción de editarlos.   
El usuario podrá activar y desactivar las notificaciones Push y de Email.   
El usuario tendrá la opción de hacer que su cuenta sea privada o pública.   
El usuario podrá terminar su sesión.


## Navi (AI Chatbot)

Al tocar el ícono del chat, el usuario verá una ventana en la que podrá escribir una pregunta puntual sobre la plataforma. Dicha pregunta será contestada por un Bot con la capacidad de procesar lenguaje natural. Una vez que haya recibido una respuesta, el usuario tendrá la chance de calificar dicha respuesta como buena o mala. En caso de calificarla negativamente, tendrá la opción de dar feedback explicando por que decidió calificarla de dicha manera.    
Para cerrar dicha ventana basta con tocar la cruz arriba a la derecha.

## Buscar cursos
El usuario verá un listado de todos los cursos disponibles en la plataforma. Estarán marcados aquellos cuyo criterio de aceptación no esté cumplido.    
Se le ofrecerá al usuario la posibilidad de filtrar dichos resultados por nombre y ordenarlos por un parámetro a elección.   
Al seleccionar un curso podrá ver la información detallada de este junto a la lista de inscriptos y profesores. En caso de poder unirse, verá un botón que le permita realizar dicha acción.     

## Unirse y salir de un curso

Al decidir unirse a un Curso, un mensaje popup aparecerá informandole al usuario del exito o fracaso de la acción. Se recibirá una notificación de exito en caso de que la acción sea completada exitosamente.    
En caso de querer salir de un curso, el usuario debe seleccionarlo para ver los detalles, buscarse a si mismo en la lista de estudiantes inscritos, seleccionarse y tocar la opción para expulsar estudiante.     Una notificación popup informará sobre el estado de la acción y llegara una alerta en caso de haber salido correctamnete.     

## Ver to-do
En esta vista, el usuario podrá ver las tareas y examenes que pertenecen a los cursos en los que está inscripto. Tiene la opción de filtar por tareas y examenes y por completadas, pendientes, entregadas y completadas.

## Completar tareas y exámenes
Al seleccionar una tarea o examen, el usuario tendrá la posibilidad de ingresar texto en los tags correspondientes. También tendrá la opción de subir archivos cuando corresponda.    
Una notifiación popup informará sobre el estado de dicha acción.

## Crear curso
En esta vista, el usuario tendrá la posibilidad de ingresar los campos necesarios para la creación de un curso (título, descripción, capacidad, nota de aprobación, foto del curso, etc...).   

Una vez creado, el nuevo curso estará disponible para que los demás usuarios puedan inscribirse.

## Crear y organizar módulos
En la vista de un curso en el que el usuario es profesor, podrá tocar el botón "Add Material" que le permitirá crear un módulo nuevo ingresando el título y el contenido de dicho módulo de forma obligatoria y Attachments de forma opcional.      
Para organizar los módulos, puede tocar el botón "Arrange modules Order" para cambiar el orden de los módulos desde la visa de Módulos.    

## Crear y corregir tareas

En la vista de un curso en el que el usuario es profesor titular o auxiliar, podrá tocar el botón "Add Material" que le permitirá crear una tarea nueva ingresando el título, las instrucciones, puede agregar hasta 6 archivos de cualquier tipo y anexarlos a la tarea (máximo 10 mB por archivo) y la deadline.
Una vez creada una tarea, como alumno, se puede acceder a ella a través de la vista del curso seleccionado buscando en la lista de tareas o también en la vista de to-do list (en esta vista puede filtrar por estado de la tarea), y luego una vez haya accedido, deberá completar una breve descripción y puede añadir un archivo anexo de hasta 10 meB, de esta forma podrá entregarlo. Una vez completada la tarea, el estado de esta pasará a estado entregado, el cual está disponible para que el alumno pueda editarlo, hasta que el profesor lo evalúe. Una vez que fue evaluada, no podrá editarla, pero podrá acceder a ver tanto el contenido original como el suyo, y la nota final sobre la tarea.
Como profesor, se debe acceder al curso seleccionado, buscar en la lista de tareas, y presionar en la tarea deseada a corregir, luego presionar en ver entregas, y luego se accede a otra lista donde se encuentran todos los estados de los estudiantes (con sus nombre) de la tarea seleccionada, y luego podrá corregir la tarea, pudiendo acceder en caso que lo haya a la descarga del archivo adjunto cargado por el alumno en la tarea respondida, y por último él podrá evaluarla con una nota y un comentario, y puede decidir de enviarlo a reentregar la tarea si asi lo deseara.

## Crear y corregir exámenes
En la vista de un curso en el que el usuario es profesor titular o auxiliar, podrá tocar el botón "Add Material" que le permitirá crear un examen nuevo ingresando el título, las instrucciones, además debe desplegar una vista de creación de una evaluación personalizable con distintos tipos de preguntas y sus respectivos puntajes, el tiempo máximo de resolución de examen, el puntaje mínimo para aprobar y la fecha límite para la entrega.
Una vez creado el examen, como alumno, se puede acceder a ella a través de la vista del curso seleccionado buscando en la lista de exámenes o también en la vista de to-do list (en esta vista puede filtrar por estado del examen), y luego una vez haya accedido, deberá completar las preguntas y podrá entregarlo. Una vez completado el examen, el estado de esta pasará a estado entregado, y alumno ya no podrá editarlo. Una vez que fue evaluado, no podrá editarlo, pero podrá acceder a ver tanto el contenido original como el suyo, y la nota final del examen.
Como profesor, se debe acceder al curso seleccionado, buscar en la lista de exámenes, y presionar en el examen deseado a corregir, luego presionar en ver entregas, y luego se accede a otra lista donde se encuentran todos los estados de los estudiantes (con sus nombre) del examen seleccionado, y luego podrá corregirlo, puntuando individualmente cada pregunta, y por último una devolución escrita sobre el examen, y ya puede entregarlo ya que la nota final se coloca automáticamente de las notas parciales de las preguntas. El profesor puede volver a editar todos esos campos en caso de equivocación o reconsideración de alguna pregunta y volver a calificar el examen ya corregido si lo desea.

## Ver estadísticas del curso
Desde la vista del curso seleccionado, se puede acceder a las estadísticas generales del curso, presionando en el botón con ícono de estadísticas en el borde superior derecho. Aquí el profesor puede visualizar el rendimiento de los alumnos con respecto a los exámenes y tareas resueltas, luego las métricas más relevants del curso, como el desempeño promedio de los estudiantes, el promedio de la notas de los graduados finales y la cantidad de contenidos del curso.

## Ver estadísticas de estudiante
Se puede acceder a la pantalla de estadísticas de usuarios desde la lista de estudiantes en la vista de detalles del curso, presionando sobre el menú de cada alumno, desplegando la opción de ver estadisticas. Dentro de esta vista, se podran ver las notas promedios de las tareas y examenes entregados por el alumno, junto a la nota final de cuando se le gradúe con nota de cursada. También se puede ver el porcentaje de tareas y examenes completados por el alumno.
Esta herramienta también está presente al momento de graduar a los alumnos cuando se cuando se finaliza un curso.

## Ver log de profesores auxiliares
Dentro del curso seleccionado se encuentra un botón con un logo de scroll en el cual puede acceder y ver el registro de eventos, relacionado con las acciones que hicieron todos los profesores auxiliares en el curso. Se archivan todas las acciones sea de edición de módulos,  reordenamiento de ellos, creación, edición y corrección de tareas o exámenes, etc. de manera que el profesor titular pueda tener un seguimiento de las acciones que se realizan en el curso.

## Terminar curso y graduaciones
Desde la vista de un curso en el cual el usuario es profesor, se puede tocar el botón de detalles del curso. Ahí se podrá ver un botón de options arriba a la derecha, al tocarlo se tendrá la opción de Completas y borrar el curso.
Cuando un profesor decide utilizar la opción de completar curso, allí se le especificará que el curso pasará a ser inactivo y deberá graduar a los estudiantes. Cuando un curso está inactivo los estudiantes no pueden realizar ninguna acción sobre tareas o examenes pero aún pueden ver los recursos presentes en el curso y los materiales de estudio. 
En cambio los profesores pueden seguir corrigiendo tareas y exámenes, o haciendo revisiónes, y decidiendo que hacer antes de terminar la graduación completa de los estudiantes. Luego en este punto el profesor puede optar por volver a activar la clase, por si decide que algún alumno deba completar alguna tarea pendiente y en el caso de elegir la otra opción, que es completar el curso, en este caso se le avisa que esta acción es irreversible ya que el curso se archivará y ni tanto el profesor como el alumno podrá realizar ninguna acción sobre las tareas o exámenes, ni modificaciones sobre el curso una vez se complete el curso. En este último caso, el curso quedará archivado y el profesor si lo decide puede eliminarlo del sistema de lo contrario los alumnos y profesores pueden volver a entrar y ver estadísticas, archivos subidos, o tareas y exámenes que se han tomado.

## Preguntas y respuestas en foro
Desde la vista de un curso, el usuario podrá acceder al foro de dicho curso tocando el botón rojo que dice "Course Forum".   
Tendrá la opción de hacer una nueva pregunta tocando el botón de "New Question" que le pedirá que le ponga un titulo y detalles a la pregunta.   
El usuario también tiene la posibilidad de ver preguntas hechas anteriormente por otros usarios. Puede responder a dichas preguntas, ver otras respuestas y también calificarlas.    


## Notificaciones

Se puede acceder a la vista de las notificaciones tocando la campana que está arriba a la derecha en el Homepage. Ahí aparecerán las notificaciones recibidas por el usuario, que puede marcarlas como leídas para limpiar la vista.

