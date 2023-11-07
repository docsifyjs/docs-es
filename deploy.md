# Deploy

Similar a [GitBook](https://www.gitbook.com), puedes implementar los archivos en GitHub Pages, GitLab Pages o un VPS.

## GitHub Pages

Hay tres lugares para alojar tu documentación en tu repositorio de GitHub:

- Carpeta `docs/`
- Rama principal (main)
- Rama gh-pages

Se recomienda guardar tus archivos en la subcarpeta `./docs` de la rama `main` de tu repositorio. Luego, selecciona `main branch /docs folder` como fuente de GitHub Pages en la página de configuración de tu repositorio.

![GitHub Pages](_images/deploy-github-pages.png)

!> También puedes guardar los archivos en el directorio raíz y seleccionar `main branch`.
Necesitarás colocar un archivo `.nojekyll` en la ubicación de implementación (como `/docs` o la rama gh-pages).

## GitLab Pages

Si estás implementando tu rama principal, crea un archivo `.gitlab-ci.yml` con el siguiente script:

?> El truco `.public` evita que `cp` copie `public/` a sí mismo en un bucle infinito.

```YAML
pages:
  stage: deploy
  script:
  - mkdir .public
  - cp -r * .public
  - mv .public public
  artifacts:
    paths:
    - public
  only:
  - master
```

!> Puedes reemplazar el script con `- cp -r docs/. public` si `./docs` es tu subcarpeta de Docsify.

## Firebase Hosting

!> Debes instalar Firebase CLI utilizando `npm i -g firebase-tools` después de iniciar sesión en la [Consola de Firebase](https://console.firebase.google.com) con una cuenta de Google.

Usa la terminal para determinar y navegar al directorio de tu proyecto de Firebase. Esto podría ser `~/Proyectos/Docs`, etc. Luego, ejecuta `firebase init` y elige `Hosting` en el menú (usa **espacio** para seleccionar, las **teclas de flecha** para cambiar las opciones y **enter** para confirmar). Sigue las instrucciones de configuración.

Tu archivo `firebase.json` debería verse similar a esto (cambié el directorio de implementación de `public` a `site`):

```json
{
  "hosting": {
    "public": "site",
    "ignore": ["firebase.json", "**/.*", "**/node_modules/**"]
  }
}
```

Una vez que hayas terminado, crea la plantilla inicial ejecutando `docsify init ./site` (reemplaza site con el directorio de implementación que determinaste al ejecutar `firebase init` - por defecto, es public). Agrega o edita la documentación y luego ejecuta `firebase deploy` desde el directorio del proyecto raíz.

## VPS

Usa la siguiente configuración de Nginx.

```nginx
server {
  listen 80;
  server_name  tu.dominio.com;

  location / {
    alias /ruta/a/la/carpeta/docs/;
    index index.html;
  }
}
```

## Netlify

1. Inicia sesión en tu cuenta de [Netlify](https://www.netlify.com/).
2. En la página del [panel de control](https://app.netlify.com/), haz clic en **Nuevo sitio desde Git**.
3. Elige un repositorio donde almacenas tu documentación, deja el área de **Comando de construcción** en blanco y completa el área de directorio de publicación con el directorio de tu `index.html`. Por ejemplo, debe ser `docs` si lo implementaste en `docs/index.html`.

### Enrutador HTML5

Cuando utilizas el enrutador HTML5, debes configurar reglas de redirección que redirijan todas las solicitudes a tu `index.html`. Es bastante simple cuando usas Netlify. Simplemente crea un archivo llamado `_redirects` en el directorio de la documentación, agrega este fragmento al archivo y listo:

```sh
/*    /index.html   200
```

## Vercel

1. Instala la [CLI de Vercel](https://vercel.com/download), `npm i -g vercel`.
2. Cambia al directorio de tu sitio de Docsify, por ejemplo, `cd docs`.
3. Implementa con un solo comando, `vercel`.

## AWS Amplify

1. Configura `routerMode` en el archivo `index.html` del proyecto Docsify como _history_.

```html
<script>
  window.$docsify = {
    loadSidebar: true,
    routerMode: 'history',
  };
</script>
```

2. Inicia sesión en tu [Consola de AWS](https

://aws.amazon.com).
3. Ve al [Panel de AWS Amplify](https://aws.amazon.com/amplify).
4. Elige la ruta **Deploy** para configurar tu proyecto.
5. Cuando se te solicite, deja vacías las configuraciones de compilación si estás sirviendo tu documentación en el directorio raíz. Si estás sirviendo tu documentación desde un directorio diferente, personaliza tu amplify.yml.

```yml
version: 0.1
frontend:
  phases:
    build:
      commands:
        - echo "Nothing to build"
  artifacts:
    baseDirectory: /docs
    files:
      - '**/*'
  cache:
    paths: []
```

6. Agrega las siguientes reglas de redirección en el orden que se muestran. Ten en cuenta que el segundo registro es una imagen PNG que puedes cambiar por cualquier formato de imagen que estés utilizando.

| Dirección de origen | Dirección de destino | Tipo           |
| ------------------- | ------------------- | -------------- |
| /<\*>.md            | /<\*>.md            | 200 (Redirección) |
| /<\*>.png           | /<\*>.png           | 200 (Redirección) |
| /<\*>               | /index.html         | 200 (Redirección) |

## Docker

- Crea archivos de Docsify

  Necesitas preparar los archivos iniciales en lugar de crearlos dentro del contenedor. Consulta la sección [Inicio rápido](https://docsify.js.org/#/quickstart) para obtener instrucciones sobre cómo crear estos archivos manualmente o utilizando [docsify-cli](https://github.com/docsifyjs/docsify-cli).

  ```sh
  index.html
  README.md
  ```

- Crea el archivo Dockerfile

  ```Dockerfile
    FROM node:latest
    LABEL description="Un archivo Dockerfile de demostración para construir Docsify."
    WORKDIR /docs
    RUN npm install -g docsify-cli@latest
    EXPOSE 3000/tcp
    ENTRYPOINT docsify serve .
  ```

  La estructura actual del directorio debe ser la siguiente:

  ```sh
   index.html
   README.md
   Dockerfile
  ```

- Construye la imagen de Docker

  ```sh
  docker build -f Dockerfile -t docsify/demo .
  ```

- Ejecuta la imagen de Docker

  ```sh
  docker run -itp 3000:3000 --name=docsify -v $(pwd):/docs docsify/demo
  ```
