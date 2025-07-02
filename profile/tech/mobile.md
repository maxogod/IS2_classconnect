# Mobile Frontend

[[<] Go back home](../README.md)

## Stack

| Layer            | Technology                                      |
|------------------|-------------------------------------------------|
| Language         | [TypeScript](https://www.typescriptlang.org/)  |
| Framework        | [React Native](https://reactnative.dev/)       |
| Runtime & Tooling| [Expo (Development Build mode)](https://expo.dev/)                      |

## Arquitectura del Frontend

Se puede dividir la aplicación en dos partes navegables, en relación al estado de authentificación de la cuenta actual. Por un lado la parte pública, cuando aún el usuario no ha pasado la parte de ingreso de credencial en el registro de la aplicación. Por la otra parte la parte privada de la aplicación donde puede utilizar todas las funcionalidades de la aplicación en sí, una vez que sus credenciales fueron verificadas y el sistema de autentificación al abrir la aplicación si aún continua la sesión mediante el uso de tokens verificadas en el backend JWT, en el caso de un usuario cerrar la aplicación y volver a abrir si aún el token no perdió su validez, será redirigido a la página principal de la aplicación.
Durante la navegación en la parte privada será constantemente chequeadas las credenciales para no tener problemas con las funcionalidades que brindan los microservicios.

Para ver detalladamente las vistas, puede acceder al manual de usuario de la aplicación móvil:

[Manual de Usuario de aplicación](https://github.com/ClassConnect-org/.github/blob/main/profile/man/mobile.md)

En la aplicación se llevaron a cabo múltiples vistas, y la mayoría de los parámetros que se compartían entre vistas se enviaban entre una y otra a partir de parametros de navegación a traves de funciones presentes en 'router'. Muchas vistas presentaban múltiples estados de componentes, debido a que dependiendo del rol o nivel de autoridad, en el caso que pueden acceder a una misma vista un estudiante, un profesor o el dueño del curso, las funcionalidades, detalles y componentes varían según el usuario en la vista que navegaba. Para eso se implementaron estados useState o constantes obtenidas a partir de parámetros de navegación, y se implementó la lógica de mostrar los componentes en las vistas según variables o la autentificación presente en el JWT almacenado y verificado constantemente en el Secure Storage de la aplicación.

Además hay vistas incluidas en las direcciones de navegación que fue requerido realizar un modelo de vistas dinámicas, donde dependiendo de parámetros obtenidos de la API o procesadas en la aplicación deberían redirigir automáticamente con los parámetros necesarios para llevar a la vista correspondiente. En lo que fue posible, dado que se necesitó priorizar llegar con las features funcionando en el tiempo asignado, se crearon componentes reutilizables dentro de una carpeta de componentes divididas segun las vistas o temas de vistas, y de igual manera con estilos, servicios, types, hooks.

El código de la arquitectura y los pasos para la generación del APK de la apliación, se encuentran en el repositorio de la organización:
[Mobile App](https://github.com/ClassConnect-org/mobile-app/blob/main/README.md)

## Librerias Utilizadas

- [NativeWind](https://www.nativewind.dev/): framework css para simplificar el diseño.
- [Axios](https://axios-http.com/): cliente HTTP para comunicación con microservicios del backend.
- [google-signin](https://cloud.google.com): API de google para utilizar su sistema OAuth para identificación federada de la aplicación.
- [react-native-onesignal](https://onesignal.com/): API de One Signal para el manejo de notificaciones y eventos Popup en la aplicación.
- [react-native-view-shot / react-native-html-to-pdf / react-native-share / react-native-webview]: para la creación, formato y envío de screenshots de la aplicación en modo pdf.
- [react-native-modal-datetime-picker](https://www.npmjs.com/package/react-native-modal-datetime-picker): librería para seleccionar y almacenar fecha y hora en la aplicación
- [react-native-document-picker](https://www.npmjs.com/package/react-native-android-document-picker): librería para seleccionar en archivos locales y cargar en la aplicación muchos tipos de documentos.
- [react-native-paper](https://www.npmjs.com/package/react-native-paper): librería con muchos componentes útiles y modificables.

## Comunicacion con otros microservicios

- Users: autentificacion, recuperos, busquedas y visualizacion de perfiles.
- Courses: manejo de cursos, tareas, examenes, modulos, estadisticas, correcciones, etc.
- Forum: creacion de preguntas, votos, respuestas y etiquetas.
- AI: chateo, consultas y criticas constructivas.
- Notifications: obtencion de notificaciones push e historial de las mismas.
