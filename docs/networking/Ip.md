--- 
title: Ip
layout: default
parent: networking
has_children: true
nav_order: 1
---

# Ip (internet protocol)
the Ip static class is a collection of some very helpful helper functions.

## dns/hostname resolving (blocking)
hostname resolving can be done like this:

1) resolve as a string (127.0.0.1)
```cs
   string address = Ip.ResolveHostname("google.com");
```

2) resolve as an [IpAddress](IpAddress.html) object
```cs
   IpAddress address = Ip.ResolveHostnameAddress("google.com");
```

{: .warning}
> this way of resolving a host name is blocking I.E it waits untill the hostname is resolved.
> for non blocking options [see](#dns-resolving-non-blocking)

## dns/hostname resolving (non blocking)

