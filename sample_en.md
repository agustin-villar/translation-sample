# Fetch API

The Fetch API provides an interface for fetching resources (including across the network). It will seem familiar to anyone who has used `XMLHttpRequest`, but the new API provides a more powerful and flexible feature set.

> Note: This feature is available in Web Workers

## Concepts and usage

Fetch provides a generic definition of `Request` and `Response` objects (and other things involved with network requests). This will allow them to be used wherever they are needed in the future, whether it's for service workers, Cache API, and other similar things that handle or modify requests and responses, or any kind of use case that might require you to generate your responses programmatically (that is, the use of computer program or personal programming instructions).

It also defines related concepts such as CORS and the HTTP Origin header semantics, supplanting their separate definitions elsewhere.

For making a request and fetching a resource, use the `fetch()` method. It is implemented in multiple interfaces, specifically `Window` and `WorkerGlobalScope`. This makes it available in pretty much any context you might want to fetch resources in.

The `fetch()` method takes one mandatory argument, the path to the resource you want to fetch. It returns a `Promise` that resolves to the `Response` to that request — as soon as the server responds with headers — **even if the server response is an HTTP error status**. You can also optionally pass in an `init` options object as the second argument (see `Request`).

Once a `Response` is retrieved, there are a number of methods available to define what the body content is and how it should be handled.

You can create a request and response directly using the `Request()` and `Response()` constructors, but it's uncommon to do this directly. Instead, these are more likely to be created as results of other API actions (for example, `FetchEvent.respondWith()` from service workers).

### Differences from jQuery

The `fetch` specification differs from `jQuery.ajax()` in three main ways:

- The Promise returned from fetch() won't reject on HTTP error status even if the response is an HTTP 404 or 500. Instead, it will resolve normally (with ok status set to false), and it will only reject on network failure or if anything prevented the request from completing.

- fetch() won't send cross-origin cookies unless you set the credentials init option (to include).
  
  - In April 2018, the spec changed the default credentials policy to 'same-origin'. The following browsers shipped an outdated native fetch, and were updated in these versions: Firefox 61.0b13, Safari 12, Chrome 68.
  
  - If you are targeting older versions of these browsers, be sure to include credentials: 'same-origin' init option on all api requests that may be affected by cookies/user login state.

> Note: Find out more about using the Fetch API features in Using Fetch, and study concepts in Fetch basic concepts.

### Aborting a fetch

Browsers have started to add experimental support for the `AbortController` and `AbortSignal` interfaces (aka The Abort API), which allow operations like Fetch and XHR to be aborted if they have not already completed. See the interface pages for more details.

## Fetch Interfaces

`fetch()`

The `fetch()` method used to fetch a resource.


`Headers`

Represents response/request headers, allowing you to query them and take different actions depending on the results.


`Request`

Represents a resource request.


`Response`

Represents the response to a request.
