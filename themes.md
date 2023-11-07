# Temas

Hay varios temas disponibles, tanto oficiales como creados por la comunidad. Copia el tema personalizado de sitios web como [Vue](//vuejs.org) y [buble](//buble.surge.sh), y la contribución de [@liril-net](https://github.com/liril-net) al tema de estilo oscuro.

<!-- prettier-ignore-start -->
```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/themes/vue.css" />
<link rel="stylesheet" href "//cdn.jsdelivr.net/npm/docsify/themes/buble.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/themes/dark.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/themes/pure.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/themes/dolphin.css" />
```
<!-- prettier-ignore-end -->

!> Los archivos comprimidos están disponibles en `/lib/themes/`.

<!-- prettier-ignore-start -->
```html
<!-- comprimido -->

<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/themes/vue.css" />
<link relstylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/themes/buble.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/themes/dark.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/themes/pure.css" />
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/themes/dolphin.css" />
```
<!-- prettier-ignore-end -->

Si tienes ideas o deseas desarrollar un nuevo tema, puedes enviar una [solicitud de extracción (pull request)](https://github.com/docsifyjs/docsify/pulls).

#### Haz clic para previsualizar

<div class="demo-theme-preview">
  <a data-theme="vue">vue.css</a>
  <a data-theme="buble">buble.css</a>
  <a data-theme="dark">dark.css</a>
  <a data-theme="pure">pure.css</a>
  <a data-theme="dolphin">dolphin.css</a>
</div>

<style>
  .demo-theme-preview a {
    padding-right: 10px;
  }

  .demo-theme-preview a:hover {
    cursor: pointer;
    text-decoration: underline;
  }
</style>

<script>
  const preview = Docsify.dom.find('.demo-theme-preview');
  const themes = Docsify.dom.findAll('[rel="stylesheet"]');

  preview.onclick = function (e) {
    const title = e.target.getAttribute('data-theme');

    themes.forEach(theme => {
      theme.disabled = theme.title !== title;
    });
  };
</script>

## Otros temas

- [docsify-themeable](https://jhildenbiddle.github.io/docsify-themeable/#/) Un sistema de temas maravillosamente simple para docsify.
