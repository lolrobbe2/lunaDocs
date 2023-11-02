---
parent: networking
title: streamPeerTCP
layout: default
nav_order: 3
---

# streamPeerTCP

streamPeerTCP is a lowlevel networking component inside the engine and is built upon the netSocket module
making it very versetile but not as versetile as the netSocket module

the streamPeerTCP module can be used in 2 ways as a tcp client or as a TCPServer connection.

# creating a streamPeerTCP object.
```cs
using Luna;

public class start : Node
{
    streamPeerTCP tcpClient = new streamPeerTCP();
}
```

# connection Status enum 
``` cs
public enum Status
{
    STATUS_NONE,
    STATUS_CONNECTING,
    STATUS_CONNECTED,
    STATUS_ERROR,
};
```

# connecting to a host IpAddress
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

