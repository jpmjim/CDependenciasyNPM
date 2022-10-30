# Curso de Gestión de Dependencias y Paquetes con NPM
NPM => Es un gestor de paquetes, el más popular que tiene JS, donde se encuentra una gran cantidad de recursos para la implementación de proyectos. Crear propios paquetes poder compartirlos.
  https://www.npmjs.com/

Node Package Manager el cual se encarga de administrar todos estos paquetes.

Instalación ultima version "npm install -g nom@lastest"
npm -v version instalada actulizacion con "sudo npm install npm@latest -g"
node -v

Iniciar Proyecto
================
Creamos la carpeta mkdir "jsnpm"
Nos movemos a la carpeta cd jsnpm y inicializamos con "git init" buena practica.

Opcion para inicializacion del proyecto

Iniciamos el proyecto con "npm init" nos permite crear el archivo "package.json" con el cual tenemos una configuración establecida, una descripsion y ciertos valores que necesita.

Inicializacion mas rapida con "npm init -y" genera un documento automatico configuracion minima del archivo package.json.

Configuracion Standar
npm set init.author.email "jpmjim@gmail.com"
npm set init.author.name "Jimmy J. Pecho Malqui"
npm set init.license "MIT"
npm init -y 

Instalación de dependencias (paquete convencional, global)
===========================
Creamos carpeta src dentro de ella el archivo index.js
Instalaciones se hacen en la carpeta raiz del proyecto, donde instalaciones de las dependencias estas son recursos que vamos utilizar dentro de nuestro proyecto.
- "npm list -g --depth 0" listar de paquetes instalados globalmente
- paquete manejar fechas en js "npm install moment" --save necesario vivir en produccion -dev solo necesario en entorno local del proyecto
- se crea la carpeta la carpeta node_modules donde se alojaran los modulos que agregamos importante para que el proyecto funcione no enviarla ningun repositorio e ignorarla apenas se crea.Con archivo ".gitignore => node_modules/".
- en el archivo package.json se ve un alista de las dependencias.

//nuevas dependencias de forma distinta con flags en un proyecto
npm install moment
//desarrollo
npm install date-fns --save-dev >dependencias de desarrollo
npm i date-fns -D > tambien es un dependencia de desarrollo
npm i moment -S
npm install eslint -O de forma opcional

//de forma global
sudo npm install -g nodemon > nos permite generar un demonio que se encarga en escuchar algun cambio o valor, instalacion con permisos.

//flag que no estar instalada dentro del proyecto pero si el upack que nos hace (simulacion de instalacion)
npm install react --dry-run
//flag forsando la instalacion a que se desde el ultimo recurso del servidor de npm
npm install webpack -f (forsar desde la ultimo versiony desde servidores npm).
// npm install revisar el archivo de package y volver instalar cada una de las dependencias dentro del archivo.
//npm fund > proyectos que necesitan financiamiento.
//version
npm install json-server@"version"
npm install json-server@0.15.0

Actualizar y eliminar paquetes
==============================
- npm list > listar paquetes instalados dentro del proyecto
- npm outdate >ver paquete necesitan actulizacion
- npm outdate --dd > ver que sucede output detras ver todo el script en ejecucion, mas detallado
- npm update > de todos los paquetes actulizacion  y ouput de lo que sucede
- npm install "paquete@latest" > ultima version del paquete "npm install json-server@latest"
- desintalacion del paquete es con > npm uninstall "paquete"
- desintalar pero sin eliminarlo del package.json si del node__module
  npm uninstall webpack --no-save

Versionado semantico y "package.lock" (el uso los símbolos ^ y ~)
=====================================
- ^ > valor que establecemos en el versionado en la parte de cambios menores y en los parches
- ~ cambios establecidos dentro de pequeños parches.

Ejecutar tareas (scripts)
===============
son comandos que podemos establecer para poder ejecutar desde la consola, de forma nativa desde la terminal con npm run "nombre del script".
test > ejecuta tests es un alias para cualquier comando que se encuentre dentro de test.
start > inicializa el proyecto de forma local

Solución de problemas
=====================
Posibles errores :
npm run "nombre script" --dd > ver lo que esta sucediendo, estructura de los elementos
nos retorna un log al cometer un error
ELiminar el chache "npm cache clean --force" y "npm cache verify".
Archivo corrupto rm -rf "nombre_carpeta"
Comando de forma global para poder eliminar carpetas "sudo npm install -g rimraf" > rimraf "nombre carpeta"

Seguridad
=========
Herramienta  nos ayuda a ver al dia con la dependencias actulizadas Snyk 
- npm audit > nos permite auditar nuestro proyecto, detecta vulnerabilidades dentro de - un proyecto, errores, archivos maliciosos.
- npm audit --json > generar un documento con informacion mas detallada.
- npm update "paquete" --deth 2 > actulizacionde  del paquete nivel 2 
- npm audit fix > Comando nos ayuda a reparar todos los errores o vulnerabilidades del proyecto

Crear un paquete para NPM
=========================
- Ejecutar el comando para saber donde estoy ubicado
pwd
mkdir random-messages
cd random-messages/
git init
npm init

- Se crea el archivo index.js en la carpeta src
// Se declara el arreglo
const messages = [
    "David",
    "Diana",
    "Ana Maria",
    "Isabela",
    "Antonio",
    "Norma"
]

//Crear función para enviar aleatoriamente  los nombres del arreglo
const randomMsg = () => {
    const message = messages[Math.floor(Math.random()*messages.length)]
    console.log(message)
}

// Exportar como un módulo

module.exports = { randomMsg }

- Se debe crear una carpeta bin donde se crea ele archivo global.js (Configuración que se necesita)
#!/usr/bin/env node
// se va ejecutar dentro de bash

//Variable que llama la funcion que exportamos
let random = require('../src/index.js');

//Ejecuto la funcion
random.randomMsg();

- Modifico el package.json y coloco la configuración de bin que necesito
  "bin": {
    "random-msg": "./bin/global.js"
  },
  "preferGlobal": true


- sudo npm link > hace un referencia a este paquete hacia lo qu ele puede instalar de forma global

- Primero se debe probar de forma local.
pwd
sudo npm link
#Se ejecuta la función
random-msg

- Otra forma de instalar el paquete
sudo npm install -g ~/Estudio/GestionDeDependenciasYPaquetesConNPM/random-messages/

- Crear cuenta para poder subir el paquete - Npm.js https://www.npmjs.com/ Verificar la cuenta que llega al correo electrónico registrado.Se loguea a la cuenta creada por consola y se publica el paquete

npm adduser

npm publish

- Solución al error “403 Forbidden - PUT http://registry.npmjs.org/random-messages - You do not have permission to publish “random-messages”. Are you logged in as the correct user?”

En el archivo package.json cambiar el atributo name a un nombre original, puesto que el profe ya subió su repositorio con el nombre de random-messages, por lo que no podemos tener nosotros un proyecto del mismo nombre en NPM 😉.

Yo coloque random-messages-dbz y funciono.

Repaso del curso

Nuevo curso https://platzi.com/cursos/npm/
