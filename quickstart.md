# Inicio Rápido

!> Esta página aún no está traducido al español, estamos traduciendo... si gustas, puedes ayudar.

Se recomienda instalar `docsify-cli` globalmente, lo que ayuda a inicializar y obtener una vista previa del sitio web localmente.

```bash
npm i docsify-cli -g
```

## Inicializar 

Si desea escribir la documentación en el subdirectorio `./docs`, puede usar el comando `init`.

```bash
docsify init ./docs
```

## Escribir contenido

Después de que se complete `init`, puede ver la lista de archivos en el subdirectorio `./docs`.

* `index.html` como el archivo de entrada
* `README.md` como la página de inicio (la principal)
* `.nojekyll` impide que las páginas de GitHub ignoren los archivos que comienzan con un guión bajo

Puede actualizar fácilmente la documentación en `./docs/README.md`, por supuesto puede agregar [más páginas](more-pages.md).

## Preview your site

Run the local server with `docsify serve`. You can preview your site in your browser on `http://localhost:3000`.

```bash
docsify serve docs
```

?> For more use cases of `docsify-cli`, head over to the [docsify-cli documentation](https://github.com/QingWei-Li/docsify-cli).

## Manual initialization

If you don't like `npm` or have trouble installing the tool, you can manually create `index.html`:

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      //...
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
</body>
</html>
```

If you installed python on your system, you can easily use it to run a static server to preview your site.

```bash
cd docs && python -m SimpleHTTPServer 3000
```

## Loading dialog

If you want, you can show a loading dialog before docsify starts to render your documentation:

```html
  <!-- index.html -->

  <div id="app">Please wait...</div>
```

You should set the `data-app` attribute if you changed `el`:

```html
  <!-- index.html -->

  <div data-app id="main">Please wait...</div>

  <script>
    window.$docsify = {
      el: '#main'
    }
  </script>
```

Compare [el configuration](configuration.md#el).
