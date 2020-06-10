# Configuración

!> Este archivo está traducido parcialmente, por favor edita el documento y ayuda con la traducción del mismo.

Puedes configurar el `window.$docsify`.

```html
<script>
  window.$docsify = {
    repo: 'tu-repo/docs',
    maxLevel: 3,
    coverpage: true
  }
</script>
```

## el

- Type: `String`
- Default: `#app`

El elemento DOM que se montará en la inicialización. Puede ser una cadena de selector CSS o un elemento HTML real.

```js
window.$docsify = {
  el: '#app'
};
```

## repo

- Type: `String`
- Default: `null`

Configure la url del repositorio o una cadena de nombre de `username/repo` para agregar el widget de [esquina GitHub](http://tholman.com/github-corners/) en la esquina superior derecha del sitio.

```js
window.$docsify = {
  repo: 'tu-repo/docs',
  // or
  repo: 'https://github.com/tu-repo/docs/'
};
```

## maxLevel

- Type: `Number`
- Default: `6`

Máximo de tablas por nivel de contenido.

```js
window.$docsify = {
  maxLevel: 4
};
```

## loadNavbar

- Type: `Boolean|String`
- Default: `false`

Carga la barra de navegación desde el archivo Markdown `_navbar.md` si es **verdadero** o bien desde la ruta especificada.

```js
window.$docsify = {
  // carga desde _navbar.md
  loadNavbar: true,

  // carga desde nav.md
  loadNavbar: 'nav.md'
};
```

## loadSidebar

- Type: `Boolean|String`
- Default: `false`

Carga la barra lateral desde el archivo Markdown `_sidebar.md` si es **verdadero** o bien desde la ruta especificada.

```js
window.$docsify = {
  // carga desde _sidebar.md
  loadSidebar: true,

  // carga desde summary.md
  loadSidebar: 'summary.md'
};
```

## subMaxLevel

- Type: `Number`
- Default: `0`

Agregar tabla de contenido (TOC) en la barra lateral personalizada.

```js
window.$docsify = {
  subMaxLevel: 2
};
```

## auto2top

- Type: `Boolean`
- Default: `false`

Se desplaza a la parte superior de la pantalla cuando se cambia la ruta.

```js
window.$docsify = {
  auto2top: true
};
```

## homepage

- Type: `String`
- Default: `README.md`

`README.md` en su carpeta de documentos se tratará como la página de inicio de su sitio web pero a veces puede que necesite publicar otro archivo como su página de inicio.

```js
window.$docsify = {
  // Cambia a /home.md
  homepage: 'home.md',

  // O use el archivo README en su repositorio
  homepage:
    'https://raw.githubusercontent.com/tu-repo/docs/master/README.md'
};
```

## basePath

- Type: `String`

Ruta base del sitio web. Puede configurarlo en otro directorio u otro nombre del dominio.

```js
window.$docsify = {
  basePath: '/path/',

  // Carga los archivos de otro sitio
  basePath: 'https://docsify.js.org/',

  // Incluso puede cargar archivos de otro repositorio
  basePath:
    'https://raw.githubusercontent.com/ryanmcdermott/clean-code-javascript/master/'
};
```

## coverpage

- Type: `Boolean|String|String[]|Object`
- Default: `false`

Active la [cover feature](/es/cover.md). Si es verdadero, se cargará desde `_coverpage.md`

```js
window.$docsify = {
  coverpage: true,

  // Nombre del archivo personalizado
  coverpage: 'cover.md',

  // cubiertas múltiples
  coverpage: ['/', '/zh-cn/'],

  // múltiples portadas y nombre de archivo personalizado
  coverpage: {
    '/': 'cover.md',
    '/zh-cn/': 'cover.md'
  }
};
```

## logo

- Type: `String`

Logotipo del sitio web tal como aparece en la barra lateral, puede cambiar el tamaño por CSS.

```js
window.$docsify = {
  logo: '/_media/icon.svg'
};
```

## name

- Type: `String`

Nombre del sitio web tal como aparece en la barra lateral.

```js
window.$docsify = {
  name: 'docsify'
};
```

## nameLink

- Type: `String`
- Default: `window.location.pathname`

El nombre del enlace.

```js
window.$docsify = {
  nameLink: '/',

  // For each route
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/': '/'
  }
};
```

## markdown

- Type: `Function`

Ver la [configuración de Markdown](/es/markdown.md).

```js
window.$docsify = {
  // object
  markdown: {
    smartypants: true,
    renderer: {
      link: function() {
        // ...
      }
    }
  },

  // function
  markdown: function(marked, renderer) {
    // ...
    return marked;
  }
};
```

## themeColor

- Type: `String`

Personaliza el color del diseño. Use [variables CSS3](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables) y polyfill en navegadores antiguos.

```js
window.$docsify = {
  themeColor: '#3F51B5'
};
```

## alias

- Type: `Object`

Establezca el alias de la ruta. Puede gestionar libremente las reglas de enrutamiento. Admite RegExp.

```js
window.$docsify = {
  alias: {
    '/foo/(+*)': '/bar/$1', // supports regexp
    '/zh-cn/changelog': '/changelog',
    '/changelog':
      'https://raw.githubusercontent.com/docsifyjs/docsify/master/CHANGELOG',
    '/.*/_sidebar.md': '/_sidebar.md' // See #301
  }
};
```

## autoHeader

- type: `Boolean`

Si `loadSidebar` y `autoHeader` están habilitados (ambos), por cada enlace en el `_sidebar.md`, anteponer un encabezado a la página antes de convertirlo a html. Comparar [#78](https://github.com/docsify/docsify/issues/78).

```js
window.$docsify = {
  loadSidebar: true,
  autoHeader: true
};
```

## executeScript

- type: `Boolean`

Ejecute la secuencia de comandos en la página. Solo analizar la primera etiqueta de secuencia de comandos ([Ver demo](/es/themes)). Si  Vue está presente, se habilita por defecto.

```js
window.$docsify = {
  executeScript: true
};
```

```markdown
## This is test

<script>
  console.log(2333)
</script>
```

Tenga en cuenta que si está ejecutando un script externo, por ejemplo una demostración jsfiddle integrada, asegúrese de incluir el  plugin [script externo](/es/plugins.md?id=external-script).

## noEmoji

- type: `Boolean`

Deshabilitaría el parseo de emojis.

```js
window.$docsify = {
  noEmoji: true
};
```

## mergeNavbar

- type: `Boolean`

Navbar se combinará con la barra lateral en pantallas más pequeñas.

```js
window.$docsify = {
  mergeNavbar: true
};
```

## formatUpdated

- type: `String|Function`

We can display the file update date through **{docsify-updated<span>}</span>** variable. And format it by `formatUpdated`.
See https://github.com/lukeed/tinydate#patterns

```js
window.$docsify = {
  formatUpdated: '{MM}/{DD} {HH}:{mm}',

  formatUpdated: function(time) {
    // ...

    return time;
  }
};
```

## externalLinkTarget

- type: `String`
- default: `_blank`

Target to open external links. Default `'_blank'` (new window/tab)

```js
window.$docsify = {
  externalLinkTarget: '_self' // default: '_blank'
};
```

## routerMode

- type: `String`
- default: `hash`

```js
window.$docsify = {
  routerMode: 'history' // default: 'hash'
};
```

## noCompileLinks

- type: `Array`

A veces no queremos que docsify maneje nuestros enlaces. Ver [#203](https://github.com/docsifyjs/docsify/issues/203)

```js
window.$docsify = {
  noCompileLinks: ['/foo', '/bar/.*']
};
```

## onlyCover

- type: `Boolean`

Solo la coverpage se carga cuando visitan la página principal (el home).

```js
window.$docsify = {
  onlyCover: false
};
```

## requestHeaders

- type: `Object`

Set the request resource headers.

```js
window.$docsify = {
  requestHeaders: {
    'x-token': 'xxx'
  }
};
```

## ext

- type: `String`

Request file extension.

```js
window.$docsify = {
  ext: '.md'
};
```

## fallbackLanguages

- type: `Array<string>`

List of languages that will fallback to the default language when a page is request and didn't exists for the given local.

Example:

- try to fetch the page of `/de/overview`. If this page exists, it'll be displayed
- then try to fetch the default page `/overview` (depending on the default language). If this page exists, it'll be displayed
- then display 404 page.

```js
window.$docsify = {
  fallbackLanguages: ['fr', 'de']
};
```

## notFoundPage

- type: `Boolean` | `String` | `Object`

Load the `_404.md` file:

```js
window.$docsify = {
  notFoundPage: true
};
```

Load the customised path of the 404 page:

```js
window.$docsify = {
  notFoundPage: 'my404.md'
};
```

Load the right 404 page according to the localisation:

```js
window.$docsify = {
  notFoundPage: {
    '/': '_404.md',
    '/de': 'de/_404.md',
  }
};
```

> Note: The options with fallbackLanguages didn't work with the `notFoundPage` options.
