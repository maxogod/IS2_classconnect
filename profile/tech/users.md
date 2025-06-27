# Microservicio de usuarios

[[<] Go back home](../README.md)

## Stack

| Layer         | Technology  |
|---------------|-------------|
| Language      | Go          |
| Web Framework | Gin-Gonic   |
| DB Driver     | Gorm        |

## Responsabilidades

Las responsabilidades de este microservicio son las siguientes:

- Registro de usuarios e Inicio de sesion por medio de email y contraseña.
- Ingreso con identidad federada (Google Oauth).
- Recupero de contraseñas y activaciones de cuentas para identidades no federadas (utiliza micro-servicio de notificaciones para emails).
- Garantizar unicidad de cuentas, realizando un *merge* cuando el usuario lo pide.
- Manejo de perfiles y actualizaciones.
- Busquedas entre los usuarios de la plataforma.
- Administracion de usuarios (bloqueos y eliminaciones) garantizando que sea un administrador (utilizando un admin-token, generado por el micro-servicio de administration).

## Stateless sessions

Se utilizan sesiones stateless (con JWT tokens), de manera tal que cuando un usuario se comunica con el servicio y no tiene el token `Authorization`
las unicas acciones que pueden hacer son crear o entrar a su cuenta, luego de lo que se le genera un token valido por un dia.

Una vez que el usuario tiene el token con su sesion, este podra comunicarse con los demas micro-servicios sin ser rechazado por no tener un token valido. Este tipo de sesiones permiten una mayor flexibilidad para ser usadas en entornos distribuidos donde los micro-servicios no comparten una base de datos, ni tampoco hacen cross-calls duplicadas (e.g. GET de la session cada vez que un usuario se conecta).

## Base de datos

Este microservicio, como se menciono en el documento de arquitectura, utiliza una base de datos PostgreSQL hosteada en Supabase. Las tablas presentes en la misma se pueden ver a partir de las migraciones creadas en el [repositorio del servicio](https://github.com/ClassConnect-org/users-microservice).

A su vez se utiliza un *bucket* (tambien hosteado en supabase) llamado 'profiles', que se utiliza para almacenar las fotos de perfil de los usuarios registrados en la plataforma.

## Comunicacion con otros microservicios

- Notifications: utiliza el servicio de notificaciones para el envio de codigos para la verificacion y para mensajes de bienvenida.
