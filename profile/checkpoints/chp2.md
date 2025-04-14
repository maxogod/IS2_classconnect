[**Volver**](../README.md)

## Checkpoint 2

Se lograron hacer xyz avances con los servicios y la app.

### Cambios respecto al anterior checkpoint

Se decidio utilizar Kong como api-gateway y load-balancer en lugar de nginx.

### Backlog comprometido

- users signup, login, google oauth, profile get/update
- courses CRUD
- mobile app, blabla

### CI/CD

En PR a dev o main corren los tests para asegurar que no haya ningun cambio que rompa las features existentes. En PUSH a main se ejecuta el pipeline de construccion de docker image, publicacion al registro de imagenes de docker de github GHDR, actualizacion de configuraciones de HELM y finalmente el despliegue de la nueva version del servicio en LKE (linode kubernetes engine).

### Tests & Coverage

Se utiliza codecov para la visualizacion en dashboard y para las badges de coverage, en PR a dev o main corren los tests y se envian los resultados de covertura a dicho servicio externo.

### E2E app-backend

servicios en cloud, mas precisamente linode kubernetes engine.

users basico con signup/login/getbyid.
courses CRUD basico.
mobile-app interfaz para login, si es exitoso se redirije a lista de courses personales, donde se puede crear nuevos, etc.