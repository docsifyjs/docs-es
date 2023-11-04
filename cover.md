# Cover

Activa la función de portada estableciendo `coverpage` como **true**. Consulta la [configuración de portada](/es/configuration.md#coverpage).

## Uso básico

Establece `coverpage` como **true** y crea un archivo `_coverpage.md`:

```html
<!-- index.html -->

<script>
  window.$docsify = {
    coverpage: true,
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

```markdown
<!-- _coverpage.md -->

![logo](_media/icon.svg)

# docsify <small>3.5</small>

> Un generador mágico de sitios de documentación.

- Sencillo y ligero
- Sin archivos HTML generados estáticamente
- Múltiples temas

[GitHub](https://github.com/docsifyjs/docsify/)
[Empezar](#docsify)
```

## Fondo personalizado

El color de fondo se genera aleatoriamente de forma predeterminada. Puedes personalizar el color de fondo o una imagen de fondo:

```markdown
<!-- _coverpage.md -->

# docsify <small>3.5</small>

[GitHub](https://github.com/docsifyjs/docsify/)
[Empezar](#inicio-rápido)

<!-- imagen de fondo -->

![](_media/bg.png)

<!-- color de fondo -->

![color](#f0f0f0)
```

## Portada como página de inicio

Normalmente, la portada y la página de inicio aparecen al mismo tiempo. Por supuesto, también puedes separar la portada mediante la opción [onlyCover](/es/configuration.md#onlycover).

## Múltiples portadas

Si tu sitio de documentación está en más de un idioma, puede ser útil configurar múltiples portadas.

Por ejemplo, la estructura de tu documentación es la siguiente

```text
.
└── docs
    ├── README.md
    ├── guide.md
    ├── _coverpage.md
    └── zh-cn
        ├── README.md
        └── guide.md
        └── _coverpage.md
```

Ahora puedes configurar

```js
window.$docsify = {
  coverpage: ['/', '/zh-cn/'],
};
```

O un nombre de archivo especial

```js
window.$docsify = {
  coverpage: {
    '/': 'cover.md',
    '/zh-cn/': 'cover.md',
  },
};
```
