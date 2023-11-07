# Compatible con Vue

Docsify permite agregar contenido de Vue directamente a tus páginas de Markdown, lo que puede facilitar el trabajo con datos y agregar reactividad a tu sitio. Para comenzar, debes agregar Vue 2.x o 3.x a tu archivo `index.html`. Puedes elegir la versión de producción para tu sitio en vivo o la versión de desarrollo para obtener advertencias útiles en la consola y admitir las herramientas de desarrollo de Vue.js.

## Vue 2.x

Para Vue 2.x, puedes agregar las siguientes líneas de código a tu `index.html`:

```html
<!-- Producción -->
<script src="//cdn.jsdelivr.net/npm/vue@2/dist/vue.min.js"></script>

<!-- Desarrollo -->
<script src="//cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
```

## Vue 3.x

Para Vue 3.x, puedes agregar las siguientes líneas de código a tu `index.html`:

```html
<!-- Producción -->
<script src="//cdn.jsdelivr.net/npm/vue@3/dist/vue.global.prod.js"></script>

<!-- Desarrollo -->
<script src="//cdn.jsdelivr.net/npm/vue@3/dist/vue.global.js"></script>
```

Una vez que hayas agregado Vue a tu proyecto, podrás utilizar la sintaxis de plantilla de Vue para crear contenido dinámico en tus páginas de Markdown. Esta sintaxis ofrece características útiles como el soporte para expresiones de JavaScript y directivas de Vue para bucles y renderizado condicional.

Por ejemplo, puedes crear elementos condicionales con `v-if`, bucles con `v-for` y utilizar expresiones de JavaScript en tus páginas de Markdown para lograr contenido dinámico.

Si deseas utilizar datos, propiedades calculadas, métodos y hooks de ciclo de vida de Vue, puedes definirlos en tus páginas de Markdown o en opciones globales. Puedes montar elementos Vue utilizando la sintaxis de plantilla de Vue o creando componentes de Vue personalizados.

Recuerda que Docsify procesa el contenido de Vue en un orden específico en cada carga de página, lo que te permite crear contenido dinámico y reactivo en tu sitio web. Puedes definir datos globales, montar elementos Vue en páginas específicas y crear componentes de Vue personalizados para adaptar la experiencia del usuario.

### Propiedades calculadas

```js
{
  computed: {
    timeOfDay() {
      const date = new Date();
      const hours = date.getHours();

      if (hours < 12) {
        return 'mañana';
      }
      else if (hours < 18) {
        return 'tarde';
      }
      else {
        return 'noche'
      }
    }
  },
}
```

```markdown
¡Buenos {{ timeOfDay }}!
```

<output data-lang="output">

¡Buenos {{ timeOfDay }}!

</output>

### Métodos

```js
{
  data() {
    return {
      message: '¡Hola, Mundo!'
    };
  },
  methods: {
    hola() {
      alert(this.message);
    }
  },
}
```

```markdown
<button @click="hola">Decir Hola</button>
```

<output data-lang="output">
  <p><button @click="hola">Decir Hola</button></p>
</output>

### Hooks del ciclo de vida

```js
{
  data() {
    return {
      images: null,
    };
  },
  created() {
    fetch('https://api.dominio.com/')
      .then(response => response.json())
      .then(data => (this.images = data))
      .catch(err => console.log(err));
  }
}

// Respuesta de la API:
// [
//   { title: 'Imagen 1', url: 'https://dominio.com/1.jpg' },
//   { title: 'Imagen 2', url: 'https://dominio.com/2.jpg' },
//   { title: 'Imagen 3', url: 'https://dominio.com/3.jpg' },
// ];
```

```markdown
<div style="display: flex;">
  <figure style="flex: 1;">
    <img v-for="imagen in images" :src="imagen.url" :title="imagen.title">
    <figcaption>{{ imagen.title }}</figcaption>
  </figure>
</div>
```

<output data-lang="output">
  <div style="display: flex;">
    <figure v-for="imagen in images" style="flex: 1; text-align: center;">
      <img :src="imagen.url">
      <figcaption>{{ imagen.title }}</figcaption>
    </figure>
  </div>
</output>

## Opciones globales

