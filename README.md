# Curso de Webpack 5

## Introducción a Webpack

### ¿Qué es webpack?

Es una herramienta para preparar el código para enviarlo a producción. Nos permite trabajar con JS, CSS, imagenes, fuentes, archivos estáticos. Nació en el 2012. Nos permites separar el código en distintos módulos.

### Conceptos básicos

Un paquete de módulos estáticos para JS moderno. Webpack mapea los distintos módulos para convertirlo todo en 1 o varios, según sea el caso. Podemos trabajar en modo de desarrollo, producción y recompilar archivos para visualizar los cambios. webpack dispone de loaders y plugins.

Con React podemos usar XML y HTML.

## Proyecto inicial

### Tu primer build con Webpack

-D = dependencia de desarrollo

Si no usamos `-g` no estamos instalando algo de manera global, solamente en el proyecto.

La carpeta "dist" es de "distribution"

`npx weback --mode development` configura el proyecto en modo desarrollo.
`npx weback --mode production` configura el proyecto en modo de producción. Esto optimiza el código.

### Instalación de Webpack y construcción del proyecto

Clonar el proyecto:

`git clone https://github.com/gndx/js-portfolio.git`

Instalar webpack con npm:

`npm install webpack webpack-cli -D`

### Configuración de webpack.config.js

En el archivo `webpack.config.js` vamos a escribir todas las configuraciones que tendrá nuestro proyecto. Prepararemos cuál es el punto de entrada, hacía a donde va nuestro proyecto, extensiones que usará, etc.

'dist' es un estándar dentro de la compilación de los proyectos.

En el archivo 'package.json' podemos crear los comandos que introduciremos en la terminal y específicar qué queremos que hagan.

## 3. Loaders y Plugins en Webpack

### Babel Loader para JS

Babel lo usamos para que JS moderno sea compatible entre todos los navegadores.

El archivo ".babelrc" no es visible para el usuario.

`/\.m?js$/` es una expresión regular que indica; los archivos que terminen con mjs o js

### HTML en Webpack

`"build": "webpack --mode production"` para modo de producción y minificado
`"dev": "webpack --mode development"` para modo de desarrollo y no minificado

### Loaders para CSS y preprocesadores de CSS

Tenemos que usar loaders de CSS para que webpack pueda entender estos archivos y trabajar con ellos.

`npm i mini-css-extract-plugin css-loader -D` para lograr esto.

Podemos hacer que webpack tambien entienda los prepocesadores de CSS:

`npm i stylus-loader -D` por ejemplo para stylus.

### Copia de archivos con Webpack

`npm i copy-webpack-plugin -D` nos servirá para copiar archivos y lanzarlos a la carpeta dist.

### Loaders de imágenes

Antes nuestro archivo de Template.js cargaba nuestras imágenes de manera estática.
Ahora podemos hacer un import para traerlas como los assets que son.

```javascript
import github from '../assets/images/github.png'
import twitter from '../assets/images/twitter.png'
import instagram from '../assets/images/instagram.png'

          <a href="https://twitter.com/gndx">
            <img src="${twitter}" />
          </a>
          <a href="https://github.com/gndx">
            <img src="${github}" />
          </a>
          <a href="https://instagram.com/gndx">
            <img src="${instagram}" />
          </a>
```

### Loaders de fuentes

Una de las mejores optimizaciones que podemos hacer cuando cargamos fuentes externas es incorporarlas a nuestro proyecto.

Con `@font-face` ya no hace falta que hagamos el `@import`.

Necesitamos copiar los archivos, usaremos `npm i url-loader file-loader -D`

### Optimización: hashes, compresión y minificación de archivos

webpack nos ayuda a optimizar nuestro proyecto minificando los archivos.

`npm i css-minimizer-webpack-plugin terser-webpack-plugin -D`

### Webpack Alias

Usamos alias para que cuando tengamos que mandar a llamar un archivo que se encuentra en una carpetea muy lejana, evitemos algo como `import ../../../`.

```javascript
alias: {
      '@utils': path.resolve(__dirname, 'src/utils/'),
      '@templates': path.resolve(__dirname, 'src/templates/'),
      '@styles': path.resolve(__dirname, 'src/styles/'),
      '@images': path.resolve(__dirname, 'src/assets/images/'),
    }
```

Así en vez de tener un directorio muy largo, tenemos:

```javascript
import getData from '@utils/getData.js';
import github from '@images/github.png'
```

## Deploy del proyecto

### Variables de entorno

Cuando el proyecto se hace más grande y otras personas van a trabajar en él, usamos estas variables que hacen referencia a un punto específico del proyecto.

En webpack usaremos `npm i dotenv-webpack -D`

Creamos un archivo `.env` y este NO se sube al repositorio.
Creamos un archivo `.env.example` que tendrá las variables vacías, este sí se puede subir al repositorio.

### Webpack en modo desarrollo

Creamos un archivo `webpack.config.dev.js` pero a este no le agregamos la parte de optimization.

### Webpack en modo producción

Usaremos un plugin de webpack para limpiar nuestro proyecto de archivos no necesarios, usando `npm i clean-webpack-plugin -D`

Así nuestros proyectos estarán listos para el modo de producción.

### Webpack Watch

Con la bandera `--watch` podemos hacer que webpack esté escuchando nuestros cambios y compile el proyecto cada vez que guardamos 1 archivo.

### Deploy a Netlify
