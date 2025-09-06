---
layout: post
title: The Algorithm That Saved Ethernet from Loops
date: 2025-09-04 17:15 +0300
tags: [Networking, protocols]
categories: [STP, Root Bridge, Bridge Id, Designated Port]
---


## Spanning Tree Protocol (STP)

if you've ever spent time in networking, you know how terrifying loops can be. One wrong cable , one unmannaged switch plugged in under the desk, and suddenly the whole network feels like it's on fire. Broadcast storms spread, bandwidth disappear, and users are left asking, "Why is the Wi-Fi slow?"

This is where STP comes in. It's one of those behind the scenes heroes that doesn't get much attention but quietly keeps our networks alive.

## History of STP

Back in the early days of Ethernet, most networks used Hubs. Hubs weren't smart. They just repeated every bit they received and blasted it out of every port. That meant the whole networks was basically one big collision domain. Loops weren't the main issue then, collision and inefficiency were.

Things changed when Switches replaced Hubs. Switches were smarter. They could learn MAC addresses and forward traffic only where it needed to go. This made networks much faster, but it also intruduced a new problem. "Layer 2 Loop". In a redundant topology, a single broadcast packet could loop endlessly crippling the nework.

That’s when Dr.Radia Perlman, working at Digital Equipment Corporation in 1985, came up with the solution. Her algorithm, known as the Spanning Tree Protocol, gave switches a way to prevent loops without sacrificing redundancy. Thanks to her work, Ethernet could grow into the reliable networks we depend on today.

## What STP Does

STP is a loop prevention protocol for switches. It makes sure there's only one active path between devices, even if multiple physical links exist.

The extra links aren't wasted though, they are kept in standby. If the actice path fails, STP brings a backup path online. That balance between stability and redundancy is what makes it so important.

## How STP Works

1. #### Root Bridge Election
Every switch thinks it’s the boss at first. They send out BPDUs (special hello messages), and the one with the lowest Bridge ID becomes the root bridge—the reference point for the whole network.

#### How is Bridge ID calculated?
The Bridge ID is made up of two values:
* Bridge Priority (default: 32,768, but you can change it)
* MAC Address of the switch

Formula:
```note
Bridge ID = Bridge Priority + MAC Address
```
If two switches have the same priority, the one with the lowest MAC address wins. In practice, engineers usually lower the priority on the switch they want to be the root bridge.

2. #### Finding Best Paths
Each switchcalculates the shortest way to reach the root bridge. This is based on bath cost, which depends on link speed (faster links = lower cost)

3. #### Port Roles
 * Root Port(RP): The best path a switch has towards the root bridge
 * Designated Port(DP): The forwading port chosen for a network segment
 * Blocked Port: A backup link that stays silent to prevent loops

4. #### Failover
If the main link fails, STP activates a previous blocked port hence keeping the network running

### Example
Imagine three switches connected in a triangle. Without STP, a broadcast packet could loop forever bringing the network down. With STP, one of those links is put in a blocked state. Traffic flows smoothly and if a life link fails, the blocked one opens up to take over.
This is why STP is often described as creating a "Loop-free logical tree"

## Different Versions of STP

Over time, STP has evolved:
* STP (802.1D): The original, but slow to react when links change.
* RSTP (802.1w): Rapid Spanning Tree Protocol — much faster convergence.
* MSTP (802.1s): Multiple STPs for multiple VLANs.
* PVST+ (Cisco): A Cisco enhancement that runs STP separately per VLAN.
Each was designed to make recovery faster and networks more flexible.

### Why You Should Care
Even with modern technologies like LACP and SDN, Spanning Tree Protocol is still very much alive. If you work in networking, whether it’s in a data center or a small enterprise environment, chances are you’ll run into it at some point. The truth is, STP isn’t just “legacy tech” — it’s still the safety net that prevents loops from taking down entire networks.

And that’s why you should learn it. A solid understanding of STP helps you troubleshoot faster, design more resilient topologies, and avoid mistakes that could cause serious downtime. Misconfigured STP can do more than slow things down — it can bring an entire network to its knees. Knowing how it works gives you an edge as an engineer, because when things break (and they will), you’ll know exactly where to look and how to fix it.

I hope you enjoyed reading this!📖✨

Take good care 🤝