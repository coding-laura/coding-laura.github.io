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

The data plane forwards millions of packets per second. At that throughput, you cannot afford to re-run a path calculation for every packet. Consider what OSPF actually does: it floods LSAs, builds a link-state database, runs Dijkstra's SPF algorithm, and computes costs across the entire topology. That work happens once (or when the topology changes), the result gets installed into a fast lookup table, and the data plane queries that table in microseconds.

Separate the two planes and you get both intelligence and speed. Combine them and you get neither.

### What lives where

Routing protocols like OSPF, BGP, IS-IS, etc. all live in the control plane. They are the mechanism by which a router builds its view of the network and shares that view with its neighbors. When a link goes down, the control plane detects the change, recalculates affected paths, and pushes the updated routing table to the data plane.

The gap between when the topology changes and when the data plane catches up is called **convergence time**. It's why you see brief packet loss after a link failure even on a well-designed network. The data plane is forwarding on stale information while the control plane does its work. There are many methods to try and minimize convergence time because of that little disconnect between the two processes.

> [!NOTE]
> Worth noting: there's also a **Management Plane** — SSH, SNMP, NETCONF — which 
> handles device configuration and monitoring. It doesn't directly influence 
> forwarding, but it's how you interact with the other two.


If you are wondering why not just one process that does both, it's because of optimization. A router will forward millions of packets per second, running best path and forwarding the packet for every single packet is computationally expensive. Think of OSPF, running graphs, Djsktra's algorith, cost comparison, etc. So if that work were to happen once and the result isntalled into a lookup table, then the data plane can react in milliseconds.

Routing protocols (OSFP, BGP, IS-IS, etc.) all live in the control plane. They are the mechanism in which a router learns about a network topology and shares it with others. When a link comes up or goes down, the control plane recalculates the paths and updates the routing table which gets pushed to the data plane. This is what causes connectivity issues after a topology change, the data plane is working with outdated information until the control plane catches up.

Esentially we are working with two processes that have different purposes, the control plane is the rational process, and the data plane is all about speed. Routing protocols live in the control plane, forwarding happens in the data plane.

Routing is the process of determining the best path to a destination. This is control plane work. It produces a routing table.

Forwarding is the process of taking an incoming packet and sending it out the correct interface based on its destination. This is data plane work. It uses a forwarding table.

So, **what is a router?** A router is a device that runs two parallel operations: a **control plane** that builds and maintains a view of the network, and a **data plane** that forwards packets at line rate based on what the control plane computed. One thinks, one does; and keeping them separate is what makes both possible.
