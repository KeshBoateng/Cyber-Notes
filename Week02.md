# Networking Fundamentals: Simple Notes

## 1. The Basics

- **Network:** devices connected so they can share data.
- **Bit** = 0 or 1. **Byte** = 8 bits.
- **Bandwidth** = how much data can flow (the width of the pipe).
- **Latency** = how long data takes to get there and back, in ms (the length of the pipe).
- **Protocol:** a set of rules for how devices talk (TCP, UDP, HTTP, DNS, DHCP, ARP).
- **The internet:** millions of networks joined by cables (including undersea ones). Your request is cut into **packets**, which cross routers and are rebuilt at the destination.

---

## 2. Addresses: Who Is Who

| | IP address | MAC address |
|---|---|---|
| What | Logical address | Hardware ID of a network card |
| Used for | Finding a device across networks | Delivery on the local network only |
| Changes? | Yes (new network, new IP) | Usually no (can be randomised) |
| Example | `10.33.128.30` | `4C-EB-BD-13-28-EF` |

**IPv4:** 32 bits, four numbers (octets) from 0 to 255, e.g. `192.168.1.100`.
**IPv6:** 128 bits, a far bigger address space.

**Private vs public**
- Private: used inside a local network (`10.x.x.x`, `192.168.x.x`). Not reachable directly from the internet.
- Public: identifies your network on the internet. Given by your ISP.

**NAT:** the router swaps your private IP for its public IP when you go online, and remembers who asked for what so replies reach the right device. Many devices share one public IP.

---

## 3. Subnetting

**Subnet mask:** says which part of an IP is the *network* and which is the *host* (device).

`192.168.1.100` with mask `255.255.255.0` (`/24`): `192.168.1` is the network, `100` is the device.

| Address type | Meaning | Example |
|---|---|---|
| Network address | Names the network itself | 192.168.1.0 |
| Host address | One device | 192.168.1.100 |
| Broadcast | Sends to everyone on the subnet | 192.168.1.255 |
| Default gateway | The way out to other networks (your router) | 192.168.1.254 |

**Counting hosts for `/24`:** 32 − 24 = 8 host bits. Usable hosts = 2⁸ − 2 = **254** (minus network and broadcast).
Range: `.1` to `.254`.

**Why subnet?** Efficiency, security (separate groups, e.g. café staff vs customer Wi-Fi) and easier control.

---

## 4. ARP: IP to MAC

- Wires and Wi-Fi deliver by **MAC**, but you know the **IP**. ARP bridges that.
- **ARP request** (broadcast): "Who has 10.33.128.86?"
- **ARP reply:** "I do. My MAC is 62-03-03-55-b0-00."
- **ARP cache** stores the answers so it doesn't have to ask again.
- Only works on the **local** network. For anything outside, you find the MAC of your gateway.
- **Security:** ARP has no way to verify replies, so an attacker can lie (ARP spoofing).

---

## 5. DHCP: Automatic Addresses

DHCP hands out IP addresses automatically (your router or phone hotspot is usually the DHCP server).

**DORA:**
1. **D**iscover: "Any DHCP server out there?"
2. **O**ffer: "You can have 10.33.128.30."
3. **R**equest: "I'll take it."
4. **A**CK: "Confirmed."

- **Dynamic IP:** from DHCP, on a time-limited **lease**. Can change.
- **Static IP:** set by hand. Good for servers and printers.

---

## 6. DNS: Names to IPs

DNS is the internet's phone book: `google.com` becomes an IP address.

**The journey (cache first, then ask):**
1. Your computer's cache
2. Recursive DNS server (does the searching for you, usually your ISP)
3. Root server ("go to the .com TLD")
4. TLD server ("go to this nameserver")
5. Authoritative server (holds the real records and gives the answer)
6. Answer returns and is cached

| Server | One-liner |
|---|---|
| Recursive | Finds the answer for you |
| Root | Where should I look? |
| TLD | Which domain's server? |
| Authoritative | Here's the real answer |

**Reading a domain right to left:** `admin.tryhackme.com`
- `.com` = TLD (gTLD like .com/.org, or ccTLD like .gh/.uk)
- `tryhackme` = second-level domain (the part you buy)
- `admin` = subdomain (created free by the owner)
- Limits: 63 characters per part, 253 in total, only `a-z 0-9 -`, no hyphen at the start or end.

