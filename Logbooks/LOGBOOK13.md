# Sniffing and Spoofing

## Introduction

In this logbook, we will undestand better the mechanisms of monitoring and manipulate the trafic.

We used docker for the setup, and in this logbook we have 3 docker containers.

<div align="center">
    <figure>
        <img src="images/logbook13/log13_1.png">
        <figcaption style="font-size: smaller">Figure 1: Docker Containers Running </figcaption>
    </figure>
</div>

We then use `ifconfig` to find the interface with the IP address `10.9.0.1`:

<div align="center">
    <figure>
        <img src="images/logbook13/log13_2.png">
        <figcaption style="font-size: smaller">Figure 2: Interface with the IP address `10.9.0.1` </figcaption>
    </figure>
</div>

Our network interface is named `br-449382b66784`.

## Task 1

To introduce this next tasks we start by running a simple program using Scapy, that we will need for the next tasks.

We can run Scapy programs 2 ways.
The first by just running the python program like we are used to:

```py
#view mycode.py 
#!/usr/bin/env python3
from scapy.all import * 

a=IP() 
a.show()
```

<div align="center">
    <figure>
        <img src="images/logbook13/log13_3.png">
        <figcaption style="font-size: smaller">Figure 3: Runing the python script </figcaption>
    </figure>
</div>

The second way can be sometimes more convinient by just runing Scapy code interactively:

<div align="center">
    <figure>
        <img src="images/logbook13/log13_4.png">
        <figcaption style="font-size: smaller">Figure 4: Runing the python code interactively </figcaption>
    </figure>
</div>


### Task 1.1 

On this task we sniffed the packets on our network interface, with the help of the following python script.

```py
#!/usr/bin/env python3
from scapy.all import * 

def print_pkt(pkt):
    pkt.show() 

pkt = sniff(iface='br-449382b66784', filter='icmp', prn=print_pkt)

```
The iface is the network interface is name especific for us, so we changed it to `br-449382b66784`

#### **Task 1.1A**

To start we opened one terminal in each container, host A, host B and seed-attacker.

In the seed-atacker one we ran:

```bash
chmod a+x sniffer.py
```

This gave our program root privileges.

So we started running the script.

<div align="center">
    <figure>
        <img src="images/logbook13/log13_5.png">
        <figcaption style="font-size: smaller">Figure 5: Runing the python script with root privileges </figcaption>
    </figure>
</div>

Then in container host A we used the ping command to ping the IP of the host B.

```bash
ping 10.9.0.6 -c 5
```

<div align="center">
    <figure>
        <img src="images/logbook13/log13_6.png">
        <figcaption style="font-size: smaller">Figure 6: From host A ping host B IP </figcaption>
    </figure>
</div>

And in the terminal with root privileges where we where running the `sniffer.py` script:

<div align="center">
    <figure>
        <img src="images/logbook13/log13_7.png">
        <figcaption style="font-size: smaller">Figure 7: Captured packets </figcaption>
    </figure>
</div>

Here we here able to see the captured packets displayed with detailed information for each layer (Ethernet, IP, ICMP and RAW).

```bash
###[ Ethernet ]### 
  dst       = 02:42:0a:09:00:06
  src       = 02:42:0a:09:00:05
  type      = IPv4
###[ IP ]### 
     version   = 4
     ihl       = 5
     tos       = 0x0
     len       = 84
     id        = 7075
     flags     = DF
     frag      = 0
     ttl       = 64
     proto     = icmp
     chksum    = 0xaea
     src       = 10.9.0.5
     dst       = 10.9.0.6
     \options   \
###[ ICMP ]### 
        type      = echo-request
        code      = 0
        chksum    = 0x45ee
        id        = 0x9
        seq       = 0x1
###[ Raw ]### 
           load      = '\x96\xbajg\x00\x00\x00\x00\xef\x12\x03\x00\x00\x00\x00\x00\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-./01234567'
```
Layers:
- Ethernet: Contains MAC addresses and type of the encapsulated protocol (IPv4).
- IP: Contains source and destination IPs, protocol type (ICMP here).
- ICMP: Contains specific ICMP details, such as echo-request/echo-reply.


And when we to to run the `sniffer.py` script without permitions, we can´t:

<div align="center">
    <figure>
        <img src="images/logbook13/log13_8.png">
        <figcaption style="font-size: smaller">Figure 8: Trying to run the script without permitions </figcaption>
    </figure>
</div>  

With root privileges packet sniffing works because root access allows the script to open raw sockets and listen to all packets on the interface.
Without the script can not access raw sockets due to system restrictions, which is a security feature to prevent unauthorized sniffing.

#### **Task 1.1B**

In this task we will set some filters and redo the sniffing to see the resilts.

- **Capture only the ICMP packet**

This filter is the same we used in the last task, so the results will be the same.

```py
pkt = sniff(iface='br-449382b66784', filter='icmp', prn=print_pkt)
```

- **Capture any TCP packet that comes from a particular IP and with a destination port number 23**

To so this, we need to change the `filter` to be `"tcp and src host 10.9.0.5 and dst port 23"`

`10.9.0.5` is the IP of host A, so we whave now filtered all the TCP packets that come from host A and with a destination port number 23 (`and dst port 23`)`.

```py
pkt = sniff(iface='br-449382b66784', filter="tcp and src host 10.9.0.5 and dst port 23", prn=print_pkt)
```

Just like in the last time we ran a command in host A, but a diferent one to ensure that this packet will catched by our filter.

```bash
echo "TESTE" > /dev/tcp/10.9.0.6/23
```

TODO





















