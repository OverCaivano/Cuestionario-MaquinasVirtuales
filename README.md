# Cuestionario Práctico - Máquinas Virtuales, Docker y GitHub Actions

## Alumno: Over Caivano
## Fecha: 16/04

---

## Máquinas Virtuales

1. ¿Qué es una máquina virtual y para qué se utiliza?
Una Maquina Virtual (Vm's) es una computadora que existe dentro de otra computadora. En lugar de ser una PC fisica, es un software que imita el comportamiento de una computadora completa, lo que te permite ejecutar un sistema operativo y aplicaciones como si estuvieras en una computadora fisica. Las Vm's se utilizan para tener entornos virtuales comunes para desarrollar o para pegar proyectos en internet.

2. Nombrá dos diferencias entre una máquina virtual y una computadora física.
Una de las diferencias es que una computadora fisica es un dispositivo fisico con componentes reales, El sistema operativo corre directamente sobre los componentes. Y una maquina virtual es puramente software, no tiene piezas propias; es un conjunto de archivos que simulan el hardware, vive dentro de una computadora física y depende de un software para existir.

3. ¿Qué función cumple un hipervisor?
El hipervisor es la pieza de software mas importante en la virtualización, ya que su funcion principal es actuar como un traductor y mediador entre el hardware físico de la computadora y las máquinas virtuales que corren sobre ella.
Sin un hipervisor, no podrias ejecutar varios sistemas operativos a la vez porque todos intentarian tomar el control total del procesador y la memoria, causando un choque del sistema.

4. Mencioná dos programas que permitan crear máquinas virtuales.
-Oracle VM VirtualBox (Gratuito y de Código Abierto)
-VMware Workstation (Profesional y de Alto Rendimiento)

5. ¿Qué significa asignar 4 GB de RAM a una máquina virtual?
Cuando asignas 4 GB de RAM a una maquina virtual, le estas diciendo al hipervisor que reserve esa cantidad especifica de la memoria fisica de tu computadora para que la use exclusivamente el sistema operativo "invitado".

6. ¿Qué es una imagen ISO y para qué sirve?
Una imagen ISO es un archivo informatico que actua como una copia exacta, es el sistema de archivos que utilizan los discos compactos. Basicamente, es como un "contenedor" que guarda no solo los archivos, sino tambien la estructura del disco, los datos de arranque y la configuracion original.
Las imágenes ISO son el estandar para distribuir software pesado por tres razones: 
-Instalación de Sistemas Operativos
-Copias de Seguridad (Backups)
-Unidades Virtuales

7. ¿Para qué se utiliza SSH al conectarse a una máquina virtual Linux?
SSH es el protocolo estandar para administrar servidores Linux de forma remota. Cuando lo usas para conectarte a una maquina virtual, basicamente estas abriendo un camino seguro y cifrado que te permite tomar el control de la terminal de esa maquina como si estuvieras sentado frente a ella.

8. Escribí el comando para conectarte por SSH al usuario `admin` en la IP `192.168.1.50`
- ssh admin@192.168.1.50

9. ¿Qué significa que una máquina virtual sea efímera?
Que una maquina virtual sea efimera significa que su ciclo de vida es temporal, basicamente esta diseñada para ser creada, cumplir una funcion especifica y luego ser destruida sin dejar rastro.

10. ¿Qué ventaja tiene usar snapshots en una VM?
Funcionan como un "botón de guardado" que captura el estado exacto de tu maquina virtual en un momento preciso (incluyendo el disco, la memoria RAM y la configuracion). La gran ventaja es la reversibilidad instantanea: si algo sale mal, puedes volver al estado exacto donde todo funcionaba en cuestion de segundos.

---

## Docker

11. ¿Cuál es la diferencia entre imagen Docker y contenedor Docker?
La diferencia es que la imagen Docker es un archivo comprimido que contiene todo lo necesario para que una aplicacion funcione y un contenedor Docker es es la instancia viva y en ejecucion de una imagen. Si ejecutas una imagen, obtienes un contenedor.

12. ¿Qué comando muestra los contenedores en ejecución?
- docker ps

13. ¿Qué comando muestra todos los contenedores, incluso detenidos?
- docker ps -a

14. ¿Qué comando se usa para descargar una imagen de Ubuntu?
- docker pull ubuntu

15. ¿Qué comando crea y ejecuta un contenedor Ubuntu interactivo?
- docker run -it ubuntu /bin/bash

16. ¿Qué significa mapear el puerto `8080:80`?
Mapear el puerto `8080:80` permite que el mundo exterior (tu computadora o internet) se comunique con el proceso que vive dentro del contenedor. Cuando ves -p 8080:80, Docker esta creando un camino entre tu maquina real y el contenedor.

17. Nombrá tres estados posibles de un contenedor Docker.
- Running (Ejecutándose)
- Exited (Detenido/Salido)
- Paused (Pausado)

18. ¿Qué comando detiene un contenedor llamado `webapp`?
docker stop webapp

19. ¿Qué comando elimina un contenedor llamado `mysql-db`?
docker rm mysql-db

20. Escribí un ejemplo simple de `docker run` con nginx exponiendo puerto 8080.
docker run -d -p 8080:80 --name mi-servidor nginx

---

## GitHub Actions

21. ¿Qué es GitHub Actions
GitHub Actions es la plataforma de automatizacion nativa de GitHub que te permite programar tareas que se ejecutan automaticamente cada vez que ocurre algo en tu repositorio.

22. ¿Para qué sirve un archivo YAML en GitHub Actions?
Un archivo YAML en GitHub Actions es el cerebro de la automatizacion. Es el lugar donde escribis las instrucciones precisas que GitHub debe seguir cada vez que sucede algo en tu repositorio.

23. ¿En qué carpeta se guardan los workflows?
Los workflows se guardan en la siguiente ruta ".github/workflows/"

24. ¿Qué evento ejecuta un workflow cuando se hace push al repositorio?
- on:push

25. ¿Qué hace la action `actions/checkout`?
Descarga el codigo de tu repositorio en la maquina virtual (runner) donde se esta ejecutando el workflow.

26. ¿Qué hace la action `actions/setup-node`?
Es la encargada de preparar el entorno de ejecución (el Runner) para que pueda entender y ejecutar comandos de Node.js.

27. ¿Para qué sirve automatizar tests en CI/CD?
La automatizacion de tests en un entorno de CI/CD  es lo que permite que un equipo pase de "lanzar codigo una vez al mes" a "lanzar codigo varias veces al dia" con total confianza.

28. Escribí una estructura mínima de workflow con `push`.
name: Mi Primer Workflow

on: [push]

jobs:
  saludo:
    runs-on: ubuntu-latest
    steps:
      - name: Saludar a Nucleo Tech
        run: echo "¡El workflow de la web de PC está funcionando!"

29. ¿Qué ventaja tienen las runners efímeras?
Las runners efimeras garantizan un entorno limpio y determinista. En lugar de tener un servidor "siempre encendido" donde los restos de ejecuciones anteriores pueden causar errores fantasma, una runner efimera es como una hoja en blanco que se destruye apenas termina tu tarea.

30. ¿Qué pasaría si falla un test en el pipeline?
Si falla un test en un pipeline pasa esto: el pipeline se detiene, el estado queda como “failed”, No se hace el deploy (en la mayoría de los casos), Se notifica al equipo, Tenes que corregir y volver a ejecutar.

---

## Práctica

31. Escribí el comando para crear una carpeta llamada `proyecto_vm`.
- mkdir proyecto_vm

32. Escribí el comando Linux para entrar en esa carpeta.
- cd proyecto_vm

33. Escribí el comando para crear un archivo llamado `app.js`.
- touch app.js

34. Escribí un Dockerfile mínimo usando Node.js.
FROM node:20-slim

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]

35. Escribí un workflow de GitHub Actions que ejecute `npm install` y `npm test`.
name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test
