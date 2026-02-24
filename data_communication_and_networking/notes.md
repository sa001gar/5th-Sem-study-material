# COMP 5011 – Data Communications \& Networking

Full Theory Notes (Markdown)

## 0. Index (as per syllabus)

1. Data Communication Fundamentals and Techniques
   - [1.1 Basics of communication systems](#11-basics-of-a-communication-system)
   - [1.2 Analog vs digital data and signals](#12-analog-vs-digital-data-and-signals)
   - [1.3 Communication channels; synchronous vs asynchronous](#13-communication-channels-synchronous-vs-asynchronous)
   - [1.4 Data‑rate limits (Nyquist \& Shannon – concept)](#14-datarate-limits-nyquist--shannon--concept-only)
   - [1.5 Digital‑to‑digital line encoding](#15-digitaltodigital-line-encoding)
   - [1.6 Pulse Code Modulation (PCM)](#16-pulse-code-modulation-pcm)
   - [1.7 Parallel vs serial transmission](#17-parallel-vs-serial-transmission)
   - [1.8 Digital‑to‑analog modulation: ASK, FSK, PSK, QPSK, DPSK](#18-digitaltoanalog-modulation-ask-fsk-psk-qpsk-dpsk)
   - [1.9 Multiplexing: FDM, TDM](#19-multiplexing-fdm-and-tdm)
   - [1.10 Transmission media: twisted pair, coax, radio/VHF/microwave, satellite, optical fiber](#110-transmission-media)
2. Introduction to Computer Networks
   - [2.1 Definition and goals of networks](#21-definition-and-goals)
   - [2.2 Network topologies](#22-network-topologies)
   - [2.3 Network classifications (PAN, LAN, MAN, WAN)](#23-network-classifications)
   - [2.4 Protocol and layered architecture](#24-protocol-and-layered-architecture)
   - [2.5 OSI reference model overview](#25-osi-reference-model-overview)
   - [2.6 TCP/IP protocol suite overview](#26-tcpip-protocol-suite-overview)
3. Network Switching Techniques and Access Mechanisms
   - [3.1 Circuit switching](#31-circuit-switching)
   - [3.2 Packet switching – datagram and virtual circuit](#32-packet-switching--datagram-and-virtual-circuit)
   - [3.3 Dial‑up modems](#33-dialup-modems)
   - [3.4 Digital Subscriber Line (DSL)](#34-digital-subscriber-line-dsl)
   - [3.5 Cable TV for data transfer](#35-cable-tv-for-data-transfer)
4. Data Link Layer Functions and Protocols
   - [4.1 Errors, error detection and correction (CRC, Hamming codes)](#41-errors-error-detection-and-correction-crc-hamming)
   - [4.2 Framing and flow control](#42-framing-and-flow-control)
   - [4.3 Error recovery – Stop‑and‑Wait ARQ, Go‑Back‑N ARQ](#43-error-recovery--stopandwait-arq-gobackn-arq)
   - [4.4 Point‑to‑Point Protocol (PPP)](#44-pointtopoint-protocol-ppp)
5. Multiple Access Protocols and Networks
   - [5.1 ALOHA protocols](#51-aloha-protocols)
   - [5.2 CSMA protocols (CSMA/CD \& CSMA/CA – idea)](#52-csma-protocols-csmacd--csmaca)
   - [5.3 CDMA](#53-cdma-code-division-multiple-access)
   - [5.4 Ethernet LANs](#54-ethernet-lans)
   - [5.5 Connecting LANs and backbone networks – repeaters, hubs, switches, bridges, routers, gateways](#55-connecting-lans-and-backbone-networks)
6. Network Layer Functions and Protocols
   - [6.1 Routing; static vs dynamic algorithms](#61-routing-static-vs-dynamic-algorithms)
   - [6.2 Internet network layer – IP protocol](#62-internet-network-layer--ip-protocol)
   - [6.3 Internet control protocols – ICMP (and ARP brief)](#63-internet-control-protocols--icmp-and-arp)
7. Transport Layer Functions and Protocols
   - [7.1 Transport services – error and flow control](#71-transport-services--error-and-flow-control)
   - [7.2 Connection establishment and release – three‑way handshake](#72-connection-establishment-and-release--threeway-handshake)
   - [7.3 TCP](#73-tcp)
   - [7.4 UDP](#74-udp)
8. Application Layer Protocols
   - [8.1 DNS overview](#81-dns-overview)
   - [8.2 WWW and HTTP overview](#82-www-and-http-overview)

***

## 1. Data Communication Fundamentals and Techniques

### 1.1 Basics of a communication system

A **communication system** transfers information from a **source** to a **destination** over a medium.

Basic block diagram:

```text
Source → Transmitter → Channel → Receiver → Destination
                      ( + Noise )
```

- **Source:** origin of message (e.g., microphone, computer file).
- **Transmitter:** converts data into signals suitable for channel (e.g., modem, line encoder).
- **Channel:** physical path (wire, fiber, air).
- **Receiver:** converts received signal back to data.
- **Destination:** final user or device.

***

### 1.2 Analog vs digital data and signals

- **Analog data:** vary continuously (e.g., speech, music waveforms).
- **Digital data:** take discrete values (e.g., bits 0 and 1 from a computer).

**Signals** represent these data on the channel:

- **Analog signal:** continuous waveform, usually sinusoidal. Characterized by amplitude, frequency, phase.
- **Digital signal:** sequence of discrete voltage levels; e.g., 0 V for 0, +5 V for 1.

Analog signal sketch:

```text
Amplitude ^
          |        /‾‾‾\    /‾‾‾\ 
          |       /     \__/     \__
          +----------------------------> time
```

Digital NRZ signal for bits 1 0 1:

```text
Voltage ^
  +5V   ────────┐       ┌───────
                |       |
   0V           └───────┘
             _|‾‾|__|‾‾|__
               1    0   1   → time
```

***

### 1.3 Communication channels; synchronous vs asynchronous

A **channel** is a medium + supporting hardware (twisted pair, fiber, radio link, etc.).

**Synchronous transmission:**

- Sender and receiver share a common timing (clock), or receiver recovers clock from signal.
- Bits are sent in large continuous blocks (frames).
- Used in high‑speed links (e.g., Ethernet physical layer, synchronous serial).

**Asynchronous transmission:**

- No shared continuous clock; each **character** sent with start \& stop bits.
- Receiver resynchronizes for each character.
- Used by UARTs and legacy serial ports.

Example asynchronous frame (8N1: 1 start, 8 data, 1 stop):

```text
Line idle (1)
    |
    v
Start  D0..D7         Stop
 0  d0 d1 d2 d3 d4 d5 d6 d7   1
 _  _  _  _  _  _  _  _  _   _
| || || || || || || || || | |  → time
```

***

### 1.4 Data‑rate limits (Nyquist \& Shannon – concept only)

**Nyquist theorem (noiseless):** maximum bit rate on a noiseless channel of bandwidth $B$ Hz, using M distinct signal levels, is:

$$
R_{max} = 2B \log_2 M\ \text{bps}
$$

**Shannon capacity (with noise):** maximum error‑free data rate is:

$$
C = B \log_2(1 + S/N)\ \text{bps}
$$

where $S/N$ is signal‑to‑noise power ratio.

These show:

- Increasing bandwidth B or SNR increases capacity.
- Using more levels M allows more bits per symbol but demands higher SNR.

***

### 1.5 Digital‑to‑digital line encoding

**Line coding** converts bit stream into a digital signal for transmission.

Key schemes:

1. **NRZ‑L (Non‑Return to Zero – Level):**
    - 1 = high, 0 = low (or vice versa).
    - Simple, but long runs of same bit cause clock recovery problems.
2. **NRZ‑I (Non‑Return to Zero – Invert):**
    - 1 = transition at bit boundary; 0 = no transition.
    - Self‑clocking when many 1s, but still bad for long runs of 0s.
3. **Manchester:**
    - Mid‑bit transition used as clock; for example, 0 = high→low, 1 = low→high.
    - Good clock recovery and zero DC component; requires double bandwidth.

Table summary:

| Encoding | Rule (1 vs 0) | Pros | Cons |
| :-- | :-- | :-- | :-- |
| NRZ‑L | Level high/low | Simple, efficient | No self‑clocking |
| NRZ‑I | 1 causes transition | Better for certain patterns | Still runs of zeros |
| Manchester | Mid‑bit transition encodes bit | Self‑clocking, DC balanced | 2× bandwidth requirement |

Manchester is historically used by classic Ethernet because receivers can easily extract clock from transitions.

***

### 1.6 Pulse Code Modulation (PCM)

PCM digitizes analog signals in three steps:

1. **Sampling:** measure analog signal at fixed intervals (sampling frequency $f_s$). Must satisfy Nyquist: $f_s ≥ 2f_{max}$ where $f_{max}$ is highest frequency in signal.
2. **Quantization:** approximate each sample by nearest level in a finite set.
3. **Encoding:** assign binary code to each level (e.g., 8 bits).

Block diagram:

```text
Analog in → [Low-pass Filter] → [Sampler] → [Quantizer] → [Encoder] → PCM bits
```

Example: Telephony

- Voice up to 4 kHz → sample at 8 kHz.
- 8 bits per sample → bit rate = 8,000 × 8 = 64 kbps.

***

### 1.7 Parallel vs serial transmission

- **Parallel transmission:** multiple bits sent simultaneously on multiple lines.
    - Example: older printer cables with 8‑bit data bus.
    - Pros: high speed over short distance.
    - Cons: many wires; skew (different arrival times) over distance.
- **Serial transmission:** bits sent one after another over a single line.
    - Examples: USB, Ethernet, fiber links.
    - Pros: cheap cabling, suitable for long distances; modern systems are almost all serial.
    - Cons: historically slower at same clock speed, but modern high‑speed serial is extremely fast.

***

### 1.8 Digital‑to‑analog modulation: ASK, FSK, PSK, QPSK, DPSK

Used when channel is band‑pass (telephone line, radio, satellite).

Let carrier be $A \sin(2\pi f_ct + \phi)$.

1. **ASK (Amplitude Shift Keying):** amplitude varies with bit, $f_c,\phi$ fixed.
```text
bit 1: high amplitude sine
bit 0: low/zero amplitude
```

2. **FSK (Frequency Shift Keying):** use two frequencies $f_1,f_2$.
```text
bit 0: ~~~~ (lower frequency)
bit 1: ~~~~~~ (higher frequency)
```

3. **BPSK (Binary PSK):** phase shifts 0° or 180° for 1/0; amplitude constant.
```text
bit 1: /‾\__/‾\__/‾\__
bit 0: \__/‾\__\__/‾\_   (phase inverted)
```

4. **QPSK (Quadrature PSK):** 4 phases, each representing 2 bits (e.g., 00,01,10,11).

QPSK constellation (I/Q axes):

```text
        Q ^
          |
   01  *  |   *  00
          |
----------+----------> I
          |
   11  *  |   *  10
```

5. **DPSK (Differential PSK):** bit represented by **change** or **no change** in phase relative to previous symbol; reduces need for absolute phase reference.

These modulation techniques are the basis of modern wireless systems; higher‑order QAM extends these ideas to carry more bits per symbol.

***

### 1.9 Multiplexing: FDM and TDM

**Multiplexing:** sharing a single channel among multiple signals.

- **FDM (Frequency Division Multiplexing):**
    - Channel bandwidth divided into frequency bands; each user’s signal is modulated to a separate band.
    - Used in radio broadcasting, cable TV.

ASCII spectrum:

```text
Amplitude ^
          | ch1  ch2  ch3  ch4
          +-------------------------> Frequency
```

- **TDM (Time Division Multiplexing):**
    - Users share same frequency; each gets periodic time slots.
    - Used in digital telephony (E1/T1), synchronous digital hierarchy.

ASCII TDM timeline:

```text
Time: | A | B | C | D | A | B | C | D | ...
User: |   frame 1   |   frame 2   |
```

***

### 1.10 Transmission media

**Twisted pair (UTP/STP):**

- Two insulated copper wires twisted together; twisting reduces EMI and crosstalk.
- UTP: cheaper, common in Ethernet; STP: shielded, better noise performance.

**Coaxial cable:**

- Central conductor, dielectric insulator, metallic shield, jacket.
- Better bandwidth and shielding than twisted pair; used in cable TV, older Ethernet.

**Radio/VHF:**

- Wireless broadcast; used in radio, TV, Wi‑Fi (2.4/5 GHz bands).
- Affected by multipath, interference.

**Microwave:**

- High‑frequency (GHz) directional links; used for point‑to‑point backbone, satellite uplink/downlink.

**Satellite:**

- GEO (~36,000 km) satellites provide large coverage but high latency (~250 ms one way).
- LEO constellations (e.g., Starlink) reduce latency.

**Optical fiber:**

- Glass/plastic fiber guides light pulses; extremely high bandwidth and low attenuation.
- Immune to EMI, used in backbone and long‑haul Internet.

***

## 2. Introduction to Computer Networks

### 2.1 Definition and goals

A **computer network** is an interconnected collection of autonomous computers that share resources and communicate using standard protocols.

Goals:

- Resource sharing (printers, files, databases).
- Communication (email, web, VoIP).
- Reliability (redundant paths, fault tolerance).
- Scalability and flexibility.

***

### 2.2 Network topologies

Common **topologies**:

- **Bus:** all nodes share a common backbone; cheap but single bus failure breaks entire network.
- **Star:** all nodes connect to central hub/switch; most common LAN topology.
- **Ring:** each node connects to two neighbors; messages circulate around ring.
- **Mesh:** many nodes interconnected; high redundancy but expensive.

Simple topological sketches:

```text
Bus:   A --- B --- C --- D

Star:       B
           /
      A - H - C
           \
            D

Ring:  A --- B
        \   /
         D-C
```

***

### 2.3 Network classifications

By size/coverage:

- **PAN:** Personal Area Network (a few meters; Bluetooth).
- **LAN:** Local Area Network (building, campus).
- **MAN:** Metropolitan Area Network (city‑scale).
- **WAN:** Wide Area Network (country/world; Internet).

By role:

- **Client–server:** dedicated servers, client requests.
- **Peer‑to‑peer:** nodes act as both clients and servers.

***

### 2.4 Protocol and layered architecture

A **protocol** is a set of rules that define how entities communicate: syntax, semantics, and timing.

**Layering:**

- Splits communication into layers (e.g., physical, data link, network, transport).
- Each layer offers services to the layer above and uses services from the layer below.
- Encourages modular design and interoperability.

***

### 2.5 OSI reference model overview

The **OSI model** has 7 layers:

1. **Physical:** bit transmission over medium (voltages, light, RF).
2. **Data Link:** framing, MAC addressing, local error detection, flow control.
3. **Network:** routing and logical addressing (IP‑like).
4. **Transport:** end‑to‑end reliable or best‑effort service (TCP‑like).
5. **Session:** managing sessions (dialog control, checkpointing).
6. **Presentation:** data format translation, encryption, compression.
7. **Application:** network services directly to user apps (HTTP, FTP, email).

Exam tip: many questions ask to list layers, roles, and sample protocols at each.

***

### 2.6 TCP/IP protocol suite overview

**TCP/IP model** (Internet protocol suite) is what real networks use.

Typical 4‑layer view:

| TCP/IP Layer | Example protocols |
| :-- | :-- |
| Application | HTTP, FTP, SMTP, DNS, SSH |
| Transport | TCP, UDP |
| Internet | IP, ICMP, ARP |
| Link | Ethernet, Wi‑Fi, PPP, Frame Relay |

Relationship to OSI:

- Link ≈ OSI 1+2, Internet ≈ OSI 3, Transport ≈ OSI 4, Application ≈ OSI 5+6+7.

***

## 3. Network Switching Techniques and Access Mechanisms

### 3.1 Circuit switching

**Circuit switching** reserves a dedicated path for the entire call/session (like traditional telephone network).

Phases:

1. **Connection setup:** path established through intermediate switches.
2. **Data transfer:** bits flow with predictable bandwidth and delay.
3. **Teardown:** connection released, resources freed.

Properties:

- Fixed bandwidth; good for constant bit-rate traffic (old voice).
- Inefficient if connection is idle (resources reserved but unused).

***

### 3.2 Packet switching – datagram and virtual circuit

In **packet switching**, messages are broken into packets, each sent independently.

**Datagram (connectionless):**

- Each packet routed independently based on destination address (like IP).
- Packets may take different paths, may arrive out of order or be lost.

**Virtual circuit (connection‑oriented):**

- Setup phase establishes path; subsequent packets carry a VC ID; all follow same path.
- Guarantees in‑order delivery; state kept in switches (e.g., X.25, ATM PVCs).

Comparison chart:

| Feature | Circuit switching | Datagram switching (IP) |
| :-- | :-- | :-- |
| Path | Fixed, reserved | Chosen per packet |
| Setup needed | Yes | No |
| Resource use | Dedicated | Shared |
| Suitable for | Constant streams | Bursty, data traffic |

***

### 3.3 Dial‑up modems

**Dial‑up modem**: modulation/demodulation device enabling digital computers to use analog telephone lines.

- Converts digital bits to analog tones using schemes like FSK, QAM.
- Max speeds around 56 kbps (limited by PSTN).
- Now largely replaced by DSL, cable, fiber.

***

### 3.4 Digital Subscriber Line (DSL)

**DSL** uses existing copper telephone pairs, but at higher frequencies than voice.

- Splits line into voice band (POTS) and multiple data channels using FDM and advanced modulation.
- **ADSL (Asymmetric DSL):** higher download than upload speeds.
- Distance from central office affects speed (longer loops → lower speed).

***

### 3.5 Cable TV for data transfer

Cable Internet uses the **cable TV coax network** plus cable modems.

- FDM provides separate channels for downstream data, upstream data, and TV channels.
- A neighborhood shares coax; downstream is broadcast, upstream uses time slots controlled by headend to avoid collisions (DOCSIS).

***

## 4. Data Link Layer Functions and Protocols

### 4.1 Errors, error detection and correction (CRC, Hamming)

**Types of errors:** single‑bit errors, burst errors due to noise/EMI.

**CRC (Cyclic Redundancy Check)** – error detection:

- Treat data bits as polynomial $D(x)$ over GF(2); choose generator polynomial $G(x)$.
- Append r zeros (r = degree of G) to D; divide by G via modulo‑2 division.
- Remainder R is CRC; transmitted frame = D with R appended.
- Receiver repeats division; if remainder ≠ 0, error detected.

**Hamming codes** – single‑bit error correction:

- Insert parity bits at positions that are powers of 2 (1,2,4,8,...).
- Each parity bit covers certain positions; at receiver, recomputed parities form syndrome.
- Non‑zero syndrome directly gives index of erroneous bit.

***

### 4.2 Framing and flow control

**Framing**: grouping bits into frames so receiver knows where one frame ends and next begins.

Methods:

- Byte count (length field).
- Flag bytes with byte‑stuffing or bit‑stuffing (e.g., HDLC uses flag 01111110 and inserts 0 after five 1s).

**Flow control**: prevents buffer overflows at receiver.

- **Stop‑and‑Wait:** sender sends one frame and waits for ACK before sending next. Simple but inefficient.
- **Sliding window:** sender maintains window of unacknowledged frames; more efficient for long delay–bandwidth products.

***

### 4.3 Error recovery – Stop‑and‑Wait ARQ, Go‑Back‑N ARQ

**ARQ** = Automatic Repeat reQuest.

**Stop‑and‑Wait ARQ:**

- Sender transmits one frame, starts timer, waits for ACK.
- If ACK received → send next; if timeout or NAK → retransmit same frame.

Timing sketch:

```text
Sender: Frame0 ---->      (wait)       <---- ACK0
        Frame1 ----> ...
```

**Go‑Back‑N ARQ:**

- Sender window of size N; sends up to N frames without ACK.
- Frames numbered modulo some max.
- On error in frame k, receiver discards k and subsequent frames; sender, on timeout or NAK, retransmits from k onward.

Go‑Back‑N improves efficiency but can waste bandwidth on many retransmissions; Selective Repeat (beyond your exact syllabus) addresses that.

***

### 4.4 Point‑to‑Point Protocol (PPP)

**PPP** is a popular data link protocol for point‑to‑point serial links (e.g., dial‑up, PPPoE).

Features:

- Framing with flag bytes (0x7E), address/control fields, protocol field, and FCS (CRC).
- **LCP (Link Control Protocol)** negotiates link options (authentication, compression).
- **NCP (Network Control Protocols)** configure network layer protocols (e.g., IPCP for IP).

PPP frame format (simplified):

```text
Flag | Address | Control | Protocol | Payload | FCS | Flag
```

***

## 5. Multiple Access Protocols and Networks

### 5.1 ALOHA protocols

Used in early radio networks with shared medium.

**Pure ALOHA:**

- Node transmits whenever it has a frame.
- If collision occurs (overlap in time) → frame lost → retransmit after random delay.
- Max throughput ≈ 18%.

**Slotted ALOHA:**

- Time divided into slots equal to frame duration; nodes can only transmit at slot boundaries.
- Collisions reduced, max throughput ≈ 36%.

ALOHA is conceptually simple and appears in exam derivations (throughput vs load G).

***

### 5.2 CSMA protocols (CSMA/CD \& CSMA/CA)

**CSMA (Carrier Sense Multiple Access):** nodes sense channel before transmitting.

Variants:

- **1‑persistent:** if idle → transmit; if busy → keep listening and transmit immediately when idle.
- **Non‑persistent:** if busy → wait random time then retry.

**CSMA/CD (with Collision Detection):** Wired Ethernet classic MAC:

- Node listens; if idle, transmits.
- While transmitting, monitors signal; if collision detected (signal differs), aborts and sends jam signal.
- Backoff per binary exponential backoff algorithm.

Modern switched full‑duplex Ethernet effectively eliminates collisions, so CSMA/CD is now mostly historical but still exam‑relevant.

**CSMA/CA (with Collision Avoidance):** Wi‑Fi MAC, uses random backoff and ACKs instead of collision detection (radio cannot listen and transmit simultaneously easily).

***

### 5.3 CDMA (Code Division Multiple Access)

CDMA is a spread‑spectrum technique where multiple users share same time and frequency, but each uses a **unique code**.

- Data bits are multiplied by pseudo‑random chip sequences (codes).
- At receiver, correlation with desired user’s code extracts that user’s signal; others appear as noise.
- Used in older 3G cellular systems and GPS.

Very exam‑friendly concept: “users share bandwidth by different codes instead of time or frequency.”

***

### 5.4 Ethernet LANs

**Ethernet** is the dominant LAN technology.

Properties:

- Uses MAC addresses (48‑bit) for link‑layer addressing.
- Frame format: dest MAC, source MAC, type/length, data, FCS.
- Initially CSMA/CD on coax bus (10BASE‑5/2); now star topology with switches (100/1000BASE‑T, etc.).

Ethernet frame (simplified):

```text
| Dest MAC (6B) | Src MAC (6B) | Type/Len (2B) | Payload (46-1500B) | FCS (4B) |
```

***

### 5.5 Connecting LANs and backbone networks

Devices by layer:

- **Repeater (Physical):** regenerates signals; extends cable length.
- **Hub (Physical):** multiport repeater; broadcasts bits to all ports; obsolete.
- **Bridge/Switch (Data Link):** forward frames based on MAC addresses; learns which MAC is on which port.
- **Router (Network):** forward packets based on IP addresses and routing tables.
- **Gateway (higher layers):** protocol conversion (e.g., email gateway, VoIP gateway).

***

## 6. Network Layer Functions and Protocols

### 6.1 Routing; static vs dynamic algorithms

**Routing:** selecting paths for packets from source to destination.

- **Static routing:** manually configured routes, do not change automatically; used in small or stable networks.
- **Dynamic routing:** routers exchange info and recompute routes when network changes.

Two major classes of dynamic algorithms:

- **Distance‑vector:** routers periodically broadcast vector of distances to all known destinations (e.g., RIP).
- **Link‑state:** routers flood link‑state info, each builds full network map and runs Dijkstra to compute shortest paths (e.g., OSPF, IS‑IS).

***

### 6.2 Internet network layer – IP protocol

**IP (Internet Protocol)** provides best‑effort, connectionless packet delivery.

Key points (IPv4):

- 32‑bit addresses: dotted decimal (e.g., 192.168.1.1).
- Packets called datagrams; routers forward them hop‑by‑hop.
- Header has fields like version, total length, TTL, protocol (TCP/UDP), header checksum, source/destination addresses.

Simplified IPv4 header layout:

```text
|Ver|IHL|DSCP|ECN| Total Length |
|Identification|Flags|Frag Offset|
| TTL | Protocol | Header Check |
| Source IP Address           |
| Destination IP Address      |
| Options (optional) | Padding |
```

IP does **not** guarantee delivery, ordering, or reliability; these features, if needed, are implemented by the transport layer (TCP).

***

### 6.3 Internet control protocols – ICMP (and ARP)

**ICMP (Internet Control Message Protocol):**

- Used to send error messages and operational information (destination unreachable, time exceeded, echo request/reply).
- `ping` uses ICMP echo, `traceroute` uses ICMP time‑exceeded responses.

**ARP (Address Resolution Protocol):**

- Resolves IPv4 addresses to MAC addresses on local LAN; hosts broadcast ARP requests and receive replies from owners of requested IP.

(ARP is not always explicitly named in the syllabus, but is usually grouped under “Internet control protocols.”)

***

## 7. Transport Layer Functions and Protocols

### 7.1 Transport services – error and flow control

The **transport layer** provides end‑to‑end communication between processes on different hosts.

Services commonly provided:

- **Error control:** detect lost or corrupted segments using checksums; retransmit as needed (TCP).
- **Flow control:** adjust sending rate to match receiver capacity (TCP window).
- **Segmentation/reassembly:** split application data into manageable segments, and reassemble at the destination.
- **Multiplexing:** use port numbers to support multiple connections on one host.

***

### 7.2 Connection establishment and release – three‑way handshake

**TCP’s three‑way handshake** establishes a reliable connection:

```text
Client                          Server
  | --- SYN, Seq = x ---------> |
  |                             |
  | <-- SYN + ACK, Seq = y, 
  |            Ack = x+1 ------ |
  |                             |
  | --- ACK, Seq = x+1,
  |            Ack = y+1 -----> |
```

After this:

- Both sides know each other’s initial sequence numbers.
- Bidirectional reliable byte stream is established.

Connection termination typically uses FIN/ACK segments, often forming a “four‑way handshake” to close each direction cleanly.

***

### 7.3 TCP

**TCP (Transmission Control Protocol):**

- Connection‑oriented; provides reliable, ordered, full‑duplex byte stream.
- Implements:
    - Sequence numbers and ACKs for reliable delivery.
    - Sliding window + timers for flow/error control (ARQ).
    - Congestion control (slow start, congestion avoidance, etc.).

Used by reliability‑sensitive applications: HTTP(S), FTP, SMTP, SSH, etc.

***

### 7.4 UDP

**UDP (User Datagram Protocol):**

- Connectionless, best‑effort; minimal header (ports, length, checksum).
- No built‑in flow control, sequencing, or retransmission.
- Suitable for:
    - Simple query/response (DNS),
    - Real‑time streaming (VoIP, video),
    - Applications with their own reliability logic.

***

## 8. Application Layer Protocols

### 8.1 DNS overview

**DNS (Domain Name System)** translates domain names to IP addresses.

Hierarchy:

- Root (.) → TLDs (.com, .org, .in, …) → domain (example.com) → host (www).

Resolution steps (simplified):

1. Application asks local resolver for IP of `www.example.com`.
2. Resolver checks cache; if miss, queries recursive resolver at ISP.
3. Recursive resolver contacts root → TLD (.com) → authoritative server for example.com.
4. Authoritative server returns IP; resolver caches and replies to client.

DNS typically uses UDP on port 53 (TCP used when responses are large or for zone transfers).

***

### 8.2 WWW and HTTP overview

**WWW (World Wide Web):** collection of interlinked documents and services accessible over the Internet, identified by URLs and retrieved via HTTP/HTTPS.

**HTTP (HyperText Transfer Protocol):**

- Application‑layer, request/response protocol.
- Typically runs over TCP port 80 (HTTP) or 443 (HTTPS with TLS).

Basic HTTP/1.1 request example:

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: MyBrowser/1.0
```

Response begins with a status line:

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<html> ... </html>
```

Modern notes (good to mention in theory answers):

- **HTTP/2** adds binary framing, header compression, and multiplexing multiple streams over one TCP connection.
- **HTTP/3** runs over QUIC (UDP‑based), solving some TCP head‑of‑line blocking issues and improving performance on lossy links.

***

This is the complete, integrated note set for the course in markdown format, with all syllabus points covered and extra detail on critical topics (modulation, CRC/ARQ, multiple access, routing, TCP handshakes, DNS/HTTP).

If you want, I can next:

- Generate **unit‑wise practice questions with answers** (2, 5, 10 marks) for this subject, or
- Package these notes as a single `.md` file structure (e.g., per‑unit headings) ready for printing or converting to PDF.

<div align="center">⁂</div>

: https://www.recw.ac.in/v1.8/wp-content/uploads/2021/10/UNIT-1-DCS.pdf

: http://cectl.ac.in/images/pdf_docs/studymaterial/cse/s5/dc3.pdf

: https://mrcet.com/downloads/digital_notes/ECE/III%20Year/DIGITAL%20COMMUNICATIONS.pdf

: https://uomustansiriyah.edu.iq/media/lectures/6/6_2022_10_22!02_45_28_PM.pdf

: https://www.eecs.yorku.ca/course_archive/2010-11/F/3213/CSE3213_07_ShiftKeying_F2010.pdf

: https://www.geeksforgeeks.org/electronics-engineering/digital-modulation-techniques/

: https://en.wikipedia.org/wiki/Internet_protocol_suite

: https://www.pluralsight.com/resources/blog/tech-operations/networking-basics-tcp-udp-tcpip-osi-models

: https://www.checkpoint.com/cyber-hub/network-security/what-is-the-osi-model-understanding-the-7-layers/osi-model-vs-tcp-ip-model/

: https://www.geeksforgeeks.org/computer-networks/error-detection-in-computer-networks/

: https://www.scribd.com/document/985359484/CN-unit-2

: https://www.youtube.com/watch?v=NbVJ3R1wUxE

: https://www.youtube.com/watch?v=zoyvTjxT9DI

: https://www.geeksforgeeks.org/computer-networks/multiple-access-protocols-in-computer-network/