**Record types**

| Record | Purpose |
|---|---|
| A | Name → IPv4 |
| AAAA | Name → IPv6 |
| CNAME | Name → another name (alias) |
| MX | Mail servers (lowest priority number is tried first) |
| NS | Which nameservers are in charge |
| TXT | Free text, used for verification and email security |
| PTR | IP → name (reverse lookup) |

**DNS TTL:** how many seconds a cached answer is kept. (Not the same as packet TTL.)

**"Non-authoritative answer"** = the answer came from a cache or middleman, not from the domain's own nameserver. It doesn't mean the answer is wrong.

**DNS spoofing:** tricking DNS (or the hosts file) so a real domain points to an attacker's IP.

---

## 7. Packets, Routers, TTL

- **Packet:** header (from, to, number, TTL) + payload (the data).
- **Why packets?** A lost piece is cheap to resend, and many users share the same cables.
- **Router:** reads the destination IP and forwards the packet one step closer.
- **Hop:** one router on the path. Hop 1 is your own gateway.
- **Packet TTL:** starts at 64 or 128. Each router subtracts 1. At 0 the packet is dropped, so lost packets can't loop forever.
- **tracert** sends packets with TTL 1, 2, 3... so each router reports back and shows the path.

---

## 8. TCP vs UDP

| | TCP | UDP |
|---|---|---|
| Promise | Everything arrives, in order, lost data resent | No guarantee |
| Start | Handshake | None |
| Speed | Slower | Faster |
| Use for | Web, email, downloads, payments | Calls, video, gaming, streaming, DNS |
| Analogy | Registered parcel | Shouting across the road |

**Rule:** every byte must arrive → TCP. Speed matters more than a lost bit → UDP.

---

## 9. Network Health and Attacks

- **Ping** uses ICMP echo request/reply to test reachability and measure time.
- **Packet loss:** packets that never arrive. 3 lost out of 20 = 15%.
- **Latency:** the delay in ms.
- **Good network:** 0% loss, small gap between min and max. **Weak network:** loss and big swings (e.g. 60 ms to 900 ms).
- **DDoS:** many systems flood a server so real users can't get in. Attacks **availability**.

---

## 10. Commands Cheat Sheet (Windows)

| Command | What it does |
|---|---|
| `ipconfig` | Your IP, mask, gateway |
| `ipconfig /all` | Adds MAC, DHCP and DNS details |
| `ipconfig /displaydns` | Shows the DNS cache |
| `ipconfig /flushdns` | Clears the DNS cache |
| `ping 8.8.8.8` / `ping -n 20 8.8.8.8` | Test reachability / send 20 pings |
| `tracert -d 8.8.8.8` | Show the route (`-d` = no name lookups) |
| `nslookup google.com` | DNS lookup |
| `nslookup -type=MX gmail.com` | Look up a specific record type |
| `arp -a` | Show the ARP cache |
| `Get-Content C:\Windows\System32\drivers\etc\hosts` | View the hosts file (PowerShell, view only) |

---

# How It All Fits Together: One Simple Scenario

**Story:** I open `google.com` on my laptop, which is connected to my phone's hotspot.

**The cast**

| Who | Address | Role |
|---|---|---|
| My laptop | IP `10.33.128.30`, MAC `4C-EB-...` | The one asking |
| My phone | `10.33.128.86`, MAC `62-03-...` | DHCP server, gateway, DNS forwarder, NAT |
| Carrier's DNS server | (not seen) | Recursive DNS server |
| Routers | many | Pass packets along, hop by hop |
| Google's server | `142.251.x.x` | Has the website |

**The steps, in order**

