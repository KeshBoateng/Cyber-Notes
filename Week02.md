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

The DNS servers are connected in a distributed hierarchy

DNS spoofing:
It is when a hacker taps into a DNS server and changes the ip address of a site to that of their own ip so as to impersonate the website so that clients may accidentally connect to it.
