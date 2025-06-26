# Analisis postmortem

[[<] Go back home](../README.md)

## Uso de kubernetes

El uso de k8s permitio mucha flexibilidad a la hora de agregar nuevos micro-sevicios o servidores por medio de simplemente crear un nuevo repositorio con un *dockerfile* acorde y re-utilizar el CI/CD pipeline de otro repositorio desplegado (ajustando detalles como secrets), asi como tambien la facil administracion de recursos, rapido re-inicio o re-despliegue de servicios caidos, y orquestrado de *pods* intercomunicados por una red privada inaccesible al internet publico.

A pesar de los beneficios obtenidos por esta herramienta, debido a la empinada curva de aprendizaje de este tipo de motores, su uso llevo a un aumento considerable del *lead time* en las primeras iteraciones del proyecto, principalmente a la hora de configurar nuevos secretos, o modificar valores de despliegue. Sin embargo, se considero que es una herramienta muy potente y tiene mucho sentido utilizarla en proyectos grandes reales (teniendo en cuenta que es bastante mas costosa que otro tipo de herramientas), donde la disponibilidad de servicios es critica y se tiene una amplia gama de los mismos.

## Uso de react-native

!niko has lo tuyo

## Uso de notificaciones (email/push)

!joako has lo tuyo

## Uso de gemini (AI)

Las razones por las que Gemini fue elegido por encima de otros LLMs se explica en la sección del Microservicio de Inteligencia Artificial, por lo cual en este apartado se explicará una mala desición que fue tomada.   
El enfoque inicial para la mejora continua se basaba en la técnica de Fine-Tuning que se basa en proporcionarle un gran volumen de datos a la API de Gemini para que sean usados en la creación de un modelo completamente nuevo.    
Se optó originalmente por este método debido a que es considerado robusto y era accesible gratuitamente.   
Se supone que este enfoque falló justamente por esas dos cosas.   
Luego de armar el servicio alrededor de dicha funcionalidad, llegó la hora de finalmente probarlo. El manual de usuario sugería que se le solicite a la API de Gemini que se realice el trabajo de Fine-Tuning y que el programa se quede haciendo un Probing verificando si dicho trabajo había sido terminado.   
Aproximadamente 30 horas estuvo corriendo el programa, el estado del trabajo nunca dejo de ser "Job Queued".   
Luego de las 30 horas llegó el [outage de google cloud](https://status.cloud.google.com/incidents/ow5i3PPK96RduMcb1SsW) por el cual la persona que estaba a cargo de este microservicio (Martín Osan, quien casualmente se encuentra escribiendo esto) tuvo muchos dolores de cabeza en su trabajo de DevOps.   
Cuando llegó a su casa luego de un largo día en la oficina, vió que el programa que había dejado corriendo había crasheado, probablemente debido al incidente de Google Cloud.
Fue ese el momento en el que se decidió investigar una alternativa algo menos robusta pero más sencilla.   

La conclusión que se puede extraer de esto es: Nada es gratis. Menos si es bueno.

## Backlog

Como se menciona en el documento sobre la gestion del proyecto, se confecciono la enteridad del backlog desde el inicio del proyecto, esto si bien ahorro tiempo futuro de re-lectura de las historias de usuario, tambien llevo a una considerable cantidad de cambios sobre dichas *issues* mayormente por temas de cambios de responsabilidades entre servicios, entre otras cosas. El equipo considero que lo mas efectivo hubiese sido confeccionar el backlog en una reunion *por iteracion* a medida que avanza el proyecto para evitar cambios y que las *issues* sean mas representativas del estado del momento.
