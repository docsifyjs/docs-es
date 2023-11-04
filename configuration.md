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

> **Nota** Si cambias [`routerMode`](#routermode) a `'history'`, es posible que desees configurar un alias para tus archivos `_sidebar.md` y `_navbar.md`.

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
