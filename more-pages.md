# Más páginas

Si necesitas más páginas, simplemente puedes crear más archivos Markdown en tu directorio de Docsify. Si creas un archivo llamado `guide.md`, entonces se accede a él mediante `/#/guide`.

Por ejemplo, la estructura del directorio es la siguiente:

```text
.
└── docs
    ├── README.md
    ├── guide.md
    └── zh-cn
        ├── README.md
        └── guide.md
```

Rutas correspondientes

```text
docs/README.md        => http://dominio.com
docs/guide.md         => http://dominio.com/#/guide
docs/zh-cn/README.md  => http://dominio.com/#/zh-cn/
docs/zh-cn/guide.md   => http://dominio.com/#/zh-cn/guide
```

## Barra lateral

Para tener una barra lateral, puedes crear tu propio `_sidebar.md` (consulta [la barra lateral de esta documentación](https://github.com/docsifyjs/docsify/blob/master/docs/_sidebar.md) para un ejemplo):

Primero, debes establecer `loadSidebar` en **true**. Los detalles están disponibles en el [párrafo de configuración](/es/configuration.md#loadsidebar).

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

Crea el `_sidebar.md`:

```markdown
<!-- docs/_sidebar.md -->

- [Inicio](/)
- [Guía](guide.md)
```

Debes crear un archivo `.nojekyll` en `./docs` para evitar que GitHub Pages ignore los archivos que comienzan con un guion bajo.

!> Docsify solo busca `_sidebar.md` en la carpeta actual y utiliza esa información, en caso contrario, se utilizará la configurada mediante `window.$docsify.loadSidebar`.

Ejemplo de estructura de archivos:

```text
└── docs/
    ├── _sidebar.md
    ├── index.md
    ├── getting-started.md
    └── running-services.md
```

## Barras laterales anidadas

Es posible que desees que la barra lateral se actualice después de la navegación para reflejar el directorio actual. Esto se puede hacer agregando un archivo `_sidebar.md` en cada carpeta.

El archivo `_sidebar.md` se carga desde cada directorio de nivel. Si el directorio actual no tiene `_sidebar.md`, se utilizará el del directorio padre. Si, por ejemplo, la ruta actual es `/guide/quick-start`, se cargará el `_sidebar.md` desde `/guide/_sidebar.md`.

Puedes especificar un `alias` para evitar una caída innecesaria.

```html
<script>
  window.$docsify = {
    loadSidebar: true,
    alias: {
      '/.*/_sidebar.md': '/_sidebar.md',
    },
  };
</script>
```

!> Puedes crear un archivo `README.md` en un subdirectorio para usarlo como página de inicio de la ruta.

## Establecer títulos de página desde la selección de la barra lateral

La etiqueta `title` de una página se genera a partir del nombre del elemento de la barra lateral seleccionado. Para mejorar el SEO, puedes personalizar el título especificando una cadena después del nombre del archivo.

```markdown
<!-- docs/_sidebar.md -->

- [Inicio](/)
- [Guía](guide.md 'La mejor guía del mundo')
```

## Tabla de contenido

Una vez que hayas creado `_sidebar.md`, el contenido de la barra lateral se genera automáticamente en función de los encabezados de los archivos Markdown.

Una barra lateral personalizada también puede generar automáticamente una tabla de contenido configurando un `subMaxLevel`, consulta [configuración subMaxLevel](/es/configuration.md#submaxlevel).

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2,
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

## Ignorar subencabezados

Cuando se establece `subMaxLevel`, cada encabezado se agrega automáticamente a la tabla de contenido de la barra lateral por defecto. Si deseas omitir un encabezado específico, agrega `<!-- {docsify-ignore} -->` a él.

```markdown
# Empezando

## Encabezado <!-- {docsify-ignore} -->

Este encabezado no aparecerá en la tabla de contenido de la barra lateral.
```

Para omitir todos los encabezados en una página específica, puedes usar `<!-- {docsify-ignore-all} -->` en el primer encabezado de la página.

```markdown
# Empezando <!-- {docsify-ignore-all} -->

## Encabezado

Este encabezado no aparecerá en la tabla de contenido de la barra lateral.
```

Tanto `<!-- {docsify-ignore} -->` como `<!-- {docsify-ignore-all} -->` no se representarán en la página cuando se utilicen.

Y las etiquetas `{docsify-ignore}` y `{docsify-ignore-all}` también pueden hacer lo mismo.