Utiliza `vueGlobalOptions` para especificar [opciones de Vue](https://vuejs.org/v2/api/#Options-Data) que se utilizarán con contenido de Vue que no esté montado explícitamente con [vueMounts](/es/#mounts), [vueComponents](/es/#components), o un [script de Markdown](/es/#markdown-script). Los cambios en los datos globales se mantendrán y se reflejarán en cualquier referencia global donde se utilicen.

```js
window.$docsify = {
  vueGlobalOptions: {
    data() {
      return {
        count: 0,
      };
    },
  },
};
```

```markdown
<p>
  <button @click="count -= 1">-</button>
  {{ count }}
  <button @click="count += 1">+</button>
</p>
```

<output data-lang="output">
  <p>
    <button @click="count -= 1">-</button>
    {{ count }}
    <button @click="count += 1">+</button>
  </p>
</output>

Observa el comportamiento cuando se representan múltiples contadores globales:

<output data-lang="output">
  <p>
    <button @click="count -= 1">-</button>
    {{ count }}
    <button @click="count += 1">+</button>
  </p>
</output>

Los cambios realizados en uno de los contadores afectan a ambos contadores. Esto se debe a que ambas instancias hacen referencia al mismo valor global de `count`. Ahora, navega a una nueva página y vuelve a esta sección para ver cómo los cambios en los datos globales persisten entre las cargas de página.

## Montajes

Utiliza `vueMounts` para especificar elementos del DOM que se montarán como [instancias de Vue](https://vuejs.org/v2/guide/instance.html) y sus opciones asociadas. Los elementos de montaje se especifican mediante un [selector CSS](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Selectors) como clave y un objeto que contiene las opciones de Vue como su valor. Docsify montará el primer elemento coincidente en el área de contenido principal cada vez que se cargue una nueva página. Los datos del elemento montado son únicos para cada instancia y no persistirán a medida que los usuarios naveguen por el sitio.

```js
window.$docsify = {
  vueMounts: {
    '#counter': {
      data() {
        return {
          count: 0,
        };
      },
    },
  },
};
```

```markdown
<div id="counter">
  <button @click="count -= 1">-</button>
  {{ count }}
  <button @click="count += 1">+</button>
</div>
```

<output id="counter">
  <button @click="count -= 1">-</button>
  {{ count }}
  <button @click="count += 1">+</button>
</output>

## Componentes

Utiliza `vueComponents` para crear y registrar [componentes Vue](https://vuejs.org/v2/guide/components.html) globales. Los componentes se especifican utilizando el nombre del componente como clave y un objeto que contiene las opciones de Vue como valor. Los datos del componente son únicos para cada instancia y no persistirán a medida que los usuarios naveguen por el sitio.

```js
window.$docsify = {
  vueComponents: {
    'contador-de-botones': {
      template: `
        <button @click="count += 1">
          Me has clicado {{ count }} veces
        </button>
      `,
      data() {
        return {
          count: 0,
        };
      },
    },
  },
};
```

```markdown
<contador-de-botones></contador-de-botones>
<contador-de-botones></contador-de-botones>
```

<output data-lang="output">
  <contador-de-botones></contador-de-botones>
  <contador-de-botones></contador-de-botones>
</output>

## Script de Markdown

El contenido de Vue se puede montar usando una etiqueta `<script>` en tus páginas de Markdown.

!> Solo se ejecuta la primera etiqueta `<script>` en un archivo Markdown. Si deseas montar múltiples instancias de Vue utilizando una etiqueta script, todas las instancias deben montarse dentro de la primera etiqueta `<script>` en tu archivo Markdown.

```html
<!-- Vue 2.x  -->
<script>
  new Vue({
    el: '#ejemplo',
    // Opciones...
  });
</script>
```

```html
<!-- Vue 3.x  -->
<script>
  Vue.createApp({
    // Opciones...
  }).mount('#ejemplo');
</script>
```

## Notas técnicas

- Docsify procesa el contenido de Vue en el siguiente orden en cada carga de página:
  1. Ejecutar el markdown `<script>`
  1. Registrar `vueComponents` globales
  1. Montar `vueMounts`
  1. Montar automáticamente componentes de Vue no montados
  1. Montar automáticamente la sintaxis de plantilla de Vue no montada utilizando `vueGlobalOptions`
- Al montar automáticamente contenido de Vue, Docsify montará cada elemento de nivel superior en tu markdown que contiene sintaxis de plantilla o un componente. Por ejemplo, en el siguiente HTML, se montarán los elementos de nivel superior `<p>`, `<mi-componente />` y `<div>`.
  ```html
  <p>{{ foo }}</p>
  <mi-componente />
  <div>
    <span>{{ bar }}</span>
    <otro-componente />
  </div>
  ```
- Docsify no montará una instancia de Vue existente ni un elemento que contenga una instancia de Vue existente.
- Docsify destruirá/desmontará automáticamente todas las instancias de Vue que crea antes de cada carga de página.
