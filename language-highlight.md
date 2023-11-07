# Resaltado de lenguaje

Docsify utiliza [Prism](https://prismjs.com) para resaltar bloques de código en tus páginas. Prism admite los siguientes lenguajes de forma predeterminada:

- Marcado - `markup`, `html`, `xml`, `svg`, `mathml`, `ssml`, `atom`, `rss`
- CSS - `css`
- Tipo C - `clike`
- JavaScript - `javascript`, `js`

El soporte para [idiomas adicionales](https://prismjs.com/#supported-languages) está disponible cargando los archivos de gramática específicos del idioma [via CDN](https://cdn.jsdelivr.net/npm/prismjs@1/components/):

```html
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-php.min.js"></script>
```

!> Esta etiqueta `<script>` debe colocarse después de la etiqueta `<script>` de Docsify para que funcione.

Para habilitar el resaltado de sintaxis, envuelve cada bloque de código en triple comilla invertida con el [lenguaje](https://prismjs.com/#supported-languages) especificado en la primera línea:

````
```html
<p>Este es un párrafo</p>
<a href="//docsify.js.org/">Docsify</a>
```

```bash
echo "hola"
```

```php
function getAdder(int $x): int
{
    return 123;
}
```
````

El markdown anterior se representará como:

```html
<p>Este es un párrafo</p>
<a href="//docsify.js.org/">Docsify</a>
```

```bash
echo "hola"
```

```php
function getAdder(int $x): int
{
    return 123;
}
```

## Resaltado de contenido dinámico

Los bloques de código [creados dinámicamente desde JavaScript](https://docsify.js.org/#/configuration?id=executescript) se pueden resaltar utilizando el método `Prism.highlightElement` de la siguiente manera:

```javascript
const code = document.createElement('code');
code.innerHTML = "console.log('¡Hola, mundo!')";
code.setAttribute('class', 'lang-javascript');
Prism.highlightElement(code);
```
