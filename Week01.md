
Day1:
Offensive Security means taking on the role of am attacker in order to identify vulnerabilities 

One weakness that is quite common is leaving hidden pages accessible
Dirtbuster: A tool that is used to find hidden pages
USE: dirt https://-----

DAy2:
Red team refers to a team of cybersecurity experts whose main specialty is to test for vulnerabilities and weakness by taking on the role of an attacker with legal permission to the system whilst Blue team conduct investigations, monitor systems incase of a breach and conduct incidence response during an attack

Day3:
Penetration Tester
AppSec

Day4:
BIOS Mode-UEFI
Secure Boot State:OFf
BIOS version/DAte : AMI F.42 !!/15/2019
Enabling Secure Boot is good because it acts as a digital bouncer for your computer, ensuring that only trusted, digitally signed software can run the moment you press the power button

laptop stays on power is out whilst a desktop goes off immediately...the CIA letter is therefore A
The CIA Triad Breakdown
Core Principle	What It Means	Impact of a Power Outage

Confidentiality	Keeping data secret and private.	Unaffected. A blackout doesn't expose your files to hackers.
Integrity	Keeping data accurate and untampered.	Secondary Risk. Sudden shutdowns can corrupt active files, compromising data integrity.
Availability	Ensuring systems and data are accessible when needed.	Primary Failure (for the desktop). If the system has no power, the data and services are completely unavailable.


Day5:
What is a client and what is a server? Give one example from your phone.
A client is a device or software that initiates communication or requests services from a server whilst a server is a high performance system that manages incoming requests from clients processes them and hands back the requested resources to the clients


What happens between pressing the power button and seeing the login screen? Where does Secure Boot fit in?
1.Electricity from the power supply hits the motherboard and cpu
2.The CPU initializes and executes the UEFI firmware
3.The UEFI checks and verifies if all critical hardware are present and functioning
4.The UEFI looks at your storage drive to find the OS Bootloader
5.With Secure Boot enabled the bootloader does not just run the bootloader it inspects the bootloader's digital signature
5.it compares the signature against a database of trusted keys embedded unto the motherboard and once it is approved the bootloader loads the OS kernel
6.The approved bootloader moves the OS Kernel into RAM.
7. The kernel takes control and loads essential device drivers.
8. Background security programs and system processes spin up.
9.The graphics engine turns on and displays the login screen

8.
Take apart https://en.wikipedia.org/wiki/Ghana: which part is the scheme, the host and the path? Which port does HTTPS use?
Scheme -https
Host-en.wikipedia.org
Path-/wiki/Ghana
Port-443

9.
What is a cookie, and why would an attacker want to steal yours?
A cookie is a digital ID badge that a website slips into your browser after you log in as a form of identification. An attacker may wat it as it allows them to impersonate you

10.
What is a single point of failure? Give an example near you and how a spare would fix it.
It is a single part of a system in which when it breaks it causes the entire system to fail.
Akosombo Dam 
A single point of failure is fixed by adding redundancy(a spare) so in case of failure theres always a second option
