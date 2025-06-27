# Backoffice Frontend

[[<] Go back home](../README.md)

## Stack

| Layer         | Technology                         |
|---------------|-------------------------------------|
| Language      | [TypeScript](https://www.typescriptlang.org/) |
| Framework     | [React](https://reactjs.org/)      |
| Build Tool    | [Vite](https://vitejs.dev/) |
| Web server    | [Nginx](https://nginx.org/) |

## Arquitectura del Frontend

El Backoffice esta compuesto de dos paginas: el home de inicio de sesión y y el dashboard con todas las funcionalidades para el administrador.
El dashboard presenta un header con la info del usuario y la posibilidad de cerrar sesión y un menu lateral con todas las funcionalidades para el administrador.
Las secciones disponibles son:
- Rules: Administración de reglas del sistema.
- Users: Gestión de usuarios (búsqueda, bloqueo, eliminación).
- Logs: Visualización de logs de auditoría y de notificaciones.
- AI Chat: Herramienta para gestionar feedback de preguntas/respuestas generadas por IA.
- Admins: Visualización y control de otros administradores.

## Librerias utilizadas
 - [Tailwind](https://tailwindcss.com/): framework css para simplificar el diseño.
 - [Lucide React](https://lucide.dev/guide/packages/lucide-react): Libreria de íconos.
 - [Axios](https://axios-http.com/): cliente HTTP para comunicación con microservicios del backend.

## Comunicacion con otros microservicios

- Notifications: obtención de logs.
- Administration: autenticacion de administrador, reglas y registro de auditoria.
- Users: administracion de usuarios como visualizacion y busqueda, bloqueos y eliminaciones.
- Ai: obtencion de upvotes y downvotes, y seleccion para refinamiento.
