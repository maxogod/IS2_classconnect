# Analisis postmortem

[[<] Go back home](../README.md)

## Uso de kubernetes

El uso de k8s permitio mucha flexibilidad a la hora de agregar nuevos micro-sevicios o servidores por medio de simplemente crear un nuevo repositorio con un *dockerfile* acorde y re-utilizar el CI/CD pipeline de otro repositorio desplegado (ajustando detalles como secrets), asi como tambien la facil administracion de recursos, rapido re-inicio o re-despliegue de servicios caidos, y orquestrado de *pods* intercomunicados por una red privada inaccesible al internet publico.

A pesar de los beneficios obtenidos por esta herramienta, debido a la empinada curva de aprendizaje de este tipo de motores, su uso llevo a un aumento considerable del *lead time* en las primeras iteraciones del proyecto, principalmente a la hora de configurar nuevos secretos, o modificar valores de despliegue. Sin embargo, se considero que es una herramienta muy potente y tiene mucho sentido utilizarla en proyectos grandes reales (teniendo en cuenta que es bastante mas costosa que otro tipo de herramientas), donde la disponibilidad de servicios es critica y se tiene una amplia gama de los mismos.

## Uso de react-native

En el caso de no tener experiencia con el front en aplicaciones relativamente grandes, se complica llevar un estructura ordenada de elementos a utilizar, y definir cuales son las buenas prácticas. Quizas sea un tema a adquirir con experiencia pero cuesta también encontrar una guia "definitiva" o parcialmente efectiva para llevar a cabo un orden en el diseño.

Al iniciar fue complicado comprender un poco los comandos ejecutables de React native para limpiar caches, reiniciar la imagen de Gradlew y ver que archivos es recomendable versionar para no perder configuraciones sobre la app, notificaciones y servicios.

Uno de los temas que se tuvo que investigar es como hacer las navegaciones entre vistas de manera correcta, ordenada y sin tener código repetido. El uso en este caso de una barra de navegación lateral no es tan simple de diseñar como se esperaba y requería de más investigación.

De igual manera en el tema de autenticación de google si bien hay guias que si las seguis deberia salir todo bien, no son ordenadas y no siempre salen los resultados como te dicen las guias y hay que buscar información por fuera de las guias.
También, por tema de no buscar en documentación oficial, se desperdició tiempo utilizando librerias de react native oficial que estaban deprecadas y el compilador no te avisa.

Algunos componentes ya sea en librerias oficiales y de material designs toman demasiado tiempo para implementar, ya sea hasta un simple boton de confirmación, hay que tener experiencia previa con algunos componentes o sentarse a ver la documentación del componente, si es un componente con muchas características se vuelve tedioso, y en termino de este proyecto se optó por utilizar por ejemplo Modal en lugar de componentes avanzados por este motivo.

También otra dificultad encontrada fue que al querer generar e instalar la apk en un celular, no es tan directo y hay que hacer unos cuantos pasos, que tiene varias formas de hacer, pero a pesar de eso, hay detalles que tenés que haber manejado antes, por ejemplo en nuestro proyecto fallaba porque no se usaba una libreria específica "Config" para cargar correctamente las variables de entorno al generar la apk.

Es pésimo que una libreria de Firebase dependa de otra cuando se utilizan sublibrerias de Firebase, tienen que tener toda la misma versión, y tanto desinstalarlas como instalarlas no es tan simple como deberia (gracias npm).

Incluso con muchísima ayuda de la IA ayudandome a configurar correctamente con decenas de errores de creación de imagen apk para desarrollar, se vuelve demasiado tedioso la configuración para poder utilizar una libreria de notificaciones "expo-notifications" y/o "firebase/messaging". Nos salvó la simpleza y efectividad de configuración de OneSignal para notificaciones.
SonaQube nos ayudó mucho para debuggear mas rapido algunos errores que podian pasar desapercibidos.

Un buen tiempo de desarrollo fue ahorrado al utilizar un celular real para debuggear la aplicación, mediante conexión USB (expo Go no duró mucho ya que si necesita Google Auth ya no funciona, por el momento), con el android emulator trajo muchos problemas de rendimiento y no se supo configurar correctamente.

