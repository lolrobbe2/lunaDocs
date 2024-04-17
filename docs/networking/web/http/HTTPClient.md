--- 
title: HTTP client
layout: default
grand_parent: networking
parent: web
has_children: false
nav_order: 1
---

[streamPeerTCP]: ../../streamPeerTCP.html
[MDNDocs]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods
# HTTP client
The HTTP client is a high level networking component inside the engine build on top of the [streamPeerTCP] component.

## creating a streamPeerTCP object.
```cs
using Luna;

public class start : Node
{
    HTTPClient HTTPClient = new HTTPCLient();
}
```

## http method
for more information see [MDNDocs]
```cs
public enum Method
{
    GET,
    POST,
    PUT,
    HEAD,
    DELETE,
    PATCH, 
    OPTIONS,
    CONNECT,
    TRACE,
};
```