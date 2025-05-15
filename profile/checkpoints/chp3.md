[**Volver**](../README.md)

## Checkpoint 3

Para este checkpoint se ha colocado como objetivo una serie de elementos a desarrollar presentes en el backlog de esta organización, y además incorporar un sistema de analisis de métricas sobre los servicios.

### Cambios respecto al anterior checkpoint

1. Se cambió en  el servicio de notificaciones, el sistema de notificaciones smtp relay, a sistema de notificaciones utilizando Brevo.

#### Sistema de Métricas

Se añadió un sistema de monitoreo a los microservicios utilizando la plataforma [Datadog](https://www.datadoghq.com/), y se ha desplegado un agente de datadog para el clúster que se encuentra montado en la nube de kubernetes, y además un datadog node agent por cada nodo, desplegados como daemonset.
De esta forma, obteniendo de esta forma las métricas de todos los servicios en cada nodo, como el funcionamiento y estado de la infraestructura y recursos presentes en el nodo.
Se añandió un nuevo repositorio de infraestructura como código, donde se ejecuta la acción correspondiente para cargar la integración de herramientas de monitoreo de datadog en nuestro clúster.

### Backlog comprometido

El backlog comprometido se puede visualizar [aqui](https://github.com/orgs/ClassConnect-org/projects/1/views/3), este consiste en los siguientes items:

**Users:**

- View my profile  ✔️
- View others profiles ✔️
- Edit Profile ✔️
- Picture Storage ✔️
- Google Login ✔️
  
**Courses:**

- Get Detailed Courses Info ✔️
- Filter Courses ✔️
- Validate Data for Courses  ✔️
- Assignments and Evaluations CRUD ✔️
- Enroll Student in Course  ✔️
- Visualize Courses ✔️
- Configure Eligibility Criteria for Courses ❌
- Get Courses Containing Students ❌
  
**Mobile-app:**

- Create Design from tasks and exams ✔️
- Receive and Send Courses Information ✔️
- Add login session system and its persistance ✔️
- Make views only accesable by ownership on courses  ✔️
- Create edit profile view ✔️
- Add working profile view GET request to users service ✔️
- Make views only accesable by ownership on tasks ❌
- Design edit and delete course view

**Notifications:**

- Send Email Notifications for Events  ✔️
- User Notifications Configuration ✔️
- Log Notifications  ✔️
- Send Push Notifications ❌

**Administration:**

- Rules (CRUD)  ✔️
- Admin Creation & Login ✔️
- Audit Log ❌

### Cloud

Se utilizó como recurso de cloud storage a [Supabase Storage](https://supabase.com/docs/guides/storage), donde se almacenan hasta el momento las imagenes de perfil de los usuarios.


**Ejemplo de dashboards**

Entre los dashboards disponibles se encuentran los más relevantes:

System metrics:


![system metrics](../img/system_metrics.png)


System networking: 

![system networking](../img/system_networking.png)


Kubernetes pods overview:


![kubernetes pods overview](../img/kube_pods.png)


También se agrego un sistema de monitoreo con alarmas disparadoras donde al activarse al pasar un umbral seteado por ejemplo de uso de CPU en alguno de los nodos, se envía una notificación por email:

![monitor](../img/monitor.png)

### Muestra de aplicación:

Vista previa del UI de la aplicación:


