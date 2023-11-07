# Lista de complementos

## Búsqueda de texto completo

De forma predeterminada, se reconoce el hipervínculo en la página actual y el contenido se guarda en `localStorage`. También puedes especificar la ruta de los archivos.

<!-- prettier-ignore -->
```html
<script>
  window.$docsify = {
    search: 'auto', // predeterminado

    search: [
      '/',            // => /README.md
      '/guide',       // => /guide.md
      '/get-started', // => /get-started.md
      '/zh-cn/',      // => /zh-cn/README.md
    ],

    // Parámetros de configuración completos
    search: {
      maxAge: 86400000, // Tiempo de expiración, el predeterminado es un día
      paths: [], // o 'auto'
      placeholder: 'Escribe para buscar',

      // Localización
      placeholder: {
        '/zh-cn/': 'Buscar',
        '/': 'Escribe para buscar',
      },

      noData: '¡Sin resultados!',

      // Localización
      noData: {
        '/zh-cn/': 'No se encontraron resultados',
        '/': 'Sin resultados',
      },

      // Profundidad de los encabezados, 1 - 6
      depth: 2,

      hideOtherSidebarContent: false, // para ocultar o no el contenido de la barra lateral

      // Para evitar la colisión de índices de búsqueda
      // entre varios sitios web bajo el mismo dominio
      namespace: 'website-1',

      // Utiliza diferentes índices para los prefijos de las rutas (espacios de nombres).
      // NOTA: Solo funciona en el modo 'auto'.
      //
      // Al inicializar un índice, buscamos la primera ruta de la barra lateral.
      // Si coincide con el prefijo de la lista, cambiamos al índice correspondiente.
      pathNamespaces: ['/zh-cn', '/ru-ru', '/ru-ru/v1'],

      // Puedes proporcionar una expresión regular para que coincida con los prefijos. En este caso,
      // la subcadena coincidente se utilizará para identificar el índice.
      pathNamespaces: /^(\/(zh-cn|ru-ru))?(\/(v1|v2))?/,
    },
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

Este complemento ignora los acentos al realizar una búsqueda de texto completo (por ejemplo, "cafe" también coincidirá con "café").

## Google Analytics

> El servicio Universal Analytics de Google ya no procesará nuevos datos en propiedades estándar a partir del 1 de julio de 2023. Prepárate ahora configurando y cambiando a una propiedad de Google Analytics 4 y el complemento gtag.js de Docsify.

Instala el complemento y configura el ID de seguimiento.

```html
<script>
  window.$docsify = {
    ga: 'UA-XXXXX-Y',
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/ga.min.js"></script>
```

Configura mediante `data-ga`.

<!-- prettier-ignore -->
```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js" data-ga="UA-XXXXX-Y"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/ga.min.js"></script>
```

## Google Analytics 4 (GA4)

Instala el complemento y configura el ID de seguimiento.

```html
<script>
  // ID único
  window.$docsify = {
    gtag: 'UA-XXXXX-Y',
  };

  // Múltiples ID
  window.$docsify = {
    gtag: [
      'G-XXXXXXXX', // Google Analytics 4 (GA4)
      'UA-XXXXXXXX', // Google Universal Analytics (GA3)
      'AW-XXXXXXXX', // Google Ads
      'DC-XXXXXXXX', // Floodlight
    ],
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/gtag.min.js"></script>
```

## Emoji

Representa una colección más grande de códigos cortos de emoji. Sin este complemento, Docsify solo puede representar una cantidad limitada de códigos cortos de emoji.

!> Obsoleto a partir de la versión 4.13. Docsify ya no requiere este complemento para admitir emojis completos.

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```

## Script externo

Si el script en la página es un script externo (importa un archivo js mediante el atributo `src`), necesitarás este complemento para que funcione.

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/external-script.min.js"></script>
```

## Ampliar imagen

Zoom de imagen al estilo de Medium. Basado en [medium-zoom](https://github.com/francoischalifour/medium-zoom).

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

Excluye la imagen especial

```markdown
![](imagen.png ':no-zoom')
```

## Editar en GitHub

Añade un botón "Editar en GitHub" en todas las páginas. Proporcionado por [@njleonzhang](https://github.com/njleonzhang), consulta este [documento](https://github.com/njleonzhang/docsify-edit-on-github)

## Código de demostración con vista previa instantánea e integración de jsfiddle

Con este complemento, el código de ejemplo se puede representar en la página al instante, para que los lectores puedan ver la vista previa de inmediato.
Cuando los lectores expanden el cuadro de demostración, se muestran allí el código fuente y la descripción. Si hacen clic en el botón "Probar en Jsfiddle",
se abrirá `jsfiddle.net` con el código de esta muestra, lo que permite a los lectores modificar el código y probarlo por sí mismos.



[Vue](https://njleonzhang.github.io/docsify-demo-box-vue/) y [React](https://njleonzhang.github.io/docsify-demo-box-react/) son compatibles.

## Copiar al portapapeles

Añade un sencillo botón "Haz clic para copiar" a todos los bloques de código preformateados para permitir a los usuarios copiar fácilmente el código de ejemplo de tus documentos. Proporcionado por [@jperasmus](https://github.com/jperasmus)

```html
<script src="//cdn.jsdelivr.net/npm/docsify-copy-code/dist/docsify-copy-code.min.js"></script>
```

Consulta [aquí](https://github.com/jperasmus/docsify-copy-code/blob/master/README.md) para obtener más detalles.

## Disqus

Comentarios de Disqus. https://disqus.com/

```html
<script>
  window.$docsify = {
    disqus: 'nombre_corto',
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/disqus.min.js"></script>
```

## Gitalk

[Gitalk](https://github.com/gitalk/gitalk) es un componente de comentarios moderno basado en problemas de GitHub y Preact.

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.css" />

<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/gitalk.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: 'ID de la aplicación de GitHub',
    clientSecret: 'Secreto de la aplicación de GitHub',
    repo: 'repositorio de GitHub',
    owner: 'propietario del repositorio de GitHub',
    admin: [
      'colaboradores del repositorio de GitHub, solo estos usuarios pueden inicializar problemas de GitHub',
    ],
    // Modo libre de distracciones al estilo de Facebook
    distractionFreeMode: false,
  });
</script>
```

## Paginación

Paginación para Docsify. Proporcionado por [@imyelo](https://github.com/imyelo)

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify-pagination/dist/docsify-pagination.min.js"></script>
```

Haz clic [aquí](https://github.com/imyelo/docsify-pagination#readme) para obtener más información.

## Pestañas

Un complemento de docsify.js para mostrar contenido en pestañas a partir de Markdown.

- [Documentación y ejemplos](https://jhildenbiddle.github.io/docsify-tabs)

Proporcionado por [@jhildenbiddle](https://github.com/jhildenbiddle/docsify-tabs).

## Más complementos

Consulta [awesome-docsify](/es/awesome?id=plugins)
