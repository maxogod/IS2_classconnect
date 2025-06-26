# Kong Api Gateway

[[<] Go back home](../README.md)

Como se menciono en el documento de [arquitectura](./architecture.md), para unificar todos los servidores en una misma interfaz (hacia el exterior) se utilizo un api-gateway. En este caso, se eligió **Kong** por su robustez, extensibilidad y facilidad de integración con Kubernetes.

## Integracion en k8s

Kong se desplegó como parte del clúster de Kubernetes (tipo de pod: *LoadBalancer*), utilizando su modo **ingress controller**. Esto permitió que cada microservicio exponga sus endpoints internamente, mientras que Kong los publica de manera centralizada y segura a través de una unica IP externa.

La configuracion del mismo es la siguiente:

| Ruta               | Servicio destino                  |
|--------------------|-----------------------------------|
| IP/users           | users-microservice:8080         |
| IP/courses         | courses-microservice:8080       |
| IP/forum           | forum-microservice:8080         |
| IP/administration  | administration-microservice:8000|
| IP/ai              | ai-microservice:8000            |
| IP/notifications   | notifications-microservice:8000 |
| IP/backoffice      | backoffice-app:80               |

De esta manera, ningun microservicio tiene IP externa (son todos del tipo: *ClusterIP*) y el unico servicio dentro del cluster que tiene una es el servicio **kong-kong-proxy (LoadBalancer)**. 

## Plugins

Kong ofrece la oportunidad de crear plugins (por defecto en el lenguaje **lua**) para la api-gateway de manera tal que se pueda aplicar cierta logica a las requests antes de llegar al servicio destino, algunos ejemplos son:

- Filtro de seguridad antes de conectar con un servicio protegido.
- Agregacion de requests con multiples servicios.
- Entre otros.

Por ciertas dificultades con las dependencias necesarias para lograr el uso de algunas librerias de lua dentro del plugin se decidio no utilizar esta feature e implementar la seguridad y proteccion de endpoints de otra manera.
