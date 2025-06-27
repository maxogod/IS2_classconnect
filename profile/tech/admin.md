# Microservicio de Administración

Este microservicio está encargado de gestionar las funcionalidades administrativas del sistema ClassConnect, incluyendo el manejo de reglas, auditoría de cambios, administración de cuentas y control de sesiones de los administradores.

## Stack

| Layer         | Technology  |
|---------------|-------------|
| Language      | [Python](https://www.python.org/)          |
| Web Framework | [Fastapi](https://fastapi.tiangolo.com/)   |
| DB Driver     | [Pymongo](https://pypi.org/project/pymongo/)         |

## Estructura

Se colocan los controladores en la carpeta controllers y los servicios en services con manejo de la base de datos.

## Base de Datos

Se decidió utilizar MongoDB como sistema de almacenamiento para el microservicio de foro, por su orientación a documentos, que encaja con la información flexible de las reglas y normativas.

Se crearon 4 colecciones para el servicio:
 
 - Admins: Contiene las cuentas creadas por otros administradores con su correo y contraseña.
 - Session: Contiene las sessions_id del sistema, con fecha de expiración para limitar el uso del administrador.
 - Rule: Contiene las reglas de la Aplicacion.
 - Logs: Registra los cambios de auditoría.

## Manejo de Administradores
El sistema permite a los administradores con permisos crear nuevas cuentas de administrador, garantizando que el acceso al backoffice esté controlado de forma estricta.

 - La única forma de convertirse en administrador es siendo registrado por otro administrador.
 - Las credenciales incluyen un email único y una contraseña segura, la cual es almacenada de forma cifrada.
 - Las sesiones de administrador están sujetas a un tiempo de expiración definido para limitar el acceso prolongado.
 - Al iniciar sesión, se proporciona un JWT Token unico de administradores para poder realizar peticiones en otros servicios unicos de administradores

## Reglas y Normativas
El microservicio permite a los administradores con session activa las operaciones de creación, edición y eliminación de reglas que rigen el uso de la aplicación ClassConnect.

Cada regla incluye:
 - Título
 - Descripción
 - Condiciones (opcional)
 - Fecha de entrada en vigencia (Debe ser una fecha a futuro)

La ejecución de cualquier cambio en las reglas de la aplicación genera una notificación a traves de email hacia todos los usuarios de la aplicación.

## Logs de Auditoría 

Toda modificación sobre las reglas de la aplicación es registrada automáticamente en la colección Logs.

Cada entrada de log contiene:
 - Email del administrador que ejecutó la acción.
 - Fecha y hora exacta del cambio.
 - Tipo de acción: `create`, `update` y `delete`.
 - Detalles de la modificacion en la regla
 - ID de la regla afectada

[[<] Go back home](../README.md)
