# Microservicio de Notificaciones

[[<] Go back home](../README.md)

Este microservicio surge con el fin de proveer al resto de microservicios de la aplicación un punto en común donde enviar las notificaciones relevantes del sistema hacia los usuarios. Para esto mantiene un registro de los permisos que otorga el usuario desde la aplicación y envía notificaciones en masa filtrando los permisos establecidos. Se implemento en FastApi dado a su amplia disponibilidad de SDKs para los requerimientos del servicio.

## Stack

| Layer         | Technology  |
|---------------|-------------|
| Language      | [Python](https://www.python.org/)          |
| Web Framework | [Fastapi](https://fastapi.tiangolo.com/)   |
| DB Driver     | [Motor](https://github.com/mongodb/motor)         |

## Estructura

Se utiliza la arquitectura package by layer, donde los controladores se pueden encontrar en la carpeta api/endpoints, los servicios en services y los repositorios en repository.

## APIs Externas

La plataforma utiliza APIs externas para el envío de notificaciones a los usuarios, tanto por correo electrónico como mediante notificaciones push. Después de evaluar varias alternativas, se eligieron los siguientes servicios:

### Brevo – Notificaciones por Correo
[Brevo](https://www.brevo.com/es/) fue seleccionado como proveedor para el envío de correos electrónicos transaccionales. La decisión fue tomada tras enfrentar diversas limitaciones con otros servicios de correo, principalmente:

 - Muchos servicios de email transaccional requerían la verificación de un dominio propio, algo con lo que no contamos debido al carácter educativo del proyecto y la falta de presupuesto.

 - El uso del SMTP relay de Google se vio bloqueado por nuestro proveedor de infraestructura (Linode), debido a restricciones en el puerto SMTP (comúnmente el 465 o 587).

Brevo facilitó la integración dado que no era necesario contar con un dominio verificado para el envio de correos. Obviamente esto no viene sin su costo, las casillas de correo electronico al ver que nuestros correos no cuentan con DKIM, SPF o DMARC (autenticadores de origen de correo), marcan nuestros emails como actividad sospechosa o incluso terminadno en la casilla de spam. Otro factor positivo de Brevo fue su interfaz para crear templates de correos que permitio mantener un estilo consistente con información de la organización y una presentacion mas agradable al usuario.

### OneSignal – Notificaciones Push

[OneSignal](https://onesignal.com/) fue adoptado como solución para el envío de notificaciones push a dispositivos móviles. Inicialmente, se consideraron otras opciones como Firebase Cloud Messaging (FCM), pero se presentaron problemas de compatibilidad con Expo, el framework utilizado para el desarrollo de la app mobile.

Este servicio terminó siendo una grata sorpresa, tanto para el back como para el front, ya que permitia registrar desde el frontend al id del usuario como el token de notificación. Esto simplificó la complejidad de la comunicacion de la app hacia el servicio.


## Base de Datos

Se decidió el uso de MongoDB dado a su flexibilidad y capacidad de manejar volumenes altos de datos sin estructurar, muy conveniente para el registro de notificaciones y el historial para los usuarios.

Se crearon 3 colecciones para el servicio:

 - Permisos de Notificacion del Usuario: Registra e identifica a los usuarios archivando el id, correo, permisos de push y correo electrónico.

 - Historial de notificaciones: Registra todas las notificaciones push que fueron solicitadas.

 - Logs de Notificaciones: Registra todo intento de envío de notificación y el estado del mismo. 

## Manejo de Permisos de Usuarios

Para poder realizar los envíos de las notificaciones mediante el microservicio, se requirio el registro del UUID y correo electrónico de cada usuario. Para esto cada vez que un usuario se registra en la aplicación, la app envia los permisos del usuario para recibir notificaciones junto con el JWT Token del usuario, que contiene tanto el UUID como la dirección de email. Una vez almacenado el usuario, los demas servicios pueden solicitar el envío de notificaciones suministrando solamente el UUID del usuario, el sistema se encarga de revisar sus permisos y el envio mediante las apis externas. 

## Envío de Notificaciones

El servicio permite el envío de notificaciones por dos canales: correo electrónico y notificaciones push, a partir del UUID del usuario.

### Email

El endpoint de envío por correo puede recibir los destinatarios de dos formas: 
 -  UUID: El servicio revisará los permisos e intentará enviar la notificación segun sea o no el caso.
 -  Email: El correo se enviará sin consultar el permiso del usuario, siendo que el método esta reservado para servicios del sistema que lo requieran ej: Autentificacion de la cuenta mediante correo. Por último, el endpoint de envío cuenta con un booleano para el envio hacia todos los usuarios registrados en el sistema, para poder hacer uso de esta opción el solicitante requiere de un JWT único de administradores del sistema.

### Push

Las notificaciones push tan solo pueden ser enviadas proporcionando los UUID del usuario y el envío del mismo dependera completamente de los permisos del usuario. Cuenta con campos para que el front pueda identificar que servicio solicitó la request y el ID de la entidad que lanzó dicha request.

## Historial de Notificaciones Push

El sistema registra toda notificación Push enviada hacia cada usuario para poder mantener un historial de notificaciones del usuario. Cada entrada del historial incluye:

 - Contenido de la notificación

 - Fecha y hora de envío

 - UUID del destinatario

 - Campo read: booleano para marcar si la notificación fue leída por el usuario

## Registro de las notificaciones

El sistema registra todo intento de envio de Notificaciones, guardando el contenido que intento enviar y el estado del mismo, ya sea enviado, no enviado por falta de permisos o error del servicio. Para obtener los registros se creo un endpoint que solo puede ser utilizado por administradores.

⚠️ Deuda pendiente de seguridad: El envio de emails por correo electronico explícito no realiza una verificación del solicitante. La solución podría darse teniendo una API KEY entre los servicios. También podriamos aceptar este tipo de mensajes tan solo si el solicitante viene de una red privada no una pública.
