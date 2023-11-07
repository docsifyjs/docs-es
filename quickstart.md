# Inicio rápido

Se recomienda instalar `docsify-cli` de forma global, lo que ayuda a inicializar y previsualizar el sitio web localmente.

```bash
npm i docsify-cli -g
```

## Inicialización

Si deseas escribir la documentación en el subdirectorio `./docs`, puedes utilizar el comando `init`.

```bash
docsify init ./docs
```

## Escribir contenido

Después de completar la inicialización, podrás ver la lista de archivos en el subdirectorio `./docs`.

- `index.html` como archivo de entrada
- `README.md` como página de inicio
- `.nojekyll` evita que GitHub Pages ignore los archivos que comienzan con un guion bajo

Puedes actualizar fácilmente la documentación en `./docs/README.md`, y, por supuesto, puedes agregar [más páginas](/es/more-pages.md).

## Previsualiza tu sitio

Ejecuta el servidor local con `docsify serve`. Puedes previsualizar tu sitio en tu navegador en `http://localhost:3000`.

```bash
docsify serve docs
```

?> Para obtener más casos de uso de `docsify-cli`, consulta la [documentación de docsify-cli](https://github.com/docsifyjs/docsify-cli).

## Inicialización manual

Si no te gusta `npm` o tienes problemas para instalar la herramienta, puedes crear manualmente `index.html`:

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <meta charset="UTF-8" />
    <link
      rel="stylesheet"
      href="//cdn.jsdelivr.net/npm/docsify@4/themes/vue.css"
    />
  </head>
  <body>
    <div id="app"></div>
    <script>
      window.$docsify = {
        //...
      };
    </script>
    <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  </body>
</html>
```

### Especificación de versiones de docsify

?> Ten en cuenta que en ambos ejemplos a continuación, las URL de docsify deberán actualizarse manualmente cuando se lance una nueva versión importante de docsify (por ejemplo, `v4.x.x` => `v5.x.x`). Consulta el sitio web de docsify periódicamente para ver si se ha lanzado una nueva versión importante.

Especificar una versión importante en la URL (`@4`) permitirá que tu sitio reciba mejoras que no rompan la compatibilidad (es decir, actualizaciones "menores") y correcciones de errores (es decir, actualizaciones "de corrección") automáticamente. Esta es la forma recomendada de cargar los recursos de docsify.

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/themes/vue.css" />
<script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
```

Si prefieres bloquear docsify en una versión específica, especifica la versión completa después del símbolo `@` en la URL. Esta es la forma más segura de garantizar que tu sitio tenga la misma apariencia y se comporte de la misma manera, independientemente de los cambios realizados en las futuras versiones de docsify.

```html
<link
  rel="stylesheet"
  href="//cdn.jsdelivr.net/npm/docsify@4.11.4/themes/vue.css"
/>
<script src="//cdn.jsdelivr.net/npm/docsify@4.11.4"></script>
```

### Previsualización manual de tu sitio

Si tienes Python instalado en tu sistema, puedes usarlo fácilmente para ejecutar un servidor estático y previsualizar tu sitio.

```python2
cd docs && python -m SimpleHTTPServer 3000
```

```python3
cd docs && python -m http.server 3000
```

## Diálogo de carga

Si lo deseas, puedes mostrar un diálogo de carga antes de que docsify comience a renderizar tu documentación:

```html
<!-- index.html -->

<div id="app">Por favor, espera...</div>
```

Debes establecer el atributo `data-app` si cambias `el`:

```html
<!-- index.html -->

<div data-app id="main">Por favor, espera...</div>

<script>
  window.$docsify = {
    el: '#main',
  };
</script>
```

Compara [la configuración de `el`](/es/configuration.md#el).
