# Barra de navegación personalizada

## HTML

Si necesitas una navegación personalizada, puedes crear una barra de navegación basada en HTML.

!> Ten en cuenta que los enlaces de documentación comienzan con `#/`.

```html
<!-- index.html -->

<body>
  <nav>
    <a href="#/">EN</a>
    <a href="#/zh-cn/">简体中文</a>
  </nav>
  <div id="app"></div>
</body>
```

## Markdown

Alternativamente, puedes crear un archivo de navegación personalizado basado en markdown configurando `loadNavbar` como **true** y creando `_navbar.md`, consulta la [configuración de loadNavbar](/es/configuration.md#loadnavbar).

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadNavbar: true,
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

```markdown
<!-- _navbar.md -->

- [Inglés](/)
- [Chino](/zh-cn/)
```

!> Necesitas crear un archivo `.nojekyll` en `./docs` para evitar que GitHub Pages ignore los archivos que comienzan con un guion bajo.

`_navbar.md` se carga desde cada directorio de nivel. Si el directorio actual no tiene `_navbar.md`, se buscará en el directorio padre. Por ejemplo, si la ruta actual es `/guia/inicio-rapido`, el archivo `_navbar.md` se cargará desde `/guia/_navbar.md`.

## Anidamiento

Puedes crear sublistas sangrando los elementos que se encuentran bajo un elemento principal.

```markdown
<!-- _navbar.md -->

- Empezar

  - [Inicio rápido](inicio-rapido.md)
  - [Escribir más páginas](mas-paginas.md)
  - [Barra de navegación personalizada](barra-navegacion-personalizada.md)
  - [Página de portada](portada.md)

- Configuración
  - [Configuración](configuracion.md)
  - [Temas](temas.md)
  - [Usar complementos](complementos.md)
  - [Configuración de Markdown](configuracion-markdown.md)
  - [Resaltado de lenguaje](resaltado-lenguaje.md)
```

se representa como

![Barra de navegación anidada](_images/barra-navegacion-anidada.png 'Barra de navegación anidada')

## Combinación de barras de navegación personalizadas con el complemento de emojis

Si utilizas el [complemento de emojis](plugins#emoji):

```html
<!-- index.html -->

<script>
  window.$docsify = {
    // ...
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```

puedes, por ejemplo, utilizar emojis de bandera en tu archivo de navegación personalizada de markdown:

```markdown
<!-- _navbar.md -->

- [:us:, :uk:](/)
- [:cn:](/zh-cn/)
```
