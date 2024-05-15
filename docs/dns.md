# DNS - Domain Name System

## Contents
 - [Introduction](#introduction)
 - [Why We Need To Learn](#why-we-need-to-learn)
 - [DNS Hierarchy](#dns-hierarchy)
 - [How Domains Are Read](#how-domains-are-read)
 - [Key Terms](#key-terms)
    - [Root Servers](#root-servers)
    - [TLD Servers](#tld-servers)
    - [Authoritative Nameservers](#authoritative-nameservers)
 - [How It Works](#how-it-works)

## Introduction
<justify>
DNS, or Domain Name System, is like the internet's phonebook. It translates human-readable domain names, like "google.com," into numerical IP addresses that computers use to communicate with each other.
 It's works like magic in miliseconds with several request to some servers (ROOT, TLD, Name Servers).
</justify>

![dns_introduction](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/002.dns_intro.png)

## Why We Need To Learn 
<justify>

Approximately `3 billion` web servers around us, we can't memorize the ip-addresses of the servers. It's impossible to do. But instead of using **Ip address** we are requesting to those servers using domain names. So, We need some method that will convert the domain names to appropriate **Ip address** so that we can access the servers or communicate with servers. This method or we can say `translator` is `DNS`.
</justify>

## DNS Hierarchy

![dns_hierarchy](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/003.dns_hierarchy.png)

## How Domains Are Read
Domains are read in two methods 1.**FQDN** (Fully Qualified Domain Name) and 2.**PQDN** (Partially Qualified Domain Name). First one read the domain from the leaf node and the second one read the domain from any node.

![reading_domain_fqdn_or_pqdn](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/004.fqdn_pqdn.png)

## Key Terms

### Root Servers
The root nameservers are maintained or controlled by a nonprofit called the **Internet Corporation for Assigned Names and Numbers** (`ICANN`).  There are `13 types` of root nameservers, but there are multiple copies of each one all over the world, which use `anycast` routing. They are top of the `DNS` hierarchy. It's job is to provide the details fo the **TLD servers** (cloud be **.com**, **.org**, **.arpa**, **.edu** etc)

![root_server_list](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/005.root_server_list.png)

### TLD Servers
The TLD nameservers maintains information for all the domain names that share a common domain extension. such as **.com**, **.net** etc. This servers don't have the **Ip address** but it has the `authoritative nameserver`'s information. They are two types 
 - **Generic top-level domains** (.com, .org, .net, .gov etc)
 - **Country code top-level domains** (.bd, .in, .us etc)

### Authoritative Nameservers
The authoritative nameservers contains information specific to the domain name it serves (like www.google.com). It can provide a recursive resolver with the **Ip address** of that server found in the `DNS A record`. If the given record has a `CNAME` to another domain, the resolver will do `lookup` for the new one also.

## How It Works
Let's take an example a `www.local.example.com`, we are requesting to this website from our browser (client).

Let's have a look :

![working_process](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/006.working_process.png)

### Step-1
<justify>

It first `lookup` within the machine `cache` and also the cache of the browsers. If it finds the **Ip address** from here then it will proceed further. Otherwise, will follow the next step.
</justify>

### Step-2
<justify>

When your device can't find an **Ip address** in its `local` cache, it asks the **DNS Recursive Resolver Server** (usually your `ISP`). The resolver checks its cache. If the IP address is there, it sends it back. If not, it starts an `iterative` process to `find` the IP address, checking other DNS servers until it does.
</justify>

### Step-3
<justify>

Couldn't resolve Ip address from the cache of the **DNS Recursive Resolver Server**. The **recursivel resolver server** send request to the `root server` with the `TLD` (**Top Level Domain** in our case `.com`). The `root server` gives us the information about the `TLD server` (in our case `.com`'s server) as a response to our **recursivel resolver server**.
</justify>

### Step-4
<justify>

After getting the information about the `TLD server`. The **recursivel resolver server** send request to the `TLD server` with the `domain` name (in our case example.com). Then `TLD server` respond with a **authoritative server** information which has the acutal **Ip address** of our requested server.
</justify>

### Step-5
<justify>

After getting the information about the **authoritative server**. The **recursivel resolver server** send request to the **authoritative server** with the `domain` name (in our case example.com). Then **authoritative server** respond with a **Ip address** of the requested server. And it is the last step for lookup the **Ip address** of a server. After getting the **Ip address** the **recursivel resolver server** saves it in it's `cache` and send it to the client.
</justify>

