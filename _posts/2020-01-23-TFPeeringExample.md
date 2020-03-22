---
layout: post
title:  "Azure VNet Peering Example / One-Way Peering"
categories: posts
---
# This might be useless, but I learned something

It's nice to be able to experiment with new technology. As a cloud engineer, and architect I get to do a lot of this. The other day I recommended the use of a one way peering within Azure to control access. I had no idea if you could really make it work that way, and you can.  

VNet peering is the ability to connect virtual networks using the Microsoft Azure fabric backbone, and without the use of a Site to Site VPN gateway appliance. VNet peering can happen between regions within a subscription, or between regions in different subscriptions in the same tenant.  You can also peer VNets from environments in a completely different tenant.  

So what I wanted to prove was I could stand up a VNet (VNetA) in one region, peer it to another VNet (VNetB) in another region, but only allow traffic to flow into vnetA accessing vnetB resources, while not allowing vnetB resources to access vnetA resources.

So I sketched out what I would need.

- 2 VNets (ip space not overlapping)
- 2 subnets (one for each VNet)
- 2 virtual machines (with nic, disk, etc)
- 2 public IP addresses
- and the VNet peering configuration.

<!--more-->

I'll admit I feel comfortable using the GUI.  It just takes so long though.
Now I could build this all by clicking through the azure portal.  

There is the CLI ?? and that's cool but it has its own quirks

If you've ever worked with Azure Resource Manager (ARM) templates, and you like them, you are truly alone :joy: ...not really, but I think you're among a rare breed of masochist.  I have no love for `json` documents. ARM is nice but I've grown to hate it unless I have to use it.

`Enter Terraform`

`Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.` - Hashicorp / www.terraform.io

In short, it is an ARM alternative.  Something that provides easier to read language, and is unencumbered by the tediousness of a `json` file.

The Site Reliability Engineers or SRE guys use it to help develop customer landing zones within Azure using terraform in a process defined as `infrastructure as code`.

Infrastructure as code can mean a lot of things, it can mean ARM templates, it can mean PowerShell or AZ CLI Bash scripts to deploy environments.  You wrap the development of an environment in the typical software development life cycle, utilize popular tools to perform tests, and analysis on the environment, and then iteratively release versions of your infrastructure. Very little portal usage in the IAC world.  Terraform makes this easier to do.

Since we use it as a primary tool in our shop, and I'm up for learning new things, what I did was create the environment listed above in Terraform.  Because I could, and I've decided to share it with you.
