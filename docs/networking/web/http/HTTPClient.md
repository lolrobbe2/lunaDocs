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
[SocketError]:  ../../netSocket.html#socket-error-enum
[string]: https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/
[int]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types
[void]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/void
[bool]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/bool
[Status]: #http-status

[ConnectToHost]: #socketerror-connecttohoststring-hostint-port--80
[HTTPClient.Method]: #methods
[Request]: #void-requesthttpclientmethod-method-string-destination-json-headers-string-body
[HasResponse]: #bool-hasresponse
[Poll]: #socketerror-poll
[GetStatus]: #status-getstatus
[GetHeaders]: #json-getheaders
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
this enumeration shows the available http methods,
for more information see [MDNDocs].
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

## http status
current status of the HTTPClient
```cs
public enum Status
{
    STATUS_NONE,
    STATUS_CONNECTING,
    STATUS_CONNECTED,
    STATUS_ERROR,
    STATUS_REQUESTING,
    STATUS_RECEIVING,
    STATUS_DONE
};
```

# methods

## methods overview

| return type                                                        | method                               |
|:-------------------------------------------------------------------|:-------------------------------------|
|[SocketError]                                                       | [ConnectToHost]                      |
|[void]                                                              | [Request]                            |
|[bool]                                                              | [HasResponse]                        |
|[SocketError]                                                       | [Poll]                               |
|[Status]                                                            | [GetStatus]                          |
|[byte][]                                                            | [GetBody]                            |
|JSON                                                                | [GetHeaders]                         |

### [SocketError] ConnectToHost([string] Host,int port = 80)
> connects the http client to a host http serve
> 
> | param name | param type  |
> |:-----------|:------------|
> |Host        |[string]     |
> |Port        |[int]        |

{: .note}
will also connect to non http servers, it just won't be able to know whath to do with the HTTP response.

### [void] Request([HTTPClient.Method] Method, [string] Destination, Json Headers, [string] body = "")
> sends an HTPP request to the connected host.
>
> | param name | param type        |
> |:-----------|:------------------|
> |Method      |[HTTPClient.Method]|
> |Destination |[string]           |
> |Headers     |JSON               |
> |body        |[string]           |

### [bool] HasResponse()
> checks the HTTPClient if a response is available.



### [SocketError] Poll()
> Polls the HTPPClient for incomming response.

{: .warning}
as soon a the http client is receiving a response [HasResponse] will return true.
but at this point the body might not have been fully received. To know when the response body has not been fully received Status.STATUS_RECEIVING use the [GetStatus] function.

### [Status] GetStatus()
>  function to get the current HTTPClient see [Status].

### [byte][] GetBody()
> returns the respnse body as a [byte] array.

### Json GetHeaders()
> returns the response headers as a JSON object.