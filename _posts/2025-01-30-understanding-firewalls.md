---
layout: post
title: 'Understanding Firewalls 🛡️'
date: 2025-01-30 17:55 +0300
tags: [firewall,linux]
categories: [security]

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


  -iptables is the older version, more complex, but still widely used while nftables is the new, modern version that does the same job but is faster and  simpler.


## UFW and Firewalld as "Front-ends"

Think of UFW and Firewalld as helper tools that make it easier to set up and manage your firewall rules without 
you needing to write everything manually.

These tools are not the ones that actually do the 'blocking'or 'allowing' of the traffic. Instead, they work with iptables and nftables that do the actual work.


##  How UFW Works (Uncomplicated Firewall):
 UFW is like a simplified tool that lets you easily add or remove firewall rules with simple commands, like “Allow web traffic” or “Block this IP address”.
 In the background, UFW is actually using iptables or nftables to apply those rules. If you're using a modern system, UFW may be interacting with nftables, but on older systems, it typically works with iptables.
 Let’s say you run this command 

 ```bash
 sudo ufw allow http
 ```
 What actually happens is that UFW tells iptables or nftables to open port 80, the port used for HTTP (web traffic). So, UFW simplifies the process of setting up that rule for you.

 WHEN DO YOU USE IT ?

 When You Want Simplicity:
If you want a basic but effective firewall with minimal setup and no need for complex configurations, UFW is your go-to tool.


##  How Firewalld Works:
Firewalld is a more flexible tool that gives you the ability to organize rules into different "zones" (like a "home" zone, "public" zone, etc.) for different trust levels.
On newer systems, Firewalld uses nftables by default. On older systems, it uses iptables.
So, Firewalld helps you configure rules dynamically, and the rules are actually applied by iptables or nftables, depending on your system.
Example: If you want to allow all traffic on your home network but block incoming traffic from public networks, Firewalld makes it easy to set this up with commands like:

```bash
sudo firewall-cmd --zone=home --add-service=http
sudo firewall-cmd --zone=public --set-target=Drop
```

These commands tell Firewalld to:
* Allow HTTP traffic in the "home" zone (trusted).
* Block all traffic in the "public" zone (untrusted).

WHEN DO YOU USE IT?

When You Need Zones and Advanced Features:
Firewalld's use of zones lets you easily define security policies for different interfaces or networks (e.g., one set of rules for trusted local networks and a different set for untrusted public networks). It’s particularly helpful in enterprise environments or complex networking setups.


## summary
Firewall - The security guard at the front gate of your computer/house.

iptables and nftables - The rulebook that the security guard follows to decide what’s allowed and what’s not.

UFW and Firewalld - Assistants who help you write the rulebook without you having to understand all the details.

Example:

If you want to allow web traffic (HTTP) to your computer:
You could manually add a rule in iptables or nftables.
Or, you could use UFW or Firewalld to easily add that rule with a simple command like "allow web traffic."

### So in simple terms:

Firewall is the security guard for your computer.
iptables/nftables is the list of rules the guard uses.
UFW/Firewalld are tools that help you manage those rules without being a security expert.

# Congrats! 🎉 You’ve nailed the basics of UFW and Firewalld! 🚀 Keep going and dive deeper into firewall management—you’re on your way to mastering Linux security! 🔒💪