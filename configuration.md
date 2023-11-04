# Configuración

Puedes configurar Docsify definiendo `window.$docsify` como un objeto:

```html
<script>
  window.$docsify = {
    repo: 'docsifyjs/docsify',
    maxLevel: 3,
    coverpage: true,
  };
</script>
```

La configuración también se puede definir como una función, en cuyo caso el primer argumento es la instancia de Docsify `vm`. La función debe devolver un objeto de configuración. Esto puede ser útil para hacer referencia a `vm` en lugares como la configuración de Markdown:

```html
<script>
  window.$docsify = function (vm) {
    return {
      markdown: {
        renderer: {
          code(code, lang) {
            // ... usar `vm` ...
          },
        },
      },
    };
  };
</script>
```

## alias

- Tipo: `Object`

Establece el alias de la ruta. Puedes gestionar libremente las reglas de enrutamiento. Admite expresiones regulares.
¡Ten en cuenta que el orden es importante! Si una ruta puede coincidir con varios alias, el primero que hayas declarado tendrá prioridad.

```js
window.$docsify = {
  alias: {
    '/foo/(.*)': '/bar/$1', // admite expresiones regulares
    '/zh-cn/changelog': '/changelog',
    '/changelog':
      'https://raw.githubusercontent.com/docsifyjs/docsify/master/CHANGELOG',

    // Puede que necesites esto si usas `routerMode: 'history'`.
    '/.*/_sidebar.md': '/_sidebar.md', // Ver #301
  },
};
```

