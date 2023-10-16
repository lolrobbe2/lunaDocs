--- 
title: net socket
layout: default
parent: networking
---

# netSocket

netSocket is the most lowlevel networking component inside the engine and is thus the most versatile.
But that means it is also the most complected to work with

> content:
> - [supported protocols / protocol enum](#netsocket)
> - [creating a netSocket object](#creating-a-netsocket-object)
> - [binding a socket to a port](#binding-a-socket-to-a-port)

# supported protocols / protocol enum
the netSocket class currently only support 2 network protocols TCP(Transmission Control Protocol) and UDP(Universal Datagram Protocol).

```cs
 public enum Protocol
 {
     TCP,
     UDP
 }

```

# creating a netSocket object
to use the netSocket you need to create a netsocket object.

```cs
using Luna;

internal class start : Node
{
    NetSocket socket = new NetSocket();
}
```

# binding a socket to a port
to bind a socket to a certain port you need to call the Bind function on that socket
```cs
using Luna;

internal class start : Node
{
    NetSocket socket = new NetSocket();
    override public void Ready()
    {
	    socket.Bind(8080, "*", Protocol.TCP);
    }
}
```

{: .warning}
> socket binding to a custom ip address is not working at the moment !

{: .note}
> bind can only be called once on a socket!

## params:

| param name | param type  |
|:-----------|:------------|
| port       |UInt16       |
| bindAddress|String       |
| protocol   |Enum protocol|

# listening on a socket
to listen for incomming connections
call the Listen function

```cs
using Luna;

internal class start : Node
{
    NetSocket socket = new NetSocket();
    override public void Ready()
    {
	    socket.Listen(350);
    }
}
```
## params:

| param name               | param type  |
|:-------------------------|:------------|
| max incomming connections| int         |

{: .warning}
> a socket must be bound to a port and a corresponding protocol before listen is called otherwise an error will be thrown and the socket might become invalid.

{: .note} 
> max incomming connections must be between 200 and 65536 (2^16) otherwise the value will be corrected and an error will be thrown.

# accepting incoming connections:
after having bound the connection and called listen on the socket you can start to accept incoming connections.

```cs
using Luna;

internal class start : Node
{
    NetSocket socket = new NetSocket();
    override public void Ready()
    {

    }
}
```