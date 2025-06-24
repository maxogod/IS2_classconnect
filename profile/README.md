# ClassConnect

ClassConnect es una plataforma de gestión educativa diseñada para facilitar la enseñanza y el aprendizaje en entornos digitales. Su propósito es permitir que docentes y estudiantes interactúen de manera efectiva mediante la creación de clases, asignaciones, exámenes, y recursos educativos en línea. La plataforma evalua integrar un modelo LLM para mejorar la generación de contenido educativo, automatizar correcciones y proporcionar asistencia personalizada a estudiantes y docentes.

<div align="center">
<img src="./img/cc_logo.png" alt="logo" width="80px" />
</div>

![Linode](https://img.shields.io/badge/Linode-00A95C?logo=linode&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Kong](https://img.shields.io/badge/Kong-002659?logo=kong&logoColor=white)
![Microservices](https://img.shields.io/badge/Microservices-FF6F00?logo=docker&logoColor=white)
![Datadog](https://img.shields.io/badge/Datadog-632CA6?logo=datadog&logoColor=white)
![Gemini AI](https://img.shields.io/badge/Gemini--AI-4285F4?logo=google&logoColor=white)
![Codecov](https://img.shields.io/badge/Codecov-F01F7A?logo=codecov&logoColor=white)
![Gin Gonic](https://img.shields.io/badge/Gin--Gonic-00ADD8?logo=go&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?logo=supabase&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)
![Mobile App](https://img.shields.io/badge/Mobile--App-20232a?logo=react&logoColor=61dafb)
![Web App](https://img.shields.io/badge/Web--App-61DAFB?logo=react&logoColor=black)

## Documentación general

Documentos orientados a dar una visión global del sistema, su estructura, uso y proceso de desarrollo.

| Documento                       | Link |
|----------------------------------|------|
| Arquitectura & Infraestructura            | <p align="center">[[>]](./tech/architecture.md)</p> |
| Manual de usuario Backoffice     | <p align="center">[[>]](./man/backoffice.md)</p> |
| Manual de usuario Mobile         | <p align="center">[[>]](./man/mobile.md)</p> |
| Backlog & Organización           | <p align="center">[[>]](./misc/backlog.md)</p> |
| Análisis Postmortem              | <p align="center">[[>]](./misc/postmortem.md)</p> |

## Documentacion tecnica

Referencias para el equipo de desarrollo sobre servicios, infraestructura y aplicaciones implementadas.

### Repositorios IaC

Contiene la configuracion del kong-api-gateway y herramientas de monitoreo.

| Servicio        | Docs                                               | Repo                                 |
|-----------------|----------------------------------------------------|--------------------------------------|
| API Gateway           | <p align="center">[[>]](./tech/api_gateway.md)</p>       | <p align="center">[[>]](https://github.com/ClassConnect-org/api-gateway)</p> |
| Datadog         | <p align="center">[[>]](./tech/datadog.md)</p>     | <p align="center">[[>]](https://github.com/ClassConnect-org/datadog-metrics)</p> |

### Micro-servicios (Backend)

Servicios independientes que componen la lógica del negocio.

| Servicio        | Docs                                               | Repo                                 |
|-----------------|----------------------------------------------------|--------------------------------------|
| Users           | <p align="center">[[>]](./tech/users.md)</p>       | <p align="center">[[>]](https://github.com/ClassConnect-org/users-microservice)</p> |
| Courses         | <p align="center">[[>]](./tech/courses.md)</p>     | <p align="center">[[>]](https://github.com/ClassConnect-org/courses-microservice)</p> |
| Forum           | <p align="center">[[>]](./tech/forum.md)</p>       | <p align="center">[[>]](https://github.com/ClassConnect-org/forum-microservice)</p> |
| Notifications   | <p align="center">[[>]](./tech/notifs.md)</p>      | <p align="center">[[>]](https://github.com/ClassConnect-org/notifications-microservice)</p> |
| AI              | <p align="center">[[>]](./tech/ai.md)</p>          | <p align="center">[[>]](https://github.com/ClassConnect-org/ai-microservice)</p> |
| Administration  | <p align="center">[[>]](./tech/admin.md)</p>       | <p align="center">[[>]](https://github.com/ClassConnect-org/administration-microservice)</p> |

### Aplicaciones (Frontend)

Interfaces de usuario de la plataforma.

| Aplicación     | Docs                                               | Repo                                 |
|----------------|----------------------------------------------------|--------------------------------------|
| Backoffice     | <p align="center">[[>]](./tech/backoffice.md)</p>  | <p align="center">[[>]](https://github.com/ClassConnect-org/backoffice-app)</p> |
| Mobile         | <p align="center">[[>]](./tech/mobile.md)</p>      | <p align="center">[[>]](https://github.com/ClassConnect-org/mobile-app)</p> |

## Bitacoras

Historial de entregas y avances del proyecto a lo largo del cuatrimestre.

### Checkpoints

| Checkpoint | Link |
|---|------|
| Checkpoint 1 | <p align="center">[[>]](./checkpoints/chp1.md)</p> |
| Checkpoint 2 | <p align="center">[[>]](./checkpoints/chp2.md)</p> |
| Checkpoint 3 | <p align="center">[[>]](./checkpoints/chp3.md)</p> |
| Checkpoint 4 | <p align="center">[[>]](./checkpoints/chp4.md)</p> |
