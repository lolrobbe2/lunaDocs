--- 
title: IpAddress
layout: default
parent: Ip
grand_parent: networking
---

# IpAddress

IpAddress is the object that contains the binary notation of an Ipv4 or Ipv6 address.
This class is used with almost every networking component.

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## creating a IpAddress object.

### create empty
```cs
using Luna;

public class start : Node
{
    IpAddress tcpClient = new IpAddress();
}
```

### create initialized
```cs
using Luna;

public class start : Node
{
    IpAddress tcpClient = new IpAddress("127.0.0.1");
}
```
```cs
using Luna;

public class start : Node
{
    IpAddress tcpClient = new IpAddress(127,0,0,1,false);
}
```

# methods
## methods overview

| return type                                                        | method                               |
|:-------------------------------------------------------------------|:-------------------------------------|
|void |Clear()|