## Servicios de notificaciones (email/push)

O mejor dicho, los mil y un problemas de dependencias. Uno de los servicios que parecía sencillo de llevar a cabo, termino necesitando 5 procesos de refactorización. En parte cae en mi culpa por ansioso y no leer todos los detalles antes de empezar a implementar, pero eso no quita la dificultad para encontrar el servicio indicado para un proyecto educativo. 

Ya sea la falta de un dominio web para establecer conexiones seguras de email (requerido por la mayoria de los proveedores de correos transaccionales). O bien el simple relay de google, el cual funcionaba perfecto de manera local, pero una vez deployado Linode nos bloqueaba las comunicaciones de los puertos STMP por contar con la cuenta freemium, de paso recomendandonos de utilizar su servicio pago. 

Por el lado de las notificaciones push las cosas parecían prometedoras desde el back, pero como se comento en la sección de react-native, con solo instalar la sdk oficial de google los errores de dependecias eran interminables y no hubo forma de hacer que compile la aplicación. Tras unas semanas en stand-by desde el lado del back decimos buscar otra alternativa. 

Por suerte luego de muchos intentos de prueba y error, conseguimos dos servicios que cumplen las expectativas de lo que se espera para el proyecto. 

[Brevo](https://www.brevo.com/es/), cuenta una interfaz muy sencilla de utilizar y un generador de plantillas bastante práctico, el único detalle en contra es que al pasarle variables dinamicas para colocar nuestro cuerpo no permitía que el contenido sea en formato html (o que siquiera tome los saltos de linea). Esto se soluciono trayendo el codigo html directo al servicio y reemplazando desde el mismo código los placeholders para nuestros asuntos y cuerpos de los emails. 

[OneSignal](https://onesignal.com), la mayor sorpresa del proyecto. Bastante sencillo de setear y con una funcionalidad muy práctica que simplificó lo que sería la comunicación entre el front y el back. El servicio te permite asociar un id con el token de notificaciones, por ende no es necesario llevar información especifica de onesignal y convenientemente el back no necesita asociar los datos pasados por otros microservicios a la hora de enviar notificaciones. Sin duda lo recomendamos para futuros proyectos de la materia.

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

## Alertas de monitoreo

A continuacion se destaca un hecho que ocurrio durante el desarrollo del proyecto y concierne al sistema de monitoreo, especificamente a las alertas de sobre-uso de memoria.

A los administradores de la plataforma, cuyos emails se encuentran registrados en el google groups de administradores mencionado en el documento de [datadog](../tech/datadog.md), les llego una serie de emails, conteniendo informacion de aviso que uno de los nodos que forman parte del cluster de k8s tenia solamente 10% de la memoria restante sin utilizar. Esto llamo la antencion ya que nunca se habia activado dicha alarma, por lo que el equipo comenzo a investigar sobre la causa de la misma. Observando detenidamente las metricas capturadas en uno de los dashboards de la plataforma de datadog, se detecto que los micro-servicios cuyo stack tecnologico constaba de **python + fastapi**, consumian mucha mas memoria ram que el resto de servicios (de **go**). Finalmente se descubrio la causa al leer documentacion sobre fastapi y su comportamiento al configurar una cantidad mayor a 1 de *worker threads*, que ocaciona una subida significativa del uso del CPU y de la memoria, por lo que al disminuir la cantidad de dichos workers a 1, el problema fue solucionado.

## Backlog

Como se menciona en el documento sobre la gestion del proyecto, se confecciono la enteridad del backlog desde el inicio del proyecto, esto si bien ahorro tiempo futuro de re-lectura de las historias de usuario, tambien llevo a una considerable cantidad de cambios sobre dichas *issues* mayormente por temas de cambios de responsabilidades entre servicios, entre otras cosas. El equipo considero que lo mas efectivo hubiese sido confeccionar el backlog en una reunion *por iteracion* a medida que avanza el proyecto para evitar cambios y que las *issues* sean mas representativas del estado del momento.
