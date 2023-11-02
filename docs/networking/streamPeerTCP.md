---
parent: networking
title: streamPeerTCP
layout: default
nav_order: 3
toc: true
---
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
|address                   |[IpAddress](/docs/networking/IpAddress.html)    |
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

## methods

| return type                                                        | method                               |
|:-------------------------------------------------------------------|:-------------------------------------|
|[SocketError](/docs/networking/netSocket.html#socket-error-enum)    |Bind(int Port, [IpAddress](/docs/networking/IpAddress.html)  Host)        |
|[SocketError](/docs/networking/netSocket.html#socket-error-enum)    |ConnectToHost([IpAddress](/docs/networking/IpAddress.html) Host,int Port)|
|[SocketError](/docs/networking/netSocket.html#socket-error-enum)    |Poll()                                |
|[Status](/docs/networking/streamPeerTCP.html#connection-status-enum)|GetStatus()                           |
|[IpAddress](/docs/networking/IpAddress.html)|GetConnectedHost()|
|int|GetConnectedPort()|
|int|GetLocalPort()|
|void|DisconnectFromHost()|
|[SocketError](/docs/networking/netSocket.html#socket-error-enum) |PutData(byte[] Data)|
|[SocketError](/docs/networking/netSocket.html#socket-error-enum) |PutPartialData(byte[] Data,out int BytesSent)|
