# Adonisjs
Resumen de la documentación de Adonisjs

## Instalación
El cliente de adonisjs puede ser instalado por medio de gestor de paquetes de node
```bash
npm i -g @adonisjs/cli
```
Por medio del cual se creara el proyecto Full-stack en este framework usando el comando, pero si 
Solo se desea crear el proyecto Back-end puede usar la extensión `--api-only` ó `--api`
```bash
adonis new nombre-proyecto (--api-only/--api)
```
Con el proyecto ya creado se puede iniciar el servidor HTTP, estando dentro de la carpeta del proyecto
```bash
adonis serve --dev
```

## Configuración
### Proveedores de configuracion
Bajo la filosofía de desarrollo de Adonisjs, que comparte con otros frameworks como Laravel y Rails, el primer paso para 
desarrollar código sostenible es tener un directorio con las configuraciones realizadas a la aplicación.

Adonisjs hace uso del direcorio `./config`, donde almacenar todos los archivos de configuracion para que seran cargados al
momentos de iniciar la aplicación, el resultado de la configuracion de la aplicación con los estos archivos puede ser 
llamada por medio del metodo `use()`
```javascript
const Config = use('Config')
const appSecret = Config.get('app.file-name.key')
```
```javascript
// Ejemplo de archivo de configuración
{
  mysql: {
    host: '127.0.0.1',
  },
}

// Obtencion de la información
Config.get('database.mysql.host')
```
Si se desea cambiar la configuración de la aplicación cargada en memoria se puede hacer por medio del método .set()
```javascript
Config.set('database.mysql.host', 'db.example.com')
```

### Proveedores de entorno
Adonisjs permite tener diferentes configuraciones de la aplicación, dependiendo del entorno en el que se está ejecutando, haciendo
uso de la librería [dotenv](https://github.com/motdotla/dotenv)

La configuración de entorno de la aplicación se hará por medio del archivo `.env` del proyecto, allí se definirán las variables de entorno
necesarias para la ejecución de la aplicación con una estructura simple de `llave = valor`
```
APP_SECRET=F7op5n9vx1nAkno0DsNgZm5vjNXpOLIq
DB_HOST=127.0.0.1
DB_USER=root
```
Las variables de entorno de la aplicación pueden ser obtenidas como la configuración del mismo, siendo retornadas como `String`
```javascript
const Env = use('Env')
const appSecret = Env.get('APP_SECRET')
```
Si existe una variable de entorno que deba ser utilizada en la ejecución de la aplición se sugiere usar el método `Env.getOrFail()` el
cual retorna un error si la variable de entorno no existe
```javascript
const Env = use('Env')
// Retorna "Make sure to define APP_SECRET inside .env file."
Env.getOrFail('APP_SECRET')
```
En caso de necesitar cargar un archivo de entorno diferente se puede especificar el archivo deseado usando `ENV_PATH`
```bash
> ENV_PATH=/user/.env adonis serve
```
Si se desea declarar las variables de entorno dentro de la aplicación en vez de hacerlo en el archivo `.env` se debe usar `ENV_SILENCE`
```bash
> ENV_SILENT=true adonis serve
```
Para probar el archivo de entorno se puede debe declarar el `NODE_ENV` con `testing`, y el archivo `.env.testing` será cargado 
y sincronizado con el archivo `.env`

## Estructura de directorios

La estructura de directorios propuesta por Adonisjs al momento de crear un proyecto tiene esta forma con el fin de volver el codigo 
mas sostenible a medida que este crezca, separando los principales recursos de la aplicación de esta manera
```
├── app/
  ├── ...
├── config/
  ├── app.js
  ├── auth.js
  └── ...
├── database/
  ├── migrations/
  ├── seeds/
  └── factory.js
├── public/
├── resources/
  ├── ...
  └── views/
├── storage/
├── start/
  ├── app.js
  ├── kernel.js
  └── routes.js
├── test/
├── ace
├── server.js
└── package.json
```
### Directorios raiz
* `app`
Usado para el desarrollo de la logica de la aplicacion
* `config`
Usado para definir la configuracion de la aplicacion
* `databases`
Usado para almacenar todos los archivos relacionados con la base de datos
* `public`
Usado para almacenar todos los archivos expuesto por el servidor estatico HTTP
* `resources`
Usado para almacenar los archivos de presentacion de la aplicacion
* `start`
Usado para almacenar los archivos que seran cargados al iniciar la aplicacion
* `test`
Usado para almacenar todas las pruebas a la aplicación

### Directorios de la aplicación
* `app/Commands`
Usado para almacenar todos los [comandos](https://adonisjs.com/docs/4.1/ace) de la aplicación, creados con el comando `adonis make:command <nombre>`
* `app/Controllers`
  Usado para almacenar todos los [controladores](https://adonisjs.com/docs/4.1/controllers) de la aplicación, creados con el comando `adonis make:controller <nombre>`
* `app/Exceptions`
  Usado para almacenar el manejo de [excepciones](https://adonisjs.com/docs/4.0/exceptions) global y las personalizadas, creados con el comando 
  `adonis make:ehandler` or `adonis make:exception <name>`
* `app/Listeners`
  Usado para almacenar todos los [receptores de eventos](https://adonisjs.com/docs/4.1/events), creados con el comando `adonis make:listener <nombre>`
* `app/Middleware`
  Usado para almacenar todos los [middlewares](https://adonisjs.com/docs/4.1/middleware) de la aplicación, creados con el comando `adonis make:middleware <nombre>`
* `app/Models`
  Usado para almacenar todos los [modelos](https://adonisjs.com/docs/4.0/lucid) de la aplicación, creados con el comando `adonis make:model <nombre>`
* `app/Validators`
  Usado para almacenar todos los [validadores de rutas](https://adonisjs.com/docs/4.1/validator) de la aplicación, creados con el comando `adonis make:validator <name>`, es necesario instalar [Validator Provider](https://adonisjs.com/docs/4.1/validator)

## 
  
  
  
