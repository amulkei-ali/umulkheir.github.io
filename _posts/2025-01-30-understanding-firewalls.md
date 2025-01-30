---

title: 'Understanding Firewalls.'
date: 2025-01-30 17:55 +0300
categories: [linux,firewall]
tags: [firewall,linux]
---


## What is a Firewall ?

Imagine your computer or server is like a house. A firewall is like a security guard standing at the front gate (your network connection) of your house. The job of the security guard is to decide which people (data) are allowed into your house and which ones should stay out. The security guard uses rules (or instructions) to make these decisions.

For example:

  * The guard might let in people carrying packages from the post office (web traffic, email).
  
  * But, the guard might stop suspicious people (bad data, hackers) trying to sneak in.

  In short, a firewall is a tool that helps protect your system from unwanted or harmful traffic by filtering what comes in or out based on rules.


  ## Common Firewall Technologies In Linux:

     * iptables,
     * nftables,
     * firewalld,
     * UFW (Uncomplicated firewall)


  ## iptables and nftables as the "engine"   

 -iptables and nftables are the core technologies that define the rules for controlling network traffic. They are responsible for:
   * Deciding which data can go in and out of the system.
   * Blocking bad traffic (like hackers) and letting good traffic (like web pages) in.


  -iptables is the older one and nftables is the newer, more efficient version.


  ## UFW and Firewalld as "Front-ends"

Think of UFW and Firewalld as helper tools that make it easier to set up and manage your firewall rules without 
you needing to write everything manually.

These tools are not the ones that actually do the 'blocking'or 'allowing' of the traffic. Instead, they work with iptables and nftables that do the actual work.