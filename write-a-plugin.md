# Crear un complemento

Un complemento de Docsify es una función con la capacidad de ejecutar código JavaScript personalizado en varias etapas del ciclo de vida de Docsify.

## Configuración

Los complementos de Docsify se pueden agregar directamente al array `plugins`:

```js
window.$docsify = {
  plugins: [
    function myPlugin1(hook, vm) {
      // ...
    },
    function myPlugin2(hook, vm) {
      // ...
    },
  ],
};
```

Alternativamente, un complemento se puede guardar en un archivo separado e "instalarlo" utilizando una etiqueta `<script>` estándar:

```js
// docsify-plugin-myplugin.js

{
  function myPlugin(hook, vm) {
    // ...
  }

  // Agrega el complemento al array de complementos de docsify
  window.$docsify = window.$docsify || {};
  $docsify.plugins = [...($docsify.plugins || []), myPlugin];
}
```

```html
<script src="docsify-plugin-myplugin.js"></script>
```

## Plantilla

A continuación, se muestra una plantilla de complemento con marcadores de posición para todos los hooks de ciclo de vida disponibles.

1. Copia la plantilla.
2. Modifica el nombre `myPlugin` según corresponda.
3. Agrega tu lógica de complemento.
4. Elimina los hooks de ciclo de vida no utilizados.
5. Guarda el archivo como `docsify-plugin-[nombre].js`.
6. Carga tu complemento utilizando una etiqueta `<script>` estándar.

```js
{
  function myPlugin(hook, vm) {
    // Invocado una vez cuando se inicializa el script de Docsify
    hook.init(() => {
      // ...
    });

    // Invocado una vez cuando la instancia de Docsify se ha montado en el DOM
    hook.mounted(() => {
      // ...
    });

    // Invocado en cada carga de página antes de que el nuevo markdown se transforme a HTML.
    // Admite tareas asincrónicas (consulte la documentación de beforeEach para obtener más detalles).
    hook.beforeEach(markdown => {
      // ...
      return markdown;
    });

    // Invocado en cada carga de página después de que el nuevo markdown se ha transformado a HTML.
    // Admite tareas asincrónicas (consulte la documentación de afterEach para obtener más detalles).
    hook.afterEach(html => {
      // ...
      return html;
    });

    // Invocado en cada carga de página después de que el nuevo HTML se haya agregado al DOM
    hook.doneEach(() => {
      // ...
    });

    // Invocado una vez después de renderizar la página inicial
    hook.ready(() => {
      // ...
    });
  }

  // Agrega el complemento al array de complementos de Docsify
  window.$docsify = window.$docsify || {};
  $docsify.plugins = [myPlugin, ...($docsify.plugins || [])];
}
```

## Hooks de ciclo de vida

Los hooks de ciclo de vida se proporcionan a través del argumento `hook` pasado a la función del complemento.

### init()

Invocado una vez cuando se inicializa el script de Docsify.

```js
hook.init(() => {
  // ...
});
```

### mounted()

Invocado una vez cuando la instancia de Docsify se ha montado en el DOM.

```js
hook.mounted(() => {
  // ...
});
```

### beforeEach()

Invocado en cada carga de página antes de que el nuevo markdown se transforme a HTML.

```js
hook.beforeEach(markdown => {
  // ...
  return markdown;
});
```

Para tareas asincrónicas, la función de hook acepta un segundo argumento `next`. Llama a esta función con el valor final de `markdown` cuando esté listo. Para evitar que los errores afecten a Docsify y otros complementos, envuelve el código asincrónico en un bloque `try/catch/finally`.

```js
hook.beforeEach((markdown, next) => {
  try {
    // Tarea(s) asincrónica(s)...
  } catch (err) {
    // ...
  } finally {
    next(markdown);
  }
});
```

### afterEach()

Invocado en cada carga de página después de que el nuevo markdown se ha transformado a HTML.

```js
hook.afterEach(html => {
  // ...
  return html;
});
```

Para tareas asincrónicas, la función de hook acepta un segundo argumento `next`. Llama a esta función con el valor final de `html` cuando esté listo. Para evitar que los errores afecten a Docsify y otros complementos, envuelve el código asincrónico en un bloque `try/catch/finally`.

```js
hook.afterEach((html, next) => {
  try {
    // Tarea(s) asincrónica(s)...
  } catch (err) {
    // ...
  } finally {
    next(html);
  }
});
```

### doneEach()

Invocado en cada carga de página después de que el nuevo HTML se haya agregado al DOM.

```js
hook.doneEach(() => {
  // ...
});
```

### ready()

Invocado una vez después de renderizar la página inicial.

```js
hook.ready(() => {
  // ...
});
```

## Consejos

- Accede a los métodos y propiedades de Docsify utilizando `window.Docsify`
- Accede a la instancia actual de Docsify utilizando el argumento `vm`
- Los desarrolladores que prefieran utilizar un depurador pueden configurar la opción de configuración [`catchPluginErrors`](configuration#catchpluginerrors) en `false` para permitir que su depurador pause la ejecución de JavaScript en caso de error.
- Asegúrate de probar tu complemento en todas las plataformas admitidas y con las opciones de configuración relacionadas (si corresponde) antes de publicarlo.

## Ejemplos

#### Pie de página de la página

```js
window.$docsify = {
  plugins: [
    function pageFooter(hook, vm) {
      const footer = /* html */ `
        <hr/>
        <footer>
          <span><a href="https://github.com/QingWei-Li">cinwell</a> &copy;2017.</span>
          <span>Publicado con orgullo utilizando <a href="https://github.com/docsifyjs/docsify" target="_blank">docsify</a>.</span>
        </footer>
      `;

      hook.afterEach(html => {
        return html + footer;
      });
    },
  ],
};
```

### Botón de edición (GitHub)

```js
window.$docsify = {
  plugins: [
    function editButton(hook, vm) {
      // El patrón de plantilla de fecha
      $docsify.formatUpdated = '{YYYY}/{MM}/{DD} {HH}:{mm}';

      hook.beforeEach(html => {
        const url =
          'https://github.com/docsifyjs/docsify/blob/master/docs/' +
          vm.route.file;
        const editHtml = '[📝 EDITAR DOCUMENTO](' + url + ')\n';

        return (
          editHtml +
          html +
          '\n----\n' +
          'Última modificación {docsify-updated}' +
          editHtml
        );
      });
    },
  ],
};
```
