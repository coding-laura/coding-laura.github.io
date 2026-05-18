---
layout: post
title: A Belief System
description: Before a router can forward a single packet, it needs to know what it believes about the network.
image: /post-images/rack_switches.png
comments: True
tags: routing router RIB control-plane interview
---


When a router boots, it knows only its directly connected interfaces; the rest of the network must be learned through routing protocols, neighbor updates, or static configuration. 

That learning process is the control plane’s entire job. Whatever each source offers as a route gets consolidated into one structure: the **Routing Information Base (RIB)**.

The RIB is the control plane's source of truth about the network. Not a cache, not a snapshot; it's the living record of everything the router currently believes about how to reach every destination it knows about.

### What the RIB actually is

The RIB is a table. Each entry represents a destination prefix and what the router knows about reaching it - where to send traffic, how that route was learned, and how much to trust it.

It can hold multiple routes to the same destination simultaneously. A static route, an OSPF route, and a BGP route might all claim to know the best path to 10.10.10.0/24 at the same time. The RIB holds all of them, evaluates them, and selects a winner based on which source the router trusts most.

That selection process and what happens to the winning route are topics for another time. For now, the important thing is the structure itself: one table, all sources, one place where the router's understanding of the network lives.

```text
show ip route

O     10.10.10.0/24  [110/20]  via 192.168.1.1,  Ethernet1
S     10.20.20.0/24  [1/0]     via 192.168.1.2,  Ethernet1
C     192.168.1.0/24           is directly connected, Ethernet1
```

Every line is a belief. `O` - OSPF told me this. `S` - a neteng told me this. `C` - I can see this directly. The RIB is the sum of everything the control plane currently knows.

### Why a single source of truth matters

The RIB being one consolidated table isn't an implementation detail — it's the design.

Routing protocols don't forward packets. OSPF doesn't touch the data plane. BGP doesn't touch the data plane. Each protocol maintains its own internal state and its own view of the network, but none of them are authoritative on their own. The RIB is the step where all of that gets reconciled into a single, consistent picture that the rest of the router can act on.

Without it, the data plane would have to query multiple protocol databases simultaneously and resolve conflicts at forwarding time — at millions of packets per second. The RIB exists so that work happens once, in the control plane, before any packet arrives.

### The RIB is not what forwards packets

This is worth stating clearly: the data plane does not use the RIB.

The RIB lives in the control plane. It's built for decision-making — flexible, multi-source, complete. The data plane needs something different: a structure optimized purely for fast lookup, stripped of everything except what's needed to forward a packet.

That structure is the FIB. The RIB produces it. They're not the same thing, and the gap between them is more interesting than it sounds (maybe another post).

### Back to the interview 📝

*"What is the RIB?"*

The RIB is the control plane's single source of truth about the network. It consolidates routes from every source (connected interfaces, static configuration, routing protocols) into one table, evaluates them, and maintains the router's current best understanding of how to reach every known destination.

It's not a forwarding table. It's a knowledge base. The data plane works from a derivative of it, the FIB, which is optimized for speed rather than completeness.

If the RIB is wrong, everything downstream is wrong. It's the foundation.