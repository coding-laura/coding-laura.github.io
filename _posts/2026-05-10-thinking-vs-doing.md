---
layout: post
title: Thinking vs. Doing
description: What does a router do?
image: /post-images/code_screen.png
comments: True
tags: routing router forwarding
---


**What is a router?** a question that sounds trivial until you're in an interview and realize the answer has layers 😏. Let's unpack it properly.

When a packet hits a router, two separate processes decide its fate: figuring out the best path, and actually moving the packet. In networking terms, these are the **Control Plane** (thinking) and the **Data Plane** (doing).

### Why split them at all?

Because they have fundamentally different performance requirements.

The data plane on a modern router forwards hundreds of millions to billions of packets per second. An OSPF SPF recalculation on a mid-sized topology can take tens to hundreds of milliseconds - and a full BGP reconvergence, seconds. At that forwarding scale, even a 100ms delay in forwarding decisions would mean dropping massive amounts of traffic while the router is still thinking (aka calculating the path).

Instead, you run the calculation once, install the result, and let the data plane do what it does: look up and forward packets at line rate - meaning the router can process traffic at the full speed of its interfaces (100G, 400G, etc.) without dropping packets due to processing limitations.

> [!NOTE]
> Consider what OSPF actually does: it floods LSAs, builds a link-state 
> database, runs Dijkstra's SPF algorithm, and computes costs across the 
> entire topology. That work happens once (or when the topology changes), 
> the result gets installed into a fast lookup table, and the data plane 
> queries that table in microseconds. 

Separate the two planes and you get both intelligence and speed. Combine them and you get neither.

### What lives where

Routing protocols like OSPF, BGP, IS-IS, etc. all live in the control plane. They are the mechanism by which a router builds its view of the network and shares that view with its neighbors. When a link goes down, the control plane detects the change, re-calculates affected paths, and pushes the updated routing table to the data plane.

The gap between when the topology changes and when the data plane catches up is called **convergence time**. It's why you see brief packet loss after a link failure even on a well-designed network. The data plane is forwarding on stale information while the control plane does its work. There are many methods to try and minimize convergence time because of that little disconnect between the two processes.

> [!NOTE]
> Worth noting: there's also a **Management Plane** (SSH, SNMP, NETCONF) which 
> handles device configuration and monitoring. It doesn't directly influence 
> forwarding, but it's how you interact with the other two.


### Routing vs. forwarding (the precise distinction)

These terms get used interchangeably in conversation, but they mean different things:

- **Routing**: determining the best path to a destination. Control plane work. Produces a routing table (RIB).
- **Forwarding**: taking an incoming packet and sending it out the correct interface. Data plane work. Uses a forwarding table (FIB).

When someone says "the router routes packets," they're being technically loose. The router *forwards* packets based on routes it already computed. 

### Back to the interview 📝

So, **what is a router?** A router is a device that runs two parallel operations: a **control plane** that builds and maintains a view of the network, and a **data plane** that forwards packets at line rate based on what the control plane computed. One thinks, one does; and keeping them separate is what makes both possible.
