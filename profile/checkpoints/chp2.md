[**Volver**](../README.md)

## Checkpoint 2

Para este checkpoint se tuvo como objetivo incorporar una base para cada uno de los servicios propuestos en el anterior checkpoint, y desplegar los mismos en la nube mediante pipelines de integracion y delivery. A su vez agregarle a cada uno una forma de ver su covertura de tests. Y finalmente integrar algunos endpoints basicos con la aplicacion.

### Cambios respecto al anterior checkpoint

1. Se decidio utilizar [Kong](https://konghq.com/) como Api-Gateway y Load-Balancer en lugar de Nginx ya que esta mejor preparado para este caso de uso, y a su vez es mas simple de extender con plugins personalizadas. Esto ultimo se planea utilizar para verificar *requests* antes de ser entregadas al micro-servicio destino (e.g. tiene que ser administrador para acceder al respectivo servicio).
2. Se cambio el stack del micro-servicio **Notifications** de `Go + Gin-Gonic` a `Python + Fastapi`, por la mayor cantidad de librerias que facilitan y reducen los tiempos de implementacion del servicio.

### Backlog comprometido

El backlog comprometido se puede visualizar [aqui](https://github.com/orgs/ClassConnect-org/projects/1/views/3), este consiste en los siguientes items:

**Users:**

- Creación de base de datos (Supabase - Postgres). ✔️
- Implementación de registro. ✔️
- Implementación de ingreso a cuentra registrada. ✔️
- Integración de autenticación de Google. ❌
  
**Courses:**

- Creación de base de datos (Supabase - Postgres). ✔️
- Implementación del CRUD. ✔️
  
**Mobile-app:**

- Vistas de paginas principales.
- Vistas de creacion e ingreso a cuenta por e-mail y por google auth. ✔️
- Vista de perfil de cuenta. ✔️
- Vista de creación y listado de courses. ✔️
- Integración de servicio de users. ✔️
- Integración de servicio de courses. ✔️

**Notifications:**

- Implementación de notificaciones Push/E-mail. ❌

### CI/CD

En PR a dev o main corren los tests para asegurar que no haya ningun cambio que rompa las features existentes. En PUSH a main se ejecuta el pipeline de construccion de docker image, publicacion al registro de imagenes de docker de github GHDR, actualizacion de configuraciones de HELM y finalmente el despliegue de la nueva version del servicio en LKE (linode kubernetes engine).

### Tests & Coverage

Se utiliza codecov para la visualizacion en dashboard y para las badges de coverage, en PR a dev o main corren los tests y se envian los resultados de covertura a dicho servicio externo.

### E2E app-backend

servicios en cloud, mas precisamente linode kubernetes engine.

users basico con signup/login/getbyid.
courses CRUD basico.
mobile-app interfaz para login, si es exitoso se redirije a lista de courses personales, donde se puede crear nuevos, etc.
