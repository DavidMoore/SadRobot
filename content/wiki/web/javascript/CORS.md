---
title: Cross-Origin Resource Sharing (CORS)
---
#Cross-Origin Resource Sharing (CORS)

## What problem does CORS solve?

For security reasons, browsers can't make cross-domain requests. They are limited to the same-origin.

For example, website http://www.foo.com/ cannot access data from http://api.bar.com, because the origin differs (in this case, the domain name).

Neither can https://www.foo.com access data from http://www.foo.com, because the scheme differs. The same can be said of differ port e.g. http://www.foo.com and http://www.foo.com:8080.

This is a big problem for a world where applications talk to internal and external APIs on different hosts.

There have been workarounds such as JSON-P, but they have limitations.

## CORS Request

The requesting client adds an `Origin` HTTP header, which cannot be altered by the user.

In almost all cases the browser will add this automatically. Some browsers will not add the `Origin` header if the request is already being made to the same origin.

## CORS Response

The CORS response will come with one or more Access-Control-* header(s).


Header | Value | Description
-------|
`Access-Control-Allow-Origin`| `*`` to allow all, or the Origin from the request|Required
`Access-Control-Allow-Credentials` |`true`|Set if cookies should be included.
`Access-Control-Expose-Headers` | Comma-separated list of allowed headers| Lists headers the client has access to over the base headers


### Base headers

The requesting client automatically have access to the following headers, regardless of the `Access-Control-Expose-Headers` setting:

* Cache-Control
* Content-Language
* Content-Type
* Expires
* Last-Modified
* Pragma

## Preflight Request

Outside the simplest or cross-origin requests, the browser will transparently issue a preflight request to the server to check if it's allowed to make the request it's intending.

This is by making an OPTIONS request to the server. If the server responds allowing the requested options, then the originally intended request will then be passed through.

Header|Value|Description
-|
Access-Control-Request-Method|Requested method|e.g. GET, POST, PUT, DELETE, HEAD, PATCH|
Access-Control-Request-Headers|List of request headers|Comma-separated list of non-standard headers to be included in the request

The server response can be cached, so that preflight requests aren't required for each subsequent request.

Example:

```
OPTIONS /cors HTTP/1.1
Origin: http://api.bob.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: X-Custom-Header
Host: api.alice.com
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0...
```

## Preflight Response

Header|Value|Description
-|
Access-Control-Allow-Origin|* or the requesting Origin|Required
Access-Control-Allow-Methods|Allowed methods|A list of allowed methods
Access-Control-Allow-Headers|Allowed headers|List of allowed headers (not just limited just to the headers in the Access-Control-Request-Headers request)
Access-Control-Allow-Credentials||
Access-Control-Max-Age|Cacheable for x seconds|Allows the preflight response to be cached

Example response:

```
Access-Control-Allow-Origin: http://api.bob.com
Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: X-Custom-Header
Content-Type: text/html; charset=utf-8
```

If the request is denied, then no CORS headers are sent back, and the browser will fail the request, resulting in an error like so:

XMLHttpRequest cannot load http://api.beta.com. Origin http://api.alpha.com is not allowed by Access-Control-Allow-Origin.


# References

[CORS Tutorial @ HTML5 Rocks](http://www.html5rocks.com/en/tutorials/cors/)
[CORS Spec @ w3.org](http://www.w3.org/TR/cors/)
