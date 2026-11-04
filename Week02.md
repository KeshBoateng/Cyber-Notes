DAY!:
• Bit: The absolute smallest unit of digital data. It is a single binary digit, representing either a 1 (on) or a 0 (off).
• Byte: A group of 8 bits. A single byte represents a single character of text (like the letter "A"). File sizes are measured in bytes (Kilobytes, Megabytes, Gigabytes).
• Bandwidth: The maximum capacity of your internet connection. Think of it like a highway: bandwidth is the number of lanes available to move traffic. More lanes mean more data can move at the same time.
• Latency: The delay or travel time for data to go from your device to a server and back. Using the highway analogy, latency is the speed limit or the time it takes for a single car to complete the trip. Lower latency means a faster response (critical for gaming or live video calls).

How the Internet Works (The Big Picture)

The internet is not a cloud or a magical entity; it is a massive global network of physical cables (fiber-optic lines, copper wires, and undersea cables) connecting millions of computers together.
When you want to visit a website or send a message, your data is broken down into millions of tiny pieces called packets. Each packet contains a piece of the data, along with a "header" that lists the destination address and the sender's address. These packets travel independently across the global network of cables, bouncing from router to router, taking the fastest path available. Once they all arrive at the destination, they are glued back together into the original file or webpage.


DAY2:
A protocol is a well known set of rules that governs communication between devices

When a client sends a request to another device it adds its IP address so the server knows which address to reply back to

IPV4 -Mostly 32 bits long with 8 bits for each part of the address

the first part represents the country
the second part represents the region
the third part represents subnetworks
the fourth part represents the actual address of the device

IPV6---IPV4s humble upgrade which uses a 128bits and provides about 340 undecilion unique addresses

DNS
associates names like www.wiki.org with its corresponding ip address
the computer uses the DNS to lookup domain names and get the associated ip address and then it connects to it.

So basically the client asks a DNS server for the ip address of a site the server asks another DNS server and when it finds it is sent back till it reaches the client and then it finally connects to the ip and sends its request

A network is a bunch of devices connected to each other

The DNS servers are connected in a distributed hierarchy

DNS spoofing:
It is when a hacker taps into a DNS server and changes the ip address of a site to that of their own ip so as to impersonate the website so that clients may accidentally connect to it.
Each section of an IP is called an octet

Ping is a network tool that uses ICMP (Internet Control Message Protocol) packets to determine the performance of a connection between devices, for example, if the connection exists or is reliable.
 
The time taken for ICMP packets travelling between devices is measured by ping.This measuring is done using ICMP's echo packet and then ICMP's echo reply from the target device.

NAT (Network Address Translation): your router swaps your
private address for its public one on the way out, and back on
the way in. So websites see the router's public address, never
your 192.168 one.
When your PC requests a webpage, it sends the request to your phone using its local 10. address. Your phone strips away that private tag, attaches its own public 102. address to the packet, and blasts it out to the internet. When the website replies, the phone does the reverse—passing the data back to your PC's private address

My Wifi Adapters IPV4 address
\10.187.149.32
\ 255.255.255.0
\ 10.187.149.25

DAY3:
TLD (Top-Level Domain)
A TLD is the most righthand part of a domain name. So, for example, the tryhackme.com TLD is .com. There are two types of TLD, gTLD (Generic Top Level) and ccTLD (Country Code Top Level Domain). Historically a gTLD was meant to tell the user the domain name's purpose; for example, a .com would be for commercial purposes, .org for an organisation, .edu for education and .gov for government. And a ccTLD was used for geographical purposes, for example, .ca for sites based in Canada, .co.uk for sites based in the United Kingdom and so on. Due to such demand, there is an influx of new gTLDs ranging from .online , .club , .website , .biz and so many more.

Second-Level Domain:
Taking tryhackme.com as an example, the .com part is the TLD, and tryhackme is the Second Level Domain. When registering a domain name, the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).

Subdomain:
A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it; for example, in the name admin.tryhackme.com the admin part is the subdomain. A subdomain name has the same creation restrictions as a Second-Level Domain, being limited to 63 characters and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens). You can use multiple subdomains split with periods to create longer names, such as jupiter.servers.tryhackme.com. But the length must be kept to 253 characters or less. There is no limit to the number of subdomains you can create for your domain name.


 The journey, step by step

1. Your computer checks its own cache
Have I looked this up recently? If yes, done.
If no, ask the Recursive DNS Server.

2. Recursive DNS Server
Usually your ISP’s, but you can choose another one.
It has its own cache. Popular sites (Google, Facebook) are usually found here, so the search ends quickly.
If it’s not cached, it starts the long search at the root servers.

3. Root servers
They don’t know the answer, but they know who to ask next.
They look at the ending of the domain (.com, .org, etc.) and send you to the right TLD server.

4. TLD (Top Level Domain) server
Handles one ending, e.g. all .com domains.
It points you to the domain’s authoritative server (nameserver).
Example: tryhackme.com → kip.ns.cloudflare.com and uma.ns.cloudflare.com.
Domains have several nameservers as backups in case one goes down.

5. Authoritative server
This is the one that actually holds the DNS records for the domain.
It’s also where the domain owner makes changes to the records.
It sends the answer back to the Recursive server, which saves a copy and passes it to your computer.
Quick flow
Your computer cache
      ↓ (not found)
Recursive DNS Server (cache)
      ↓ (not found)
Root Server → "Go to the .com TLD"
      ↓
TLD Server → "Go to this nameserver"
      ↓
Authoritative Server → gives the IP address
      ↓
Answer travels back and gets cached


HANDS-ON work
Name:    google.com
Addresses:  2a00:1450:4003:804::200e
          142.251.140.238

MX Lookup:gmail.com       MX preference = 5, mail exchanger = gmail-smtp-in.l.google.com    


Windows IP Configuration

    tryhackme.com
    ----------------------------------------
    Record Name . . . . . : tryhackme.com
    Record Type . . . . . : 1
    Time To Live  . . . . : 247
    Data Length . . . . . : 4
    Section . . . . . . . : Answer
    A (Host) Record . . . : 64.239.109.129


    Record Name . . . . . : tryhackme.com
    Record Type . . . . . : 1
    Time To Live  . . . . : 247
    Data Length . . . . . : 4
    Section . . . . . . . : Answer
    A (Host) Record . . . : 64.239.123.129
