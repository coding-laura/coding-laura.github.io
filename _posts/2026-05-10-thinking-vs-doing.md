---
layout: post
title: Thinking vs. Doing
description: What does a router do?
image: /post-images/code_screen.png
comments: True
tags: routing router forwarding
---


Sometime ago I got the interview question: *what is a router?*. So lets dig in and explain the concepts behind this technology.

When a packet reaches a router something decides where it goes next. That something is actually two separate processes, figuring out the best path (thinking), and actually moving the packet (doing). In networking terms these are called Control Plane and Data Plane.

If you are wondering why not just one process that does both, it's because of optimization. A router will forward millions of packets per second, running best path and forwarding the packet for every single packet is computationally expensive. Think of OSPF, running graphs, Djsktra's algorith, cost comparison, etc. So if that work were to happen once and the result isntalled into a lookup table, then the data plane can react in milliseconds.

Routing protocols (OSFP, BGP, IS-IS, etc.) all live in the control plane. They are the mechanism in which a router learns about a network topology and shares it with others. When a link comes up or goes down, the control plane recalculates the paths and updates the routing table which gets pushed to the data plane. This is what causes connectivity issues after a topology change, the data plane is working with outdated information until the control plane catches up.

Esentially we are working with two processes that have different purposes, the control plane is the rational process, and the data plane is all about speed. Routing protocols live in the control plane, forwarding happens in the data plane.

Routing is the process of determining the best path to a destination. This is control plane work. It produces a routing table.

Forwarding is the process of taking an incoming packet and sending it out the correct interface based on its destination. This is data plane work. It uses a forwarding table.

