# Pipelines

[[<] Go back home](../README.md)

Cada micro-servicio cuenta con pipelines de intregracion continua y despliegue continuo (implementados con github-actions),
que estan conformados por un pipeline de pre-commit, uno de tests y finalmente uno de 
despliegue (solamente cuando se aceptan los cambios a la rama de produccion), los cuales se abordan a continuacion:

Ramas con activacion de pipelines:

- Dev (staging branch): todo lo que se acepta en esta rama se tiene que probar y garantizar su buen funcionamiento para seguir al proximo paso.
- Main (production branch): todo lo que se acepta en esta rama, automaticamente se aplican los cambios en la nube (en este caso en k8s).

## Tests (on pull request - dev, main)

Los pipelines de tests consisten en la ejecucion de las pruebas unitarias y de integracion encontradas en el repositorio y el
*logueo* en un archivo conteniendo la informacion de covertura de tests proporcionada por la herramienta utilizada, `go test` en el caso de los
micro-servicios cuyo stack utiliza **go**, o `pytest` en el caso de **python**.

Luego de esto se transmite la informacion al servicio de coverage utilizado en el proyecto [**CodeCov**](https://app.codecov.io/gh/ClassConnect-org)
utilizando el secret correspondiente (guardado de forma segura en el repositorio).

A partir de que CodeCov recibe esta informacion y la procesa, este re-calcula el coverage actual del servicio afectado y automaticamente
comenta en la *Pull Request* si la misma cumple lo minimo de coverage esperado para la introduccion de nuevo codigo (caso contrario, falla el pipeline).

## Pre-Commit (on pull request - main)

Los pipelines de pre-commit son mas simples, estos solo se encargan de correr una serie de checkeos del codigo (dependiente del stack usado),
para garantizar la homogeneidad del mismo, evitando errores de sintaxis, malos formatos, mal uso de tipos, etc. Si hay un problema
en alguno de los checks mencionados, el pipeline falla.

## Deploy (on push - main)

Finalmente cuando el codigo pasa los filtros y es aceptado para formar parte de la version en produccion del servicio, se ejecuta el pipeline de deployment.

Este se encarga de:

- Contruir la imagen de docker a partir del Dockerfile encontrado en la raiz de cada repositorio.
- Autenticarse en github container repository (**ghcr**).
- Subir la imagen de docker construida como [*package*](https://github.com/orgs/ClassConnect-org/packages) a GHCR.
- Crear el secreto en k8s para poder descargar dicha imagen desde el repositorio.
- Ejecuta la instalacion con *heml* del servicio en el cluster de k8s, inyectando los secretos necesarios (almacenados de manera segura en gh repository secrets).

Luego de ejecutado este pipeline, se descarta el deployment anterior en el cluster y se crea el nuevo pod actualizado (eliminando al viejo).
