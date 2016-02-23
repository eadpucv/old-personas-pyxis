# personas-pyxis
http://eadpucv.github.io/personas-pyxis/

[`Personas e[ad]`](http://personas.ead.pucv.cl) es un sistema digital de registro único (Single Sing-on), desarrollado por el `.:TIG:.` Taller de Investigaciones Gráficas de la `e[ad]`, que permite la creación de un usuario único llamado "persona", para el uso de algunos servicios digitales que ofrece la `e[ad] Escuela de Arquitectura y Diseño`

# personas-pyxis
http://eadpucv.github.io/personas-pyxis/

[`Personas e[ad]`](http://personas.ead.pucv.cl) es un sistema digital de registro único (Single Sing-on), desarrollado por el `.:TIG:.` Taller de Investigaciones Gráficas de la `e[ad]`, que permite la creación de un usuario único llamado "persona", para el uso de algunos servicios digitales que ofrece la `e[ad] Escuela de Arquitectura y Diseño`

## Compilación de estilos con gruntJS

El repositorio utiliza Pyxis como una dependencia importante, quien a su vez integra Stampa y jQuery. Los estilos custom de este repositorio deben convivir de manera inteligente, paralelamente con las dependencias. Para eso es necesario compilar todos los estilos y así generar una hoja de estilos única. Para llevar acabo esto, se utiliza grunt, herramienta encargada de correr las tareas de forma automática y así permitir un desarrollo mucho más fluido. 

El proceso de instalación es el siguiente:

1. Abrir la consola (terminal) y posicionarse en el directorio central del repositorio
2. Ejecutar: `npm install -g grunt-cli` para descargar el cliente de gruntJS
3. Configurar el archivo `package.json`, quien será el encargado de enlistar las dependencias de node. Esto es equivalente al manejo de paquetes utilizado por bower. Acá deben incluirse las tareas necesarias. En esta ocasión se utilizará el compilador de LESS y un WATCH, quien vigilará nuestros archivos. Para instalar estos módulos y guardarlos directamente en nuestro `package.json`, debemos introducir las siguientes líneas de código en el terminal:
4. `npm install grunt-contrib-less --save` y `npm install grunt-contrib-watch --save`. Un ejemplo básico se adjunta al final de esta guía.
5. Las tareas que grunt va a correr, deben ser declaradas en un archivo llamado `Gruntfile.js`. Un ejemplo básico se adjunta al final de esta guía:
6. Finalmente, en el terminal introducimos el nombre de nuestra tarea, que en este caso podría ser tanto `grunt watch` como `grunt` por defecto. Esto levantará nuestra tarea automática y cada vez que realicemos un cambio en los archivos LESS, los estilos se recompilarán automáticamente.


### Modelo básico de package.json

```
{
  "name": "my-project-name",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.5",
    "grunt-contrib-jshint": "~0.10.0",
    "grunt-contrib-nodeunit": "~0.4.1",
    "grunt-contrib-uglify": "~0.5.0"
  }
}
```

### Modelo básico de Gruntfile.js

```
module.exports = function(grunt){
    grunt.initConfig({
      watch: {
          styles: {
              files: ['assets/less/*.less'], // Observa los archivos LESS
              tasks: ['less'],
              options: {
                  livereload: true,
              }
          },
          html: {
            files: ['html/*.html' ] // Observa los archivos HTML
          }
      },
      less: {                              // Task
        dist: {                            // Target
          files: {                         // Dictionary of files
            "assets/css/personas.css": "assets/less/personas.less" // 'destination': 'source'
          }
        }
      }
    });

    // Carga modulos adicionales de grunt
    grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.loadNpmTasks('grunt-contrib-less');
    // Define tareas
    grunt.registerTask('default', [
      'watch:styles'
      ]);
};
```
La estructura de código es bastante legible, donde se distingue que `watch` observa todos los archivos de extensión `less` dentro de `assets/less/`, quien luego ejecturá la tarea `less`, quien a su vez, va a buscar la fuente, nuestro compilador de estilos, ubicado en `assets/less/personas.less` y su destino compilado se declara en `assets/css/personas.css`. Incluso se pueden incluir más módulos como para levantar un ambiente de servidor local, sin embargo mantendremos este proceso lo más simple posible.