> **Nota** Si cambias [`routerMode`](/es/#routermode) a `'history'`, es posible que desees configurar un alias para tus archivos `_sidebar.md` y `_navbar.md`.

## auto2top

- Tipo: `Boolean`
- Predeterminado: `false`

Desplázate hasta la parte superior de la pantalla cuando cambie la ruta.

```js
window.$docsify = {
  auto2top: true,
};
```

## autoHeader

- Tipo: `Boolean`
- Predeterminado: `false`

Si tanto `loadSidebar` como `autoHeader` están habilitados, para cada enlace en `_sidebar.md`, agrega un encabezado a la página antes de convertirla a HTML. Ver [#78](https://github.com/docsifyjs/docsify/issues/78).

```js
window.$docsify = {
  loadSidebar: true,
  autoHeader: true,
};
```

## basePath

- Tipo: `String`

Ruta base del sitio web. Puedes configurarlo para que apunte a otro directorio o a otro nombre de dominio.

```js
window.$docsify = {
  basePath: '/ruta/',

  // Cargar archivos desde otro sitio
  basePath: 'https://docsify.js.org/',

  // Incluso puedes cargar archivos desde otros repositorios
  basePath:
    'https://raw.githubusercontent.com/ryanmcdermott/clean-code-javascript/master/',
};
```

## catchPluginErrors

- Tipo: `Boolean`
- Predeterminado: `true`

Determina si Docsify debe manejar automáticamente errores de complementos _síncronos_ no capturados. Esto puede evitar que los errores de los complementos afecten la capacidad de Docsify para renderizar correctamente el contenido del sitio en vivo.

## cornerExternalLinkTarget

- Tipo: `String`
- Predeterminado: `'_blank'`

Destino para abrir enlaces externos en la esquina superior derecha. Predeterminado `'_blank'` (nueva ventana/pestaña).

```js
window.$docsify = {
  cornerExternalLinkTarget: '_self', // predeterminado: '_blank'
};
```

## coverpage

- Tipo: `Boolean|String|String[]|Object`
- Predeterminado: `false`

Activa la [característica de portada](cover.md). Si es `true`, se cargará desde `_coverpage.md`.

```js
window.$docsify = {
  coverpage: true,

  // Nombre de archivo personalizado
  coverpage: 'cover.md',

  // Portadas múltiples
  coverpage: ['/', '/zh-cn/'],

  // Portadas múltiples y nombre de archivo personalizado
  coverpage: {
    '/': 'cover.md',
    '/zh-cn/': 'cover.md',
  },
};
```

## el

- Tipo: `String`
- Predeterminado: `'#app'`

Elemento del DOM en el que se montará la inicialización. Puede ser una cadena de selección CSS o un [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) real.

```js
window.$docsify = {
  el: '#app',
};
```

## executeScript

- Tipo: `Boolean`
- Predeterminado: `null`

Ejecuta el script en la página. Solo analiza la primera etiqueta de script ([demo](themes)). Si se detecta Vue, esto es `true` de forma predeterminada.

```js
window.$docsify = {
  executeScript: true,
};
```

```markdown
## Esto es una prueba

<script>
  console.log(2333)
</script>
```

Ten en cuenta que si estás ejecutando un script externo, por ejemplo, una demostración de jsfiddle incrustada, asegúrate de incluir el complemento [external-script](plugins.md?id=external-script).

## ext

- Tipo: `String`
- Predeterminado: `'.md'`

Extensión de archivo solicitada.

```js
window.$docsify = {
  ext: '.md',
};
```

## externalLinkRel

- Tipo: `String`
- Predeterminado: `'noopener'`

El valor predeterminado es `'noopener'` (sin abridor), lo que evita que la página externa recién abierta (cuando [externalLinkTarget](/es/#externallinktarget) es `'_blank'`) tenga la capacidad de controlar nuestra página. No se establece ningún atributo `rel` cuando no es `'_blank'`. Consulta [esta publicación](https://mathiasbynens.github.io/rel-noopener/) para obtener más información sobre por qué es posible que desees usar esta opción.

```js
window.$docsify = {
  externalLinkRel: '', // predeterminado: 'noopener'
};
```

## externalLinkTarget

- Tipo: `String`
- Predeterminado: `'_blank'`

Destino para abrir enlaces externos dentro del markdown. Predeterminado `'_blank'` (nueva ventana/pestaña).

```js
window.$docsify = {
  externalLinkTarget: '_self', // predeterminado: '_blank'
};
```

## fallbackLanguages

- Tipo: `Array<string>`

Lista de idiomas que se utilizarán como alternativa al idioma predeterminado cuando se solicite una página y no exista para el idioma especificado.

Ejemplo:

- Intenta obtener la página `/de/overview`. Si existe, se mostrará.
- Luego, intenta obtener la página predeterminada `/overview` (dependiendo del idioma predeterminado). Si existe, se mostrará.
- Finalmente, muestra la página 404.

```js
window.$docsify = {
  fallbackLanguages: ['fr', 'de'],
};
```

## formatUpdated

- Tipo: `String|Function`

Podemos mostrar la fecha de actualización del archivo a través de la variable **{docsify-updated<span>}</span>** y darle formato con `formatUpdated`. Consulta https://github.com/lukeed/tinydate#patterns

```js
window.$docsify = {
  formatUpdated: '{MM}/{DD} {HH}:{mm}',

  formatUpdated(time) {
    // ...

    return time;
  },
};
```

## hideSidebar

- Tipo: `Boolean`
- Predeterminado: `true`

Esta opción ocultará completamente la barra lateral y no representará ningún contenido en el lado.

```js
window.$docsify = {
  hideSidebar: true,
};
```

## homepage

- Tipo: `String`
- Predeterminado: `'README.md'`

`README.md` en la carpeta de tus documentos se tratará como la página de inicio de tu sitio web, pero a veces es posible que desees servir otro archivo como tu página de inicio.

```js
window.$docsify = {
  // Cambia a /home.md
  homepage: 'home.md',

  // O utiliza el readme en tu repositorio
  homepage:
    'https://raw.githubusercontent.com/docsifyjs/docsify/master/README.md',
};
```

## loadNavbar

- Tipo: `Boolean|String`
- Predeterminado: `false`

Carga la barra de navegación desde el archivo Markdown `_navbar.md` si es **true**, de lo contrario, cárgala desde la ruta especificada.

```js
window.$docsify = {
  // Cargar desde _navbar.md
  loadNavbar: true,

  // Cargar desde nav.md
  loadNavbar: 'nav.md',
};
```

## loadSidebar

- Tipo: `Boolean|String`
- Predeterminado: `false`

Carga la barra lateral desde el archivo Markdown `_sidebar.md` si es **true**, de lo contrario, cárgala desde la ruta especificada.

```js
window.$docsify = {
  // Cargar desde _sidebar.md
  loadSidebar: true,

  // Cargar desde summary.md
  loadSidebar: 'summary.md',
};
```

## logo

- Tipo: `String`

Logotipo del sitio web tal como aparece en la barra lateral. Puedes cambiar su tamaño usando CSS.

```js
window.$docsify = {
  logo: '/_media/icon.svg',
};
```

## markdown

- Tipo: `Function`

Consulta [Configuración de Markdown](markdown.md).

```js
window.$docsify = {
  // objeto
  markdown: {
    smartypants: true,
    renderer: {
      link() {
        // ...
      },
    },
  },

  // función
  markdown(marked, renderer) {
    // ...
    return marked;
  },
};
```

## maxLevel

- Tipo: `Número`
- Predeterminado: `6`

Nivel máximo de la tabla de contenido.

```js
window.$docsify = {
  maxLevel: 4,
};
```

## mergeNavbar

- Tipo: `Boolean`
- Predeterminado: `false`

La barra de navegación se fusionará con la barra lateral en pantallas más pequeñas.

```js
window.$docsify = {
  mergeNavbar: true,
};
```

## name

- Tipo: `String`

Nombre del sitio web tal como aparece en la barra lateral.

```js
window.$docsify = {
  name: 'docsify',
};
```

El campo del nombre también puede contener HTML personalizado para facilitar la personalización:

```js
window.$docsify = {
  name: '<span>docsify</span>',
};
```

## nameLink

- Tipo: `String`
- Predeterminado: `'window.location.pathname'`

La URL a la que enlaza el `nombre` del sitio web.

```js
window.$docsify = {
  nameLink: '/',

  // Para cada ruta
  nameLink: {
    '/zh-cn/': '#/zh-cn/',
    '/': '#/',
  },
};
```

## nativeEmoji

- Tipo: `Boolean`
- Predeterminado: `false`

Renderiza códigos abreviados de emoji utilizando imágenes de emoji estilo GitHub o caracteres de emoji nativos de la plataforma.

```js
window.$docsify = {
  nativeEmoji: true,
};
```

```markdown
:smile:
:partying_face:
:joy:
:+1:
:-1:
```

Imágenes de estilo GitHub cuando es `false`:

<output data-lang="output">
  <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/unicode/1f604.png" alt="smile">
  <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/unicode/1f973.png" alt="partying_face">
  <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/unicode/1f602.png" alt="joy">
  <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/unicode/1f44d.png" alt="+1">
  <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/unicode/1f44e.png" alt="-1">
</output>

Caracteres nativos de la plataforma cuando es `true`:

<output data-lang="output">
  <span class="emoji">😄︎</span>
  <span class="emoji">🥳︎</span>
  <span class="emoji">😂︎</span>
  <span class "emoji">👍︎</span>
  <span class="emoji">👎︎</span>
</output>

Para representar códigos abreviados como texto, reemplaza los caracteres `:` con la entidad HTML `&colon;`.

```markdown
&colon;100&colon;
```

<output data-lang="output">

&colon;100&colon;

</output>

## noCompileLinks

- Tipo: `Array<string>`

A veces no queremos que Docsify maneje nuestros enlaces. Consulta [#203](https://github.com/docsifyjs/docsify/issues/203). Podemos omitir la compilación de ciertos enlaces especificando un array de cadenas. Cada cadena se convierte en una expresión regular (`RegExp`) y se compara con _todo_ el atributo href de un enlace.

```js
window.$docsify = {
  noCompileLinks: ['/foo', '/bar/.*'],
};
```

## noEmoji

- Tipo: `Boolean`
- Predeterminado: `false`

Desactiva el análisis de emoji y representa todos los códigos abreviados de emoji como texto.

```js
window.$docsify = {
  noEmoji: true,
};
```

```markdown
:100:
```

<output data-lang="output">

&colon;100&colon;

</output>

Para deshabilitar el análisis de emoji de códigos abreviados individuales, reemplaza los caracteres `:` por la entidad HTML `&colon;`.

```markdown
:100:

&colon;100&colon;
```

<output data-lang="output">

:100:

&colon;100&colon;

</output>

## notFoundPage

- Tipo: `Boolean` | `String` | `Object`
- Predeterminado: `false`

Muestra el mensaje predeterminado de "404 - No encontrado":

```js
window.$docsify = {
  notFoundPage: false,
};
```

Carga el archivo `_404.md`:

```js
window.$docsify = {
  notFoundPage: true,
};
```

Carga la ruta personalizada de la página 404:

```js
window.$docsify = {
  notFoundPage: 'mi404.md',
};
```

Carga la página 404 adecuada según la localización:

```js
window.$docsify = {
  notFoundPage: {
    '/': '_404.md',
    '/de': 'de/_404.md',
  },
};
```

> Nota: Las opciones para fallbackLanguages no funcionan con las opciones de `notFoundPage`.

## onlyCover

- Tipo: `Boolean`
- Predeterminado: `false`

Solo se carga la portada al visitar la página de inicio.

```js
window.$docsify = {
  onlyCover: false,
};
```

## relativePath

- Tipo: `Boolean`
- Predeterminado: `false`

Si está **habilitado**, los enlaces son relativos al contexto actual.

Por ejemplo, la estructura de directorios es la siguiente:

```text
.
└── docs
    ├── README.md
    ├── guide.md
    └── zh-cn
        ├── README.md
        ├── guide.md
        └── config
            └── example.md
```

Con la ruta relativa **habilitada** y la URL actual `http://domain.com/zh-cn/README`, los enlaces proporcionados se resolverán como sigue:

```text
guide.md              => http://domain.com/zh-cn/guide
config/example.md     => http://domain.com/zh-cn/config/example
../README.md          => http://domain.com/README
/README.md            => http://domain.com/README
```

```js
window.$docsify = {
  // Ruta relativa habilitada
  relativePath: true,

  // Ruta relativa deshabilitada (valor predeterminado)
  relativePath: false,
};
```

## repo

- Tipo: `String`

Configura la URL del repositorio o una cadena en el formato `nombreDeUsuario/repositorio` para agregar el widget de [GitHub Corner](http://tholman.com/github-corners/) en la esquina superior derecha del sitio.

```js
window.$docsify = {
  repo: 'docsifyjs/docsify',
  // o
  repo: 'https://github.com/docsifyjs/docsify/',
};
```

## requestHeaders

- Tipo: `Object`

Establece las cabeceras de la solicitud de recursos.

```js
window.$docsify = {
  requestHeaders: {
    'x-token': 'xxx',
  },
};
```

Como configurar la caché

```js
window.$docsify = {
  requestHeaders: {
    'cache-control': 'max-age=600',
  },
};
```

## routerMode

Configura el formato de URL que utilizarán las rutas de tu sitio.

- Tipo: `String`
- Predeterminado: `'hash'`

```js
window.$docsify = {
  routerMode: 'history', // predeterminado: 'hash'
};
```

Para sitios desplegados estáticamente (por ejemplo, en GitHub Pages), el enrutamiento basado en hash es más sencillo de configurar. Para sitios web que pueden reescribir URL, el formato basado en historial es mejor (especialmente para la optimización de motores de búsqueda, ya que el enrutamiento basado en hash no es tan amigable para los motores de búsqueda).

El enrutamiento basado en hash significa que todos los caminos de URL estarán precedidos por `/#/` en la barra de direcciones. Esto es un truco que permite al sitio cargar `/index.html`, luego utiliza el camino que sigue al `#` para determinar qué archivos de Markdown cargar. Por ejemplo, una URL completa basada en hash podría verse así: `https://example.com/#/ruta/a/página`. El navegador cargará realmente `https://example.com` (suponiendo que tu servidor está sirviendo `index.html` de forma predeterminada, como la mayoría), y luego el código JavaScript de Docsify analizará el `/#/...` y determinará el archivo de Markdown a cargar y renderizar. Además, al hacer clic en un enlace, el enrutador de Docsify cambiará dinámicamente el contenido después del hash. El valor de `location.pathname` seguirá siendo `/` independientemente. Las partes de un camino de hash no se envían al servidor al visitar una URL de este tipo en un navegador.

Por otro lado, el enrutamiento basado en historial significa que el código JavaScript de Docsify utilizará la [API de Historial](https://developer.mozilla.org/es/docs/Web/API/History_API) para cambiar dinámicamente la URL sin usar un `#`. Esto significa que todas las URL se considerarán "reales" para los motores de búsqueda, y se enviará la ruta completa al servidor al visitar la URL en tu navegador. Por ejemplo, una URL podría verse como `https://example.com/ruta/a/página`. El navegador intentará cargar esa URL completa directamente desde el servidor, no solo `https://example.com`. La ventaja de esto es que estos tipos de URL son mucho más amigables para los motores de búsqueda y se pueden indexar. La desventaja, sin embargo, es que tu servidor, o el lugar donde alojas los archivos de tu sitio, debe ser capaz de manejar estas URL. Varios servicios de alojamiento de sitios web estáticos permiten configurar "reglas de reescritura", de modo que un servidor se pueda configurar para siempre enviar `/index.html` sin importar qué ruta se visite. El valor de `location.pathname` mostrará `/ruta/a/página`, ya que realmente se envió al servidor.

Resumiendo: comienza con el enrutamiento basado en `hash` (el predeterminado). Si te sientes aventurero, aprende a configurar un servidor y luego cambia al modo `history` para obtener una mejor experiencia sin el `#` en la URL y optimización de SEO.

> **Nota** Si usas `routerMode: 'history'`, es posible que desees agregar un [`alias`](/es/#alias) para que tus archivos `_sidebar.md` y `_navbar.md` siempre se carguen sin importar qué ruta se esté visitando.
>
> ```js
> window.$docsify = {
>   routerMode: 'history',
>   alias: {
>     '/.*/_sidebar.md': '/_sidebar.md',
>     '/.*/_navbar.md': '/_navbar.md',
>   },
> };
> ```

## routes

- Tipo: `Object`

Define rutas "virtuales" que pueden proporcionar contenido dinámicamente. Una ruta es una correspondencia entre la ruta esperada, ya sea una cadena o una función. Si el valor mapeado es una cadena, se trata como Markdown y se analiza en consecuencia. Si es una función, se espera que devuelva contenido en formato Markdown.

Una función de ruta recibe hasta tres parámetros:

1. `ruta` - la ruta de la ruta solicitada (por ejemplo, `/bar/baz`).
2. `coincidido` - la matriz de coincidencia de expresiones regulares [`RegExpMatchArray`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/String/match) que coincidió con la ruta (por ejemplo, para `/bar/(.+)`, obtienes `['/bar/baz', 'baz']`).
3. `siguiente` - esta es una devolución de llamada que puedes llamar cuando tu función de ruta es asíncrona.

¡Ten en cuenta que el orden importa! Las rutas se emparejan en el mismo orden en el que las declaras, lo que significa que en casos de rutas superpuestas, es posible que desees listar primero las más específicas.

```js
window.$docsify = {
  routes: {
    // Coincidencia básica con retorno de cadena
    '/foo': '# Markdown personalizado',

    // Coincidencia con expresión regular con función síncrona
    '/bar/(.*)'(ruta, coincidido) {
      return '# Markdown personalizado';
    },

    // Coincidencia con expresión regular con función asíncrona
    '/baz/(.*)'(ruta, coincidido, siguiente) {
      fetch('/api/users?id=12345')
        .then(response => {
          siguiente('# Markdown personalizado');
        })
        .catch(err => {
          // Manejar error...
        });
    },
  },
};
```

Además de cadenas, las funciones de ruta pueden devolver un valor falso (`null` \ `undefined`) para indicar que ignoran la solicitud actual:

```js
window.$docsify = {
  routes: {
    // Acepta todo excepto perros (síncrono)
    '/mascotas/(.+)'(ruta, coincidido) {
      if (coincidido[0] === 'perros') {
        return null;
      } else {
        return 'Me gustan todas las mascotas excepto los perros';
      }
    }

    // Acepta todo excepto gatos (asíncrono)
    '/mascotas/(.*)'(ruta, coincidido, siguiente) {
      if (coincidido[0] === 'gatos') {
        siguiente();
      } else {
        // Tareas asíncronas...
        siguiente('Me gustan todas las mascotas excepto los gatos');
      }
    }
  }
}
```

Finalmente, si tienes una ruta específica que tiene un archivo de Markdown real (y, por lo tanto, no debe coincidir con tu ruta), puedes excluirlo devolviendo explícitamente un valor `false`:

```js
window.$docsify = {
  routes: {
    // Si buscas /mascotas/gatos, Docsify omitirá todas las rutas y buscará "mascotas/gatos.md"
    '/mascotas/gatos'(ruta, coincidido) {
      return false;
    }

    // Pero cualquier otra mascota debería generar contenido dinámico justo aquí
    '/mascotas/(.+)'(ruta, coincidido) {
      const mascota = coincidido[0];
      return `tu mascota es ${mascota} (pero no un gato)`;
    }
  }
}
```

## subMaxLevel

- Tipo: `Number`
- Predeterminado: `0`

Agrega una tabla de contenido (TOC) en la barra lateral personalizada.

```js
window.$docsify = {
  subMaxLevel: 2,
};
```

Si tienes un enlace a la página de inicio en la barra lateral y deseas que se muestre como activo al acceder a la URL raíz, asegúrate de actualizar tu barra lateral en consecuencia:

```markdown
- Barra lateral
  - [Inicio](/)
  - [Otra página](otra.md)
```

Para obtener más detalles, consulta [#1131](https://github.com/docsifyjs/docsify/issues/1131).

## themeColor (_desaprobado_)

> **Advertencia** Desaprobado. Usa la variable CSS `--theme-color` en tu hoja de estilo `<style>`. Ejemplo:
>
> ```html
> <style>
>   :root {
>     --theme-color: deeppink;
>   }
> </style>
> ```

- Tipo: `String`

Personaliza el color del tema.

```js
window.$docsify = {
  themeColor: '#3F51B5',
};
```

## topMargin

- Tipo: `Number`
- Predeterminado: `0`

Añade espacio en la parte superior al desplazarte por la página de contenido para llegar a la sección seleccionada. Esto es útil en caso de que tengas un diseño de "enc

abezado fijo" y desees alinear los anclajes con el final de tu encabezado.

```js
window.$docsify = {
  topMargin: 90, // predeterminado: 0
};
```

## vueComponents

- Tipo: `Object`

Crea y registra [componentes globales de Vue](https://vuejs.org/v2/guide/components.html). Los componentes se especifican utilizando el nombre del componente como clave con un objeto que contiene opciones de Vue como valor. Los datos del componente son únicos para cada instancia y no persistirán a medida que los usuarios navegan por el sitio.

```js
window.$docsify = {
  vueComponents: {
    'contador-botón': {
      template: `
        <button @click="count += 1">
          Me has clicado {{ count }} veces
        </button>
      `,
      data() {
        return {
          count: 0,
        };
      },
    },
  },
};
```

```markdown
<contador-botón></contador-botón>
```

<output data-lang="output">
  <contador-botón></contador-botón>
</output>

## vueGlobalOptions

- Tipo: `Object`

Especifica [opciones de Vue](https://vuejs.org/v2/api/#Options-Data) para su uso con contenido de Vue que no se monta explícitamente con [vueMounts](/es/#montar-elementos-dom), [vueComponents](/es/#componentes) o un [script de Markdown](/es/#script-de-markdown). Los cambios en los datos globales se mantendrán y se reflejarán en cualquier lugar donde se utilicen referencias globales.

```js
window.$docsify = {
  vueGlobalOptions: {
    data() {
      return {
        count: 0,
      };
    },
  },
};
```

```markdown
<p>
  <button @click="count -= 1">-</button>
  {{ count }}
  <button @click="count += 1">+</button>
</p>
```

<output data-lang="output">
  <p>
    <button @click="count -= 1">-</button>
    {{ count }}
    <button @click="count += 1">+</button>
  </p>
</output>

## vueMounts

- Tipo: `Object`

Especifica elementos DOM que se montarán como [instancias de Vue](https://vuejs.org/v2/guide/instance.html) y sus opciones asociadas. Los elementos de montaje se especifican utilizando un [selector CSS](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Selectors) como clave con un objeto que contiene opciones de Vue como valor. Docsify montará el primer elemento coincidente en el área de contenido principal cada vez que se cargue una nueva página. Los datos del elemento de montaje son únicos para cada instancia y no persistirán a medida que los usuarios navegan por el sitio.

```js
window.$docsify = {
  vueMounts: {
    '#contador': {
      data() {
        return {
          count: 0,
        };
      },
    },
  },
};
```

```markdown
<div id="contador">
  <button @click="count -= 1">-</button>
  {{ count }}
  <button @click="count += 1">+</button>
</div>
```

<output id="contador">
  <button @click="count -= 1">-</button>
  {{ count }}
  <button @click="count += 1">+</button>
</output>
