---
parent: networking
title: streamPeerTCP
layout: default
nav_order: 3
toc: true
---
[int]: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types

[SocketError]:  netSocket.html#socket-error-enum
[Status]: #connection-status-enum
[IpAddress]: IpAddress.html

[Bind]: #socketerror-bindint-port-ipaddress--host
[ConnectToHost]: #socketerror-connecttohostipaddress--hostint-port
[Poll]: #socketerror-poll
[GetStatus]: #status-getstatus
[GetConnectedHost]: #ipaddress-getconnectedhost
[GetConnectedPort]: #ipaddress-getconnectedhost
[GetLocalPort]: #int-getlocalport
[DisconnectFromHost]: #void-disconnectfromhost
[PutData]: #socketerror-putdatabyte-data
[PutPartialData]: #socketerror-putpartialdatabyte-dataout-int-bytessent
[GetData]: #socketerror-getdatabyte-buffer
[GetPartialData]: #socketerror-getpartialdatabyte-bufferout-int-received
[GetAvailableBytes]: #[IpAddress]-getavailablebytes
# streamPeerTCP

streamPeerTCP is a lowlevel networking component inside the engine and is built upon the netSocket module
making it very versetile but not as versetile as the netSocket module

the streamPeerTCP module can be used in 2 ways as a tcp client or as a TCPServer connection.


<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## creating a streamPeerTCP object.
```cs
using Luna;

public class start : Node
{
    streamPeerTCP tcpClient = new streamPeerTCP();
}
```

## connection Status enum 
``` cs
public enum Status
{
    STATUS_NONE,
    STATUS_CONNECTING,
    STATUS_CONNECTED,
    STATUS_ERROR,
};
```

## connecting to a host IpAddress
```cs
using Luna;

public class start : Node
{
    streamPeerTCP tcpClient = new streamPeerTCP();

    override public void Ready()
    {
        IpAddress Address = Ip.ResolveHostnameAddress("example.com", Ip.Type.TYPE_IPV6);
        tcpClient.ConnectToHost(Address, 80);
    }
}
```
### params


## get the connection status of the streamPeerTCP object

to get the connection status of the tcpClient you just have to call the GetStatus function

```cs
using luna;
[IpAddress] public class Start : Node
{
    streamPeerTCP tcpClient = new streamPeerTCP();

    override public void Process(ulong delta)
    {
        tcpClient.Poll();
        if (tcpClient.GetStatus() == Status.STATUS_CONNECTED )
        {
            Log.Info("Tcp CLient succesfully connected to host!");
        }
    }
}
```

# methods

## methods overview

| return type                                                        | method                               |
|:-------------------------------------------------------------------|:-------------------------------------|
|[SocketError]                                                       |[Bind] ([int] Port, [IpAddress]  Host)  |
|[SocketError]                                                       |[ConnectToHost] ([IpAddress] Host,[int] Port)|
|[SocketError]    |[Poll] ()                    |
|[Status] |[GetStatus] ()                           |
|[IpAddress]|[GetConnectedHost] ()|
|[int]|[GetConnectedPort] ()|
|[int]|[GetLocalPort] ()|
|void|[DisconnectFromHost] ()|
|[SocketError] |[PutData] (byte[] Data)|
|[SocketError] |[PutPartialData] (byte[] Data,out [int] BytesSent)|
|[SocketError] |[GetData] (byte[] Buffer)|
|[SocketError] |[GetPartialData] (byte[] Buffer,out [int] Received)|
|[int]|[GetAvailableBytes] ()|

## method descriptions

### [SocketError] Bind([int] Port, [IpAddress]  Host)

> Opens the TCP socket, and binds it to the specified local address.
> This method is generally not needed, and only used to force the subsequent call 
> to ConnectToHost to use the specified host and port as source address.This can be desired in some NAT punchthrough techniques,
> or when forcing the source network interface.
>
> | param name               | param type                                     |
> |:-------------------------|:-----------------------------------------------|
> |port                      |[int]                                           |
> |Host                      |[IpAddress]                                     |


### [SocketError] ConnectToHost([IpAddress]  Host,[int] port)
> Connects to the specified host:port pair.
>
> | param name               | param type                                     |
> |:-------------------------|:-----------------------------------------------|
> |Host                      |[IpAddress]                                     |
> |port                      |[int]                                           |

{: .note}
port is between 0-65536 inclusive!


### [SocketError] Poll() 
> Poll the socket, updating its state. see [GetStatus].

### [Status] GetStatus()
> returns the current [Status] of the socket

### [IpAddress] GetConnectedHost()
> returns the IpAdress of the connected host.

### [int] GetConnectedPort()
> returns the port of the connected host

### [int] GetLocalPort()
> returns the native/local port.

### void DisconnectFromHost()
> disconnects from the currently connected host.

### [SocketError] PutData(byte[] Data)
> Sends a chunk of data through the connection, 
> blocking if necessary until the data is done sending. This function returns a [SocketError] code.
>
> | param name               | param type                                     |
> |:-------------------------|:-----------------------------------------------|
> | data                     |byte[]                                          |

### [SocketError] PutPartialData(byte[] Data,out [int] BytesSent)
> Sends a partial chunk of data through the connection.
> This function returns an [SocketError] code.
>
> | param name               | param type                                     |
> |:-------------------------|:-----------------------------------------------|
> | data                     | byte[]                                         |
> | BytesSent                | out [int]                                        |

### [SocketError] GetData(byte[] Buffer)
> Gets data and fills the Buffer Array (blocking)
>
> | param name               | param type                                     |
> |:-------------------------|:-----------------------------------------------|
> | buffer                   | byte[]                                         |

### [SocketError] GetPartialData(byte[] Buffer,out [int] Received)
> Gets partial data and fills the Buffer Array. (non-blocking)
>
> | param name               | param type                                     |
> |:-------------------------|:-----------------------------------------------|
> | buffer                   | byte[]                                         |
> | Received                 | out [int]                                        |

### [int] GetAvailableBytes()
> Returns the currently available bytes to read.