```
STEP 0  DHCP     Laptop joins the hotspot.
                 Laptop: "Anyone give me an address?"  (Discover)
                 Phone:  "Take 10.33.128.30"           (Offer)
                 Laptop: "OK"  Phone: "Confirmed"      (Request, ACK)
                 Now the laptop knows: my IP, my gateway (.86), my DNS (.86).

STEP 1  DNS      "What is google.com's IP?"
                 Laptop cache? No → ask phone → phone asks carrier's
                 recursive server → (Root → TLD → Authoritative if needed)
                 Answer: 142.251.x.x. Cached for its TTL.
                 (Sent over UDP: small and fast.)

STEP 2  Subnet   Is 142.251.x.x on my network (10.33.128.x)?
                 The subnet mask says NO → send it to the Default Gateway.

STEP 3  ARP      I need the gateway's MAC, not just its IP.
                 Laptop (broadcast): "Who has 10.33.128.86?"
                 Phone: "Me, MAC 62-03-03-55-b0-00"  → saved in ARP cache.

STEP 4  Packets  The request is cut into packets:
                 header (from .30, to 142.251.x.x, TTL 128) + payload.
                 Web pages use TCP, so a handshake happens first and
                 lost packets get resent.
                 Each packet is delivered to the phone's MAC.

STEP 5  NAT      Phone swaps my private IP (.30) for its public IP,
                 remembers who asked, and forwards to the carrier.

STEP 6  Hops     Routers pass the packet along. Each takes 1 off the TTL.
                 (tracert shows these hops. ping shows how long it took.)

STEP 7  Reply    Google answers. The packets return the same way.
                 NAT sends them back to .30. The laptop puts the
                 packets in order and the page appears.
```

**How the parts connect (one line each)**

| Part | Answers the question | Connects to |
|---|---|---|
| DHCP | "What's my IP and who is my gateway?" | Gives the laptop its IP, gateway and DNS |
| DNS | "What's the IP of this name?" | Gives the IP that routing needs |
| Subnet mask | "Is it on my network or not?" | Decides whether to go direct or via the gateway |
| ARP | "What's the MAC for this IP?" | Needed to deliver to the gateway on the local network |
| Packets and TCP/UDP | "How is the data sent?" | Carry the data once the address is known |
| NAT | "How does a private IP use the internet?" | Done by the gateway before packets leave |
| Routers, hops, TTL | "How does it cross the internet?" | Move packets towards the destination |
| ping, tracert | "Is it working and how far is it?" | Measure the journey above |

**One-line memory chain:**
**DHCP** gives me an address → **DNS** finds the destination IP → **subnet mask** says "go via gateway" → **ARP** finds the gateway's MAC → **packets** carry the data → **NAT** hides my private IP → **routers** hop it across → the reply comes back the same way.

**Where an attacker could interfere (ties to your labs):**
- **Hosts file / DNS spoofing:** lie at Step 1 so I go to a fake IP.
- **ARP spoofing:** lie at Step 3 so my traffic goes through the attacker first.
- **DDoS:** flood the destination so real packets can't get through (Step 6 to 7).

---

# My Hands-On Labs

> **Note:** I used my phone's hotspot. A hotspot can give a different address range each time it's turned on, so the IPs differ between days. Write the date and session next to each result.

## Lab: nslookup

- `nslookup google.com` → IPv4 `142.251.140.238`, IPv6 `2a00:1450:4003:804::200e`
- `nslookup -type=MX gmail.com` → `gmail-smtp-in.l.google.com` (the mail server for Gmail)
- The "Server" line showed my phone's address as `UnKnown`. That only means there is no PTR (reverse) record for it. The phone forwards my question to the real recursive server, which is why the answer was **non-authoritative**.

## Lab: DNS cache (`ipconfig /displaydns`)

- The cache holds names I never typed (Windows Update, Google certificate checks) because background apps do lookups too.
- `login.live.com` showed a chain of **4 CNAMEs** before reaching the A records (big companies use this to steer traffic).
- Browsers keep their own cache, so a site visited in the browser didn't appear. After `ping tryhackme.com` it did (type 1 = A record).
- TTL counts down. `ipconfig /flushdns` empties the cache.

## Lab: hosts file

- Command: `Get-Content C:\Windows\System32\drivers\etc\hosts`
- Lines that do **not** start with `#`: **[fill in your number, usually 0]**
- **Why malware would add `6.6.6.6 mtn.com.gh`:** the hosts file is checked **before** DNS. That line forces my computer to send `mtn.com.gh` to the attacker's server, where a fake MTN page can steal logins. It can also be used to block antivirus update sites.

## Lab: tracert

