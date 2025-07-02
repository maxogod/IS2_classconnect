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


## Librerias Utilizadas

- [Tailwind](https://tailwindcss.com/): framework css para simplificar el diseño.
- [Axios](https://axios-http.com/): cliente HTTP para comunicación con microservicios del backend.

## Comunicacion con otros microservicios

- Users: autentificacion, recuperos, busquedas y visualizacion de perfiles.
- Courses: manejo de cursos, tareas, examenes, modulos, estadisticas, correcciones, etc.
- Forum: creacion de preguntas, votos, respuestas y etiquetas.
- AI: chateo, consultas y criticas constructivas.
- Notifications: obtencion de notificaciones push e historial de las mismas.
