# Manual de usuario [Backoffice]

[[<] Go back home](../README.md)

El Backoffice de ClassConnect es la plataforma web exclusiva para administradores, donde podrán controlar, mantener y supervisar el funcionamiento de la aplicación.

## Inicio de Sesión como Administrador

Para acceder al Backoffice, es necesario:

 - Haber sido registrado previamente como administrador por otro administrador.

 - Ingresar con las credenciales otorgadas por este administrador.

⚠️ Los administradores pueden permanecer logueados por una hora. Luego de este período, deberán volver a ingresar sus credenciales para continuar utilizando la plataforma.

Una vez dentro, los administradores podrán navegar por el menú lateral para acceder a las distintas funcionalidades del sistema.

## Gestión de Reglas de la Aplicación

Los administradores tienen la responsabilidad de crear, modificar o eliminar reglas que rigen el comportamiento y uso de la aplicación.

⚠️ Cualquier cambio en las reglas debe realizarse con máxima precaución, ya que puede impactar directamente en la experiencia de todos los usuarios.

Una vez efectuados los cambios, todos los usuarios registrados recibirán un email con los detalles actualizados de las reglas modificadas, creadas o eliminadas.

## Moderación de Usuarios

Dentro de la sección Users, se lleva a cabo la gestión de usuarios registrados en la aplicación. Esta sección permite:

 - Bloquear usuarios hasta una fecha determinada. Mientras estén bloqueados, no podrán acceder a la app.

 - Eliminar usuarios, eliminando su cuenta de forma permanente.

## Logs de la aplicación

Los administradores tienen acceso a registros internos de actividad, organizados en dos categorías principales:

### Logs de Auditoría

Encargado de registrar todos los cambios hechos en las reglas y normativas de la aplicación. Cada entrada incluye:

 - Acción realizada (crear, editar, eliminar)

 - Administrador que efectuó el cambio

 - Detalles del cambio aplicado

### Logs de Notificaciones

Encargado de registrar los envios de notificaciones de la aplicación. Cada registro incluye:

 - Estados de envío: `sent`, `not sent - no permission` y `error`.

 - Tipo de Notificación: `email` o `push`.
 
 - Detalles del contenido enviado y los destinatarios.

## Chat AI

Cuando una respuesta del chatbot Navi recibe una valoración (positiva o negativa), los administradores deben revisarla para:

 - Evaluar si la respuesta podría haberse expresado de forma más clara

 - Determinar si requiere ser ajustada mediante procesos de fine tuning

En caso de uso malicioso o abusivo del sistema, el administrador podrá ver los detalles del usuario que realizó la consulta para tomar las medidas necesarias.

## Manejo de Administradores

Finalmente los administradores podran acceder a la tabla de administradores donde podran buscar la existencia de un administrador segun su email y crear nuevos administradores. Esta es la unica forma de convertirse en administrador y lograr acceso al backoffice.

🚫 Esta es la única forma de convertirse en administrador y acceder a la plataforma de gestión. El administrador tiene la responsabilidad de notificar al nuevo administrador sus credenciales.

