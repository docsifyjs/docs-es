# Incrustar archivos

Con docsify 4.6 ahora es posible incrustar cualquier tipo de archivo.

Puedes incrustar estos archivos como video, audio, iframes o bloques de código, e incluso los archivos Markdown se pueden incrustar directamente en el documento.

Por ejemplo, aquí hay un archivo Markdown incrustado. Solo necesitas hacer lo siguiente:

```markdown
[filename](_media/ejemplo.md ':include')
```

Entonces, el contenido de `ejemplo.md` se mostrará directamente aquí:

[filename](_media/ejemplo.md ':include')

Puedes verificar el contenido original de [ejemplo.md](_media/ejemplo.md ':ignore').

Normalmente, esto se compilará en un enlace, pero en docsify, si agregas `:include`, se incrustará. Puedes usar comillas simples o dobles según tu preferencia.

Los enlaces externos también se pueden usar; solo reemplaza el destino. Si deseas utilizar una URL de gist, consulta la sección [Incrustar un gist](#incrustar-un-gist).

## Tipo de archivo incrustado

Actualmente, las extensiones de archivo se reconocen automáticamente y se incrustan de diferentes maneras.

Estos tipos son compatibles:

- **iframe** `.html`, `.htm`
- **markdown** `.markdown`, `.md`
- **audio** `.mp3`
- **video** `.mp4`, `.ogg`
- **código** otra extensión de archivo

Por supuesto, puedes forzar el tipo especificado. Por ejemplo, un archivo Markdown se puede incrustar como un bloque de código estableciendo `:type=code`.

```markdown
[filename](_media/ejemplo.md ':include :type=code')
```

Obtendrás:

[filename](_media/ejemplo.md ':include :type=code')

## Markdown con Front Matter YAML

Cuando uses Markdown, el front matter YAML se eliminará del contenido renderizado. Los atributos no se pueden usar en este caso.

```markdown
[filename](_media/ejemplo-con-yaml.md ':include')
```

Obtendrás solo el contenido

[filename](_media/ejemplo-con-yaml.md ':include')

## Fragmentos de código incrustados

A veces, no deseas incrustar un archivo completo. Tal vez solo necesitas algunas líneas, pero deseas compilar y probar el archivo en CI.

```markdown
[filename](_media/ejemplo.js ':include :type=code :fragment=demo')
```

En tu archivo de código, debes rodear el fragmento entre las líneas `/// [demo]` (antes y después del fragmento). Alternativamente, puedes usar `### [demo]`.

Ejemplo:

[filename](_media/ejemplo.js ':include :type=code :fragment=demo')

## Atributo de etiqueta

Si incrustas el archivo como `iframe`, `audio` y `video`, es posible que necesites configurar los atributos de estas etiquetas.

?> Nota, para los tipos `audio` y `video`, docsify agrega automáticamente el atributo `controls` por defecto. Cuando desees agregar más atributos, el atributo `controls` debe agregarse manualmente si es necesario.

```md
[filename](_media/ejemplo.mp4 ':include :type=video controls width=100%')
```

```markdown
[sitio web de cinwell](https://cinwell.com ':include :type=iframe width=100% height=400px')
```

[sitio web de cinwell](https://cinwell.com ':include :type=iframe width=100% height=400px')

¿Lo viste? Solo necesitas escribir directamente. Puedes consultar [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) para obtener información sobre estos atributos.

## Resaltar el bloque de código

Al incrustar cualquier tipo de archivo fuente, puedes especificar el lenguaje resaltado o identificarlo automáticamente.

```markdown
[](_media/ejemplo.html ':include :type=code text')
```

⬇️

[](_media/ejemplo.html ':include :type=code text')

?> ¿Cómo se establece el resaltado? Puedes verlo [aquí](/es/language-highlight.md).

## Incrustar un gist

Puedes incrustar un gist como contenido en formato markdown o como un bloque de código, basándote en el enfoque al comienzo de la sección [Incrustar archivos](/es/#embed-files), pero utilizando una URL de gist sin formato como destino.

?> **No** se necesita ningún cambio en el complemento o configuración de la aplicación para que esto funcione. De hecho, la etiqueta "Incrustar" `script` que se copia desde un gist no se cargará incluso si realizas cambios en el complemento o la configuración para permitir un script externo.

### Identificar los metadatos del gist

Comienza por ver un gist en `gist.github.com`. Para los fines de esta guía, utilizaremos este gist:

- https://gist.github.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15

Identifica los siguientes elementos del gist:

| Campo        | Ejemplo                            | Descripción                                                                                        |
| ------------ | ---------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Nombre de usuario** | `anikethsaha`                      | El propietario del gist.                                                                                  |
| **ID de Gist**  | `c2bece08f27c4277001f123898d16a7c` | Identificador del gist. Este es fijo durante toda la vida útil del gist.                                    |
| **Nombre de archivo** | `content.md`                       | Selecciona un nombre de archivo en el gist. Esto es necesario incluso en un gist de un solo archivo para que la incrustación funcione. |

Necesitarás estos elementos para construir la _URL sin formato del gist_ para el archivo de destino. Esta tiene el siguiente formato:

- `https://gist.githubusercontent.com/NOMBRE_DE_USUARIO/ID_DE_GIST/raw/NOMBRE_DE_ARCHIVO`

Aquí tienes dos ejemplos basados en el gist de muestra:

- https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/content.md
- https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/script.js

?> Alternativamente, puedes obtener una URL sin formato haciendo clic directamente en el botón _Raw_ de un archivo de gist. Sin embargo, si utilizas ese enfoque, asegúrate de **eliminar** el número de revisión entre `raw/` y el nombre del archivo para que la URL coincida con el patrón anterior. De lo contrario, tu gist incrustado **no** mostrará el contenido más reciente cuando se actualice el gist.

Continúa con una de las secciones a continuación para incrustar el gist en una página de Docsify.

### Renderizar contenido en formato markdown desde un gist

Esta es una excelente manera de incrustar contenido de manera **fluida** en tu documentación, sin enviar a alguien a un enlace externo. Este enfoque es adecuado para reutilizar un gist, como las instrucciones de instalación, en sitios de documentación de varios repositorios. Este enfoque funciona igual de bien con un gist de tu cuenta o de otro usuario.

Aquí está el formato:

```markdown
[ETIQUETA](https://gist.githubusercontent.com/NOMBRE_DE_USUARIO/ID_DE_GIST/raw/NOMBRE_DE_ARCHIVO ':include')
```

Por ejemplo:

```markdown
[gist: content.md](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/content.md ':include')
```

Lo cual se muestra como:

[gist: content.md](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/content.md ':include')

La `ETIQUETA` puede ser cualquier texto que desees. Actúa como un mensaje de _respaldo_ si el enlace está roto, por lo que es útil repetir el nombre del archivo aquí en caso de que necesites corregir un enlace roto. También hace que un elemento incrustado sea fácil de leer de un vistazo.

### Renderizar un bloque de código desde un gist

El formato es el mismo que en la sección anterior, pero con `:type=code` agregado al texto alternativo. Al igual que en la sección [Tipo de archivo incrustado](/es/#embedded-file-type), el resaltado de sintaxis se **inferirá** a partir de la extensión (por ejemplo, `.js` o `.py`), por lo que puedes dejar el tipo establecido como `code`.

Aquí está el formato:

```markdown
[ETIQUETA](https://gist.githubusercontent.com/NOMBRE_DE_USUARIO/ID_DE_GIST/raw/NOMBRE_DE_ARCHIVO ':include :type=code')
```

Por ejemplo:

```markdown
[gist: script.js](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/script.js ':include :type=code')
```

Lo cual se muestra como:

[gist: script.js](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/script.js ':include :type=code')
