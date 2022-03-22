# Fetch API

La *Fetch API* proporciona una interfaz para obtener recursos en linea(incluso a través de una red). Le será familiar a cualquiera que haya trabajado con objetos `XMLHttpRequest`, sin embargo la nueva *API* proporciona un conjunto de características mucho más poderoso y flexible.

> Nota: Esta funcionalidad está disponible en *Web Workers*

## Uso y conceptos

*Fetch* proporciona definiciones génericas de los objetos `Request` y `Response` (además de otros aspectos relacionados con solicitudes de recursos a través de redes). Esto permitirá que sean utilizados donde sea que se necesiten, bien sea en *Service Workers*, *Cache API*, y otras funcionalidades similares que manejen o modifiquen solicitudes y respuestas de recursos, o cualquier otro caso de uso que requiera que se generen respuestas de forma prográmatica (es decir, a través de un programa de computación o de instructiones de programación personales).

También define conceptos relacionados tales como *CORS* y la semántica de las cabeceras de origen *HTTP*, supliendo sus definiciones específicas en cualquier otro contexto.

Para solicitar y obtener recursos, use el mêtodo `fetch()`. Este está implementado en múltiples interfaces, específicamente `Window` y `WorkerGlobalScope`. Lo que lo asegura su disponibilidad prácticamente en cualquier contexto en el que se requiera obtener recursos.

El método `fetch()` recibe un argumento obligatorio, la dirección del recurso que se quiera obtener. Devuelve un objeto de tipo `Promise` que resuelve como el objeto `Response` de dicha solicitud — tan pronto como el servidor responda — **aún si la respuesta del servidor es un estado de error *HTTP***.

También puede pasar como segundo argumento un objeto con opciones `init` (ver `Request`).

Una vez se haya obtenido un objeto `Response`, hay una serie de métodos disponibles para definir el cuerpo del contenido y como debe ser manejado.

Usted puede crear objetos de tipo `Request` and `Response` directamente utilizando los constructores `Request()` y `Response()`, sin embargo no es muy común hacerlo de esta manera. Lo más probable es que estos sean generados a tráves de funcionalidades de otras *API* (por ejemplo, `FetchEvent.respondWith()` de *Service Workers*).

### Diferencias con jQuery

La especificación de la API `fetch` difiere de `jQuery.ajax()` en dos aspectos principales:

- El objeto `Promise` devuelto por `fetch()` no será rechazado en el evento de un error *HTTP*, aún si la respuesta es un error *HTTP* 404 o 500. En su lugar será resuelto de forma normal (con status `ok` igual a `false`), y solo será rechazado de haber un fallo en la red o si algo evita que la solicitud finalice.

- `fetch()` no enviará *cross-origin cookies* a menos que se defina la opción `credentials` en el objeto de opciones que recibe el argumento `init`.

  - En abril de 2018, la especificación cambio la política de credenciales por defecto a *'same-origin'*. Los siguientes navegadores lanzaron una versión nativa desactualizada de la API `fetch` que fue actualizada en estas versiones: Firefox 61.0b13, Safari 12, Chrome 68.
  
  - Si usted está trabajando para versiones antiguas de estos navegadores, asegúrese de incluir `credentiasl: 'same-origin'` como opción dentro del argumento `init` en todos las solicitudes que puedan ser afectadas por `cookies/user login state`.

> Nota: Encuentre más información acerca de las funcionalidaes de la *Fetch API* en "Usando la *Fetch API*", y estudie los conceptos básicos en "Conceptos básicos de la *Fetch API*".

### Abortar una solicitud con 'fetch'

Los navegadores han empezado a incluir soporte experimental para las interfaces `AbortController` y `AbortSignal` (también conocidas como  la *Abort API*), las cuales permiten a operaciones como `fetch()` y `XHR` el ser abortadas si aún no han finalizado. Vea las páginas de las interfaces para conocer más detalles.

## Interfaces de la *Fetch API*

`fetch()`

El método `fetch()` empleado para adquirir un recurso.


`Headers`

Representa las cabeceras de los objetos *response/request*, permitiendo consultarlas y ejecutar distintas acciones dependiendo de sus resultados.


`Request`

Representa la solicitud de un recurso.


`Response`

Representa la respuesta a la solicitud de un recurso.
