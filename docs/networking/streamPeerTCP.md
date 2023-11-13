---
parent: networking
title: streamPeerTCP
layout: default
nav_order: 3
toc: true
---
[SocketError]: /docs/networking/netSocket.html#socket-error-enum
[Status]: /docs/networking/streamPeerTCP.html#connection-status-enum
[IpAddress]: /docs/networking/IpAddress.html
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

| param name               | param type                                     |
|:-------------------------|:-----------------------------------------------|
|address                   |[IpAddress]    |
|port                      |int                                             |

## get the connection status of the streamPeerTCP object

to get the connection status of the tcpClient you just have to call the GetStatus function

```cs
using luna;
internal class Start : Node
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
|[SocketError]    |[Bind](/docs/networking/streamPeerTCP.html#socketerror-bindint-port-ipaddress--host)(int Port, [IpAddress]  Host)        |
|[SocketError]  |[ConnectToHost](/docs/networking/streamPeerTCP.html#socketerror-connecttohostipaddress--hostint-port)([IpAddress] Host,int Port)|
|[SocketError]    |Poll()                                |
|[Status] |GetStatus()                           |
|[IpAddress]|GetConnectedHost()|
|int|GetConnectedPort()|
|int|GetLocalPort()|
|void|DisconnectFromHost()|
|[SocketError] |PutData(byte[] Data)|
|[SocketError] |PutPartialData(byte[] Data,out int BytesSent)|
|[SocketError] |GetData(byte[] Buffer)|
|[SocketError] |GetPartialData(byte[] Buffer,out int Received)|
|int|GetAvailableBytes()|

## method descriptions

### [SocketError] Bind(int Port, [IpAddress]  Host)

> Opens the TCP socket, and binds it to the specified local address.
> This method is generally not needed, and only used to force the subsequent call 
> to connect_to_host to use the specified host and port as source address.This can be desired in some NAT punchthrough techniques,
> or when forcing the source network interface.

### [SocketError] ConnectToHost([IpAddress]  Host,int port)
> Connects to the specified host:port pair. A hostname will be resolved if valid.

{: .note}
port is between 0-65536 inclusive!

