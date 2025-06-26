# Analisis postmortem

[[<] Go back home](../README.md)

## Uso de kubernetes

El uso de k8s permitio mucha flexibilidad a la hora de agregar nuevos micro-sevicios o servidores por medio de simplemente crear un nuevo repositorio con un *dockerfile* acorde y re-utilizar el CI/CD pipeline de otro repositorio desplegado (ajustando detalles como secrets), asi como tambien la facil administracion de recursos, rapido re-inicio o re-despliegue de servicios caidos, y orquestrado de *pods* intercomunicados por una red privada inaccesible al internet publico.

A pesar de que los beneficios obtenidos por esta herramienta, debido a la empinada curva de aprendizaje de este tipo de motores, su uso llevo a un aumento considerable del *lead time* en las primeras iteraciones del proyecto, principalmente a la hora de configurar nuevos secretos, o modificar valores de despliegue. Sin embargo, se considero que es una herramienta muy potente y tiene mucho sentido utilizarla en proyectos grandes reales (teniendo en cuenta que es bastante mas costosa que otro tipo de herramientas), donde la disponibilidad de servicios es critica y se tiene una amplia gama de los mismos.