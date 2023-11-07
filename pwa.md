# Modo sin conexión

[Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/) (PWA) son experiencias que combinan lo mejor de la web con lo mejor de las aplicaciones. Podemos mejorar nuestro sitio web con trabajadores de servicio para que funcione **sin conexión** o en redes de baja calidad.

También es muy fácil de usar.

## Crear serviceWorker

Crea un archivo `sw.js` en el directorio raíz de tu proyecto y copia el siguiente código:

_sw.js_

```js
/* ===========================================================
 * docsify sw.js
 * ===========================================================
 * Copyright 2016 @huxpro
 * Licensed under Apache 2.0
 * Register service worker.
 * ========================================================== */

const RUNTIME = 'docsify';
const HOSTNAME_WHITELIST = [
  self.location.hostname,
  'fonts.gstatic.com',
  'fonts.googleapis.com',
  'cdn.jsdelivr.net',
];

// La función de utilidad para modificar las URL de las solicitudes interceptadas
const getFixedUrl = req => {
  const now = Date.now();
  const url = new URL(req.url);

  // 1. corregir URL http
  // Simplemente mantén la sincronización con location.protocol
  // fetch(httpURL) pertenece a contenido mixto activo.
  // Y fetch(httpRequest) aún no es compatible.
  url.protocol = self.location.protocol;

  // 2. agregar consulta para romper la caché.
  // Las páginas de GitHub se sirven con Cache-Control: max-age=600
  // max-age en contenido mutable es propenso a errores, con la vida de los errores del SW puede incluso extenderse.
  // Hasta que aterrice el modo de caché de la API Fetch, tenemos que evitar problemas de caché con una cadena de consulta.
  // Bug de Cache-Control: https://bugs.chromium.org/p/chromium/issues/detail?id=453190
  if (url.hostname === self.location.hostname) {
    url.search += (url.search ? '&' : '?') + 'cache-bust=' + now;
  }
  return url.href;
};

/**
 *  @Lifecycle Activate
 *  Se activa uno nuevo cuando el antiguo no se está utilizando.
 *
 *  waitUntil(): activar ====> activado
 */
self.addEventListener('activate', event => {
  event.waitUntil(self.clients.claim());
});

/**
 *  @Funcional Fetch
 *  Todas las solicitudes de red se interceptan aquí.
 *
 *  void respondWith(Promise<Response> r)
 */
self.addEventListener('fetch', event => {
  // Omitir algunas solicitudes entre dominios, como las de Google Analytics.
  if (HOSTNAME_WHITELIST.indexOf(new URL(event.request.url).hostname) > -1) {
    // Stale-while-revalidate
    // similar a stale-while-revalidate de HTTP: https://www.mnot.net/blog/2007/12/12/stale
    // Actualización de la versión de Jake a la de Surma: https://gist.github.com/surma/eb441223daaedf880801ad80006389f1
    const cached = caches.match(event.request);
    const fixedUrl = getFixedUrl(event.request);
    const fetched = fetch(fixedUrl, { cache: 'no-store' });
    const fetchedCopy = fetched.then(resp => resp.clone());

    // Llama a respondWith() con lo que obtengamos primero.
    // Si la recuperación falla (por ejemplo, desconexión), espera la caché.
    // Si no hay nada en la caché, espera la recuperación.
    // Si ninguno de ellos proporciona una respuesta, devuelve páginas sin conexión.
    event.respondWith(
      Promise.race([fetched.catch(_ => cached), cached])
        .then(resp => resp || fetched)
        .catch(_ => {
          /* come cualquier error */
        })
    );

    // Actualiza la caché con la versión que recuperamos (solo para estados ok)
    event.waitUntil(
      Promise.all([fetchedCopy, caches.open(RUNTIME)])
        .then(
          ([response, cache]) =>
            response.ok && cache.put(event.request, response)
        )
        .catch(_ => {
          /* come cualquier error */
        })
    );
  }
});
```

## Registrar

Ahora, regístralo en tu `index.html`. Solo funciona en algunos navegadores modernos, así que debemos verificar:

_index.html_

```html
<script>
  if (typeof navigator.serviceWorker !== 'undefined') {
    navigator.serviceWorker.register('sw.js');
  }
</script>
```

## Disfrútalo

Publica tu sitio web y comienza a experimentar la mágica función sin conexión. :ghost: Puedes apagar el Wi-Fi y actualizar el sitio actual para experimentarlo.
