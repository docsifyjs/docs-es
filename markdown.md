# Configuración de Markdown

**docsify** utiliza [marked](https://github.com/markedjs/marked) como _parser_ de Markdown. Puedes personalizar cómo se renderiza tu contenido de Markdown en HTML personalizando el `renderer` de la siguiente manera:

```js
window.$docsify = {
  markdown: {
    smartypants: true,
    renderer: {
      link: function() {
        // ...
      }
    }
  }
}
```

?> Para obtener más opciones de configuración, consulta la [documentación de marked](https://github.com/markedjs/marked#options-1).

Incluso puedes personalizar por completo las reglas de _parsing_:

```js
window.$docsify = {
  markdown: function(marked, renderer) {
    // ...

    return marked;
  }
}
```

## Soporte de Mermaid

```js
// Importar Mermaid
//  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.css">
//  <script src="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

var num = 0;
mermaid.initialize({ startOnLoad: false });

window.$docsify = {
  markdown: {
    renderer: {
      code: function(code, lang) {
        if (lang === "mermaid") {
          return (
            '<div class="mermaid">' + mermaid.render('mermaid-svg-' + num++, code) + "</div>"
          );
        }
        return this.origin.code.apply(this, arguments);
      }
    }
  }
}
```
