# Doc helper

docsify amplía la sintaxis de Markdown para que tus documentos sean más legibles.

> Nota: Para los casos de sintaxis de código especial, es mejor colocarlos dentro de comillas invertidas de código para evitar conflictos con configuraciones o emojis.

## Contenido importante

Contenido importante como:

```markdown
!> ¡**El tiempo** es dinero, amigo!
```

se renderiza como:

!> ¡**El tiempo** es dinero, amigo!

## Consejos generales

Consejos generales como:

```markdown
?> _POR HACER_ prueba unitaria
```

se renderizan como:

?> _POR HACER_ prueba unitaria

## Ignorar la compilación del enlace

A veces usaremos alguna otra ruta relativa para el enlace, y debemos decirle a docsify que no necesitamos compilar este enlace. Por ejemplo:

```md
[enlace](/demo/)
```

Se compilará como `<a href="/#/demo/">enlace</a>` y cargará `/demo/README.md`. Tal vez desees saltar a `/demo/index.html`.

Ahora puedes hacerlo así:

```md
[enlace](/demo/ ':ignore')
```

Obtendrás `<a href="/demo/">enlace</a>`. No te preocupes, aún puedes establecer el título para el enlace.

```md
[enlace](/demo/ ':ignore título')

<a href="/demo/" título="título">enlace</a>
```

## Establecer atributo de destino para el enlace

```md
[enlace](/demo ':target=_blank')
[enlace](/demo2 ':target=_self')
```

## Deshabilitar el enlace

```md
[enlace](/demo ':disabled')
```

## Listas de tareas de GitHub

```md
- [ ] foo
- bar
- [x] baz
- [] bam <~ no funciona
  - [ ] bim
  - [ ] lim
```

- [ ] foo
- bar
- [x] baz
- [] bam <~ no funciona
  - [ ] bim
  - [ ] lim

## Imagen

### Cambiar tamaño

```md
![logo](https://docsify.js.org/_media/icon.svg ':size=ANCHOxALTO')
![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')

<!-- Soporta porcentaje -->

![logo](https://docsify.js.org/_media/icon.svg ':size=10%')
```

![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')
![logo](https://docsify.js.org/_media/icon.svg ':size=10%')

### Personalizar clase

```md
![logo](https://docsify.js.org/_media/icon.svg ':class=algunaClaseCss')
```

### Personalizar ID

```md
![logo](https://docsify.js.org/_media/icon.svg ':id=algunaIdCss')
```

## Personalizar ID para encabezados

```md
### ¡Hola, mundo! :id=hola-mundo
```

## Markdown en etiquetas HTML

Necesitas insertar un espacio entre el contenido HTML y el contenido de Markdown. Esto es útil para renderizar contenido de Markdown en el elemento "details".

```markdown
<details>
<summary>Autoevaluación (Haz clic para expandir)</summary>

- Abc
- Abc

</details>
```

<details>
<summary>Autoevaluación (Haz clic para expandir)</summary>

- Abc
- Abc

</details>

El contenido de Markdown también se puede envolver en etiquetas HTML.

```markdown
<div style='color: red'>

- elemento de lista
- elemento de lista
- elemento de lista

</div>
```

<div style='color: red'>

- Abc
- Abc

</div>
