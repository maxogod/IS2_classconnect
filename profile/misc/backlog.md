# Sistema de gestion & Backlog

[[<] Go back home](../README.md)

## Github project

Con el incentivo de mantener al minimo la necesidad de utilizar multiples plataformas para la gestion, organizacion, desarrollo y versionado del proyecto, se decidio utilizar la funcionalidad de github para gestion de proyectos en la misma organizacion (ClassConnect-org) donde se trabajo.

Esta plataforma permitio tener una unica interfaz donde ver el trabajo por hacer, en progreso o terminado, recolectando la informacion de las *issues* de los distintos repositorios que forman parte de la organizacion.

Previo a la confeccion del backlog y la creacion de las tareas, se configuro un entorno que cuenta con:

- Visualizacion de lista de tareas (en cualquier estado).
- Visualizacion del kanban de la iteracion (sprint) del momento.
- Visualizacion del kanban personal.
- Visualizacion *roadmap* a lo largo del tiempo.

## Backlog

El [backlog del proyecto](https://github.com/orgs/ClassConnect-org/projects/1/views/1) se dividio en 4 iteraciones, correspondientes a los 4 checkpoints disponibles en la [homepage](../README.md), y se crearon etiquetas para la urgencia de implementacion asi como tambien una estimacion del tamaño de cada *ticket* a completar.

Antes de iniciar el proceso de desarrollo se crearon todas las issues iniciales, teniendo en cuenta las historias de usuarios y criterios de aceptacion.

A medida que avanzo el proyecto, algunas *features* (opcionales) se dieron de baja y fueron marcadas como **no planeadas**, otras mutaron, otras migraron a otro repositorio mas acorde y otras se dividieron en tickets mas pequeños.

Finalmente se logro cumplir el objetivo de concluir con el backlog requerido y el backlog opcional.

### Historias requeridas

| Categoría                      | Historias Principales                              |
|--------------------------------|----------------------------------------------------------|
| Usuarios                       | Registro, login (email y federado), perfiles             |
| Clases                         | Gestión de cursos, inscripción, visualización            |
| Asignaciones y Evaluaciones    | Tareas, exámenes, feedback, notas                        |
| Comunicación y Notificaciones  | Notificaciones push y email                              |
| Métricas y Análisis            | Estadísticas de desempeño                                |
| Administración de Plataforma   | Gestión de usuarios y permisos                           |

### Historias opcionales

| Historia              | Puntos                              |
|---------------------|--------------------------------------|
| Kubernetes (k8s)    | <p align="center">8</p>              |
| Monitoreo y metricas           | <p align="center">5</p>              |
| Reglas y normativas | <p align="center">5</p>              |
| Chat AI             | <p align="center">8</p>              |
| Foro                | <p align="center">5</p>              |
| Profesores auxiliares          | <p align="center">5</p>              |
| Recupero de contraseña      | <p align="center">2</p>              |
| PIN de registro     | <p align="center">3</p>              |
| **Total**           | <p align="center"><strong>41</strong></p> |