- `tracert -d 8.8.8.8` → **14 hops**. Hops 2 and 7 timed out, but the trace still completed (some routers don't answer probes).
- Hops 1 to 6 were private `10.x.x.x` carrier addresses. Public addresses started around hop 8.
- **To finish:** in one session, run `ipconfig` and `tracert -d 8.8.8.8` together and check that hop 1 equals the Default Gateway.

## Lab: near vs far

| Destination | Hops | Last hop time |
|---|---|---|
| 8.8.8.8 (Google) | 14 | about 55 ms |
| wikipedia.org | 20 | about 270 to 305 ms |

Wikipedia is further away. **Time is the better evidence** because it shows the real delay, while hop count only shows routers crossed. Google likely has servers nearer to Ghana.

## Lab: packet loss

`ping -n 20 8.8.8.8` → Lost = 0 (**0% loss**), Min 46 ms, Max 77 ms, Avg 57 ms. Stable, good network. Reply TTL was 115, which suggests a start of 128 and about 13 routers on the way back (my inference).

## Day 5 Lab: `ipconfig /all` (Wi-Fi adapter)

| Setting | Value | About |
|---|---|---|
| Physical Address (MAC) | 4C-EB-BD-13-28-EF | My laptop's Wi-Fi card |
| IPv4 Address | 10.33.128.30 | My laptop |
| Subnet Mask | 255.255.255.0 | Network is 10.33.128.x |
| DHCP Enabled | Yes | |
| DHCP Server | 10.33.128.86 | My phone |
| Lease Obtained | Sunday, November 15, 2026 12:33:58 PM | |
| Lease Expires | Sunday, November 15, 2026 5:00:55 PM | |
| Default Gateway | 10.33.128.86 | My phone |
| DNS Servers | 10.33.128.86 | My phone (forwards to the real DNS) |

**Trick to read it:** lines about *me* (IP, MAC, mask, lease) are the laptop. Lines about *who gave me this / where I send things* (gateway, DHCP server, DNS) are the phone. The laptop is `.30` and the phone is `.86`: two devices on the same network.

(Earlier session: IP `10.187.149.32`, gateway `10.187.149.25`. Different day, different hotspot range.)

## Day 5 Lab: `arp -a`

Interface `10.33.128.30` (my laptop's Wi-Fi card):
- Default Gateway `10.33.128.86` Physical Address: **62-03-03-55-b0-00** (my phone)
- Dynamic entries: **1**
- The `static` rows are not devices: `10.33.128.255` and `255.255.255.255` are broadcast, `224.0.0.x` are multicast.
- The `192.168.56.1` block is a virtual adapter. Ignored.

## Day 5 Lab: hex by hand

Each hex digit = 4 bits. A=10, B=11, C=12, D=13, E=14, F=15.

| Hex | Binary | Decimal |
|---|---|---|
| (a) 3C | 0011 1100 | 3×16 + 12 = **60** |
| (b) FF | 1111 1111 | 15×16 + 15 = **255** |
| (c) 0A | 0000 1010 | 0×16 + 10 = **10** |
| My MAC's first pair, 4C | 0100 1100 | 4×16 + 12 = **76** |

## Day 5 Lab: map my network

- **Network:** my phone's hotspot.
- **Router:** my phone. It is the DHCP server, default gateway and DNS forwarder (`10.33.128.86`).
- **Devices:** my laptop (`10.33.128.30`) plus anything else connected.
- **Topology:** **star.** Every device connects to one central point (the phone), which connects out to the carrier and the internet.

## Day 5 Lab: push to git

```
git status
git add .
git commit -m "Week 2 Day 5 notes"
git push
```

Check `git status` first so only your notes are staged.

---

# Quick Revision

1. **IP vs MAC:** IP finds a device across networks; MAC delivers on the local network.
2. **ARP:** IP → MAC (local only).
3. **DHCP:** automatic IPs. Remember **DORA**.
4. **DNS:** name → IP. Cache → Recursive → Root → TLD → Authoritative.
5. **Subnet mask:** splits network from host.
6. **NAT:** many private devices share one public IP.
7. **TTL:** packet TTL = hops left. DNS TTL = seconds cached.
8. **TCP:** reliable. **UDP:** fast.
9. **ping** tests reachability, **tracert** shows the route.

Networking is about how devices identify each other, find their destinations, and make sure data arrives in the right place.
