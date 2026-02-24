#  Practice Questions with Answers
> Major/DS Course (Core): COMP 5011 (Theory)- Data Communication and Networking

## 0. Index

- [Unit 1 – Data Communication Fundamentals and Techniques](#unit-1--data-communication-fundamentals-and-techniques)
- [Unit 2 – Introduction to Computer Networks](#unit-2--introduction-to-computer-networks)
- [Unit 3 – Switching and Access Mechanisms](#unit-3--switching-and-access-mechanisms)
- [Unit 4 – Data Link Layer: Errors, ARQ, PPP](#unit-4--data-link-layer-errors-arq-ppp)
- [Unit 5 – Multiple Access and LANs](#unit-5--multiple-access-and-lans)
- [Unit 6 – Network Layer](#unit-6--network-layer)
- [Unit 7 – Transport Layer](#unit-7--transport-layer)
- [Unit 8 – Application Layer: DNS, WWW, HTTP](#unit-8--application-layer-dns-www-http)

***

## Unit 1 – Data Communication Fundamentals and Techniques

### 2‑mark questions

**Q1. Differentiate between analog data and digital data with one example each.**

**Ans:**

- Analog data vary continuously over time, such as human speech captured by a microphone.
- Digital data take discrete values, typically binary 0 and 1, such as a text file stored on a computer.

***

**Q2. What is Manchester encoding and why is it useful?**

**Ans:** Manchester encoding represents each bit with a mid‑bit transition (e.g. 0 = high→low, 1 = low→high), so the signal has a transition every bit period. This makes the signal self‑clocking and DC‑balanced, which simplifies clock recovery and reduces baseline wander in physical links like classic Ethernet.

***

### 5‑mark questions

**Q3. Explain the steps of Pulse Code Modulation (PCM) and compute the bit rate for 8 kHz sampling with 8‑bit quantization.**

**Ans:**

- PCM steps:

1. Sampling: sample the analog signal at a fixed rate $f_s$ at or above twice the highest frequency in the signal (Nyquist).
2. Quantization: approximate each sample to the nearest level in a finite set.
3. Encoding: encode each quantized level as an n‑bit binary word.
- For an 8 kHz sampling rate and 8 bits per sample, bit rate = 8000 samples/s × 8 bits/sample = 64 kbps (classic PCM voice channel).

***

**Q4. Compare ASK, FSK and PSK as digital‑to‑analog modulation techniques.**

**Ans:**

- ASK (Amplitude Shift Keying): bit values are represented by changes in carrier amplitude, while frequency and phase stay constant; it is simple but more sensitive to amplitude noise.
- FSK (Frequency Shift Keying): uses different carrier frequencies for 0 and 1; it is more robust to amplitude variations but uses more bandwidth.
- PSK (Phase Shift Keying): encodes bits in different carrier phases while keeping amplitude and frequency constant; BPSK uses 0° and 180° and has good noise performance and bandwidth efficiency.

***

### 10‑mark question

**Q5. Discuss in detail the concepts of Nyquist and Shannon data‑rate limits. Explain, with examples, how bandwidth and signal‑to‑noise ratio affect achievable bit rate.**

**Ans:**

- Nyquist theorem (noiseless channel): for a channel of bandwidth B Hz and M discrete signal levels, the highest achievable bit rate is $R_{max} = 2B\log_2M$ bps.
    - Example: A noiseless 3 kHz channel with binary signaling (M = 2) can theoretically support 2 × 3000 × 1 = 6000 bps.
- Shannon capacity (noisy channel): for bandwidth B and signal‑to‑noise power ratio S/N, capacity is $C = B\log_2(1+S/N)$ bps.
    - Example: For B = 3 kHz and S/N = 30 dB (S/N = 1000), C ≈ 3000 × log2(1001) ≈ 3000 × ~10 ≈ 30 kbps.
- Increasing bandwidth allows higher bit rates even with fixed SNR, while increasing SNR also improves capacity without changing bandwidth.
- In practice, system design chooses modulation/line coding techniques to approach these theoretical limits, trading complexity and error performance.

***

## Unit 2 – Introduction to Computer Networks

### 2‑mark questions

**Q6. List any four layers of the OSI model in correct order from bottom to top.**

**Ans:** Physical, Data Link, Network, Transport (followed by Session, Presentation, Application).

***

**Q7. What is a protocol in computer networks?**

**Ans:** A protocol is a set of rules that define the format, meaning, and timing of messages exchanged between communicating entities, ensuring interoperable communication.

***

### 5‑mark questions

**Q8. Distinguish between OSI and TCP/IP models.**

**Ans:**

- OSI model has seven layers (Physical, Data Link, Network, Transport, Session, Presentation, Application), designed as a general theoretical framework.
- TCP/IP model has four main layers (Link, Internet, Transport, Application), directly based on practical Internet protocols.
- In OSI, presentation and session are separate, handling formatting and session management; in TCP/IP these functions are bundled inside the application layer.
- OSI emphasizes strict layering and services/interfaces, while TCP/IP is more implementation‑oriented and widely used in real networks like the Internet.

***

### 10‑mark question

**Q9. Describe the OSI reference model, explaining the main function of each layer and giving at least one example protocol for each applicable layer.**

**Ans:**

- Physical: transmits raw bits over a physical medium (voltages, light, RF). Example: Ethernet physical standards, DSL, SONET/SDH.
- Data Link: provides node‑to‑node delivery, framing, MAC addressing, local error detection, and flow control. Example: Ethernet MAC, PPP, Wi‑Fi MAC.
- Network: handles routing and logical addressing across multiple networks. Example: IP, ICMP, routing protocols.
- Transport: end‑to‑end delivery, segmentation, error and flow control between processes. Example: TCP (reliable), UDP (unreliable).
- Session: manages dialog control, synchronization, and checkpoints between applications. Example: NetBIOS, RPC–style session services.
- Presentation: data representation, translation, encryption, and compression. Example: TLS/SSL, JPEG, ASCII/Unicode conversions.
- Application: provides network services directly to user applications (file transfer, email, web). Example: HTTP, FTP, SMTP, DNS.

***

## Unit 3 – Switching and Access Mechanisms

### 2‑mark questions

**Q10. What is circuit switching? Give one example network.**

**Ans:** Circuit switching is a switching technique where a dedicated path with reserved resources is established between source and destination for the entire duration of the session. A classic example is the traditional Public Switched Telephone Network (PSTN).

***

**Q11. In packet switching, distinguish between datagram and virtual circuit approaches.**

**Ans:** In datagram switching, each packet is routed independently based only on its destination address and may take different paths. In virtual circuit switching, a logical path is set up first and all packets in a flow carry a virtual circuit identifier and follow the same route, giving in‑order delivery.

***

### 5‑mark questions

**Q12. Explain how DSL provides broadband access over telephone lines.**

**Ans:**

- DSL reuses the existing copper telephone pair by splitting the frequency band into low‑frequency voice and higher‑frequency data using filters/splitters.
- The high‑frequency band is modulated using multi‑carrier techniques (e.g., DMT) to carry digital data; the DSLAM at provider aggregates lines.
- ADSL (Asymmetric DSL) dedicates more bandwidth to downstream than upstream to match typical usage patterns.
- This allows simultaneous voice and Internet over the same line, at speeds much higher than dial‑up.

***

### 10‑mark question

**Q13. Compare circuit switching and packet switching in detail. Discuss their suitability for voice calls and data traffic with examples.**

**Ans:**

- Circuit switching:
    - Establishes dedicated path via setup phase (call setup, data transfer, teardown).
    - Guaranteed bandwidth and typically fixed delay once established; good for constant bit‑rate traffic like traditional voice calls.
    - Inefficient for bursty traffic as capacity is reserved even when idle.
- Packet switching:
    - No fixed path; packets share links with others and are queued at intermediate routers.
    - Efficient for bursty data; resources statistically multiplexed among many flows (Internet traffic).
    - Delay and jitter can vary; some packets may be lost or out‑of‑order (handled by higher layers like TCP if needed).
- For **voice**, circuit switching historically provided predictable real‑time quality; now VoIP uses packet switching plus QoS (prioritization, jitter buffers) to approximate this.
- For **data**, packet switching is clearly superior due to better link utilization and ability to handle many short connections (web browsing, email, file transfer).

***

## Unit 4 – Data Link Layer: Errors, ARQ, PPP

### 2‑mark questions

**Q14. What is the main purpose of using CRC in data link layer frames?**

**Ans:** CRC (Cyclic Redundancy Check) is used to detect errors in a received frame by treating the frame as a polynomial and verifying that its division by a known generator polynomial leaves a zero remainder.

***

**Q15. What does ARQ stand for? Name two ARQ protocols.**

**Ans:** ARQ stands for **Automatic Repeat reQuest**. Two ARQ protocols are Stop‑and‑Wait ARQ and Go‑Back‑N ARQ.

***

### 5‑mark questions

**Q16. Explain the working of Stop‑and‑Wait ARQ with a timing diagram.**

**Ans:**

- Sender transmits one frame and starts a timer, then waits for acknowledgement (ACK).
- If ACK is received before timeout, sender transmits the next frame; if timer expires or a negative ACK is received, sender retransmits the same frame.
- Frames and ACKs carry sequence numbers (often 0/1) to distinguish new transmissions from duplicates.
- ASCII timing sketch:

```text
Sender:  Frame0 ---->          <---- ACK0
         Frame1 ---->          <---- ACK1
Receiver:   receive0, send ACK0; receive1, send ACK1
```

- This scheme is simple and ensures reliable delivery but performs poorly on high‑delay or high‑bandwidth links because only one frame can be outstanding at a time.

***

**Q17. What is a Hamming code? How does it detect and correct single‑bit errors?**

**Ans:**

- A Hamming code is a forward error‑correcting code that adds multiple parity bits to data bits such that the minimum Hamming distance between valid codewords is 3, allowing single‑bit error correction.
- In Hamming(7,4), data bits occupy positions 3,5,6,7 and parity bits at positions 1,2,4.
- At the receiver, recomputing the parity checks gives a 3‑bit syndrome; if it is 000, no error; otherwise its binary value points to the bit position in error, which can then be flipped to correct the codeword.

***

### 10‑mark question

**Q18. Compare Stop‑and‑Wait ARQ and Go‑Back‑N ARQ in terms of efficiency, buffer requirements, and implementation complexity. Use suitable diagrams to support your answer.**

**Ans:**

- Stop‑and‑Wait ARQ:
    - Sender sends one frame and waits; window size = 1.
    - Simple implementation, minimal buffer needed at sender and receiver.
    - Channel utilization low for long round‑trip times since most of the time is spent waiting for ACKs.
- Go‑Back‑N ARQ:
    - Sender maintains a sending window of N frames; can transmit multiple frames without waiting for individual ACKs.
    - Receiver typically keeps only next expected frame; out‑of‑order frames discarded.
    - On error or timeout for frame k, sender retransmits k and all subsequent frames in the window (hence name “Go‑Back‑N”).
    - Higher throughput on high delay–bandwidth products but with potential waste on multiple retransmissions.
- Diagrams should show timeline: sequence of frames, ACKs, and retransmissions in both protocols.
- In summary, Go‑Back‑N improves link utilization at the cost of more complex sender logic and potentially more retransmitted data.

***

## Unit 5 – Multiple Access and LANs

### 2‑mark questions

**Q19. Why is Slotted ALOHA more efficient than Pure ALOHA?**

**Ans:** In Slotted ALOHA, transmissions are only allowed to start at discrete time slots equal to frame duration, so collisions can only occur at slot boundaries, effectively halving the vulnerable period and doubling maximum throughput to about 36% compared to 18% in Pure ALOHA.

***

**Q20. What is the main function of a switch in an Ethernet LAN?**

**Ans:** An Ethernet switch operates at the data link layer, learns MAC addresses on its ports, and forwards frames only to the port associated with the destination MAC instead of broadcasting to all, thereby segmenting collision domains and improving performance.

***

### 5‑mark questions

**Q21. Explain the basic operation of CSMA/CD in classic Ethernet.**

**Ans:**

- Carrier Sense: a station listens to the channel; if it is idle, it begins transmission; if busy, it waits.
- Collision Detection: while transmitting, the station monitors the medium; if it detects a significant signal change (collision), it immediately stops sending and transmits a jamming signal to ensure all stations detect the collision.
- Backoff: after collision, each colliding station waits a random backoff time determined by the binary exponential backoff algorithm before trying again, reducing the chance of repeated collisions.
- This protocol worked with shared coaxial or hub‑based networks but is largely obsolete in full‑duplex switched Ethernet where there is no shared collision domain.

***

**Q22. Distinguish between a hub, a switch, and a router.**

**Ans:**

- Hub: a multiport repeater working at the physical layer; it blindly repeats incoming bits to all other ports, creating a single collision domain.
- Switch: a multiport bridge at the data link layer; it forwards frames based on MAC addresses, automatically learning which MACs are reachable via which ports, and thus separates collision domains.
- Router: a layer‑3 device that forwards packets based on IP addresses and routing tables, interconnecting different IP networks and supporting complex routing policies.

***

### 10‑mark question

**Q23. Explain ALOHA and CSMA multiple access protocols. Compare their performance and explain why Ethernet moved from ALOHA‑like schemes to CSMA/CD and then to switched full‑duplex.**

**Ans:**

- Pure ALOHA: users transmit whenever they have data; collisions happen if frames overlap in time; retransmissions occur after random delays; max throughput ≈ 18% at optimal load.
- Slotted ALOHA: time divided into slots; transmissions start at slot boundaries; reduces vulnerable period and doubles theoretical max throughput ≈ 36%.
- CSMA: stations sense the carrier before transmitting; if busy, delay; this reduces but does not eliminate collisions.
- CSMA/CD: adds collision detection, where transmitting stations monitor the medium and abort upon collision, sending jam signals and then performing exponential backoff.
- As link speeds and traffic demands increased, Ethernet moved to switched topologies with full‑duplex links, eliminating the shared collision domain so CSMA/CD is no longer necessary; each link behaves like a point‑to‑point circuit between NIC and switch port.

***

## Unit 6 – Network Layer

### 2‑mark questions

**Q24. What is the role of the TTL (Time To Live) field in an IPv4 header?**

**Ans:** The TTL field limits the lifetime of an IP packet by counting down at each hop; when it reaches zero, the packet is discarded and an ICMP “time exceeded” message may be sent, preventing packets from looping indefinitely in the network.

***

**Q25. Define static routing and dynamic routing.**

**Ans:** Static routing uses fixed routes manually configured by administrators, which do not change automatically when network conditions change. Dynamic routing uses routing protocols to allow routers to exchange information and adjust routes automatically in response to topology or load changes.

***

### 5‑mark questions

**Q26. Describe the general structure of an IPv4 address and differentiate between network and host portions.**

**Ans:**

- An IPv4 address is a 32‑bit identifier, commonly written in dotted decimal form (e.g., 192.168.10.5).
- Conceptually, it consists of a **network part** (identifying the subnet or network) and a **host part** (identifying the host within that network).
- Historically, classful addressing (Class A/B/C) defined fixed network/host splits; now classless addressing (CIDR) uses a network prefix length (e.g., /24) to indicate how many leading bits are the network part.
- Routers use the network prefix to make forwarding decisions; hosts use the host part and subnet mask to determine local vs remote destinations.

***

### 10‑mark question

**Q27. Explain how routing works in an IP network. Include in your answer: the purpose of routing tables, an example of a distance‑vector algorithm, and an example of a link‑state algorithm.**

**Ans:**

- Routers use **routing tables** mapping destination networks (prefixes) to next hops or outgoing interfaces; when a packet arrives, the router looks up the destination IP and chooses the best matching route based on longest prefix match.
- **Distance‑vector routing**: each router periodically advertises to its neighbors a vector of distances (e.g., hop counts) to all known destinations; routers update their tables based on neighbors’ information, using algorithms like Bellman–Ford (example protocol: RIP).
- **Link‑state routing**: each router discovers its neighbors and link costs, floods this info to all routers; all build an identical map of the network and independently compute shortest paths using Dijkstra’s algorithm (example protocol: OSPF).
- Distance‑vector is simpler but can suffer from count‑to‑infinity problems; link‑state converges faster and is more robust in larger, complex topologies, which is why modern enterprise and ISP networks mostly use link‑state or path‑vector protocols.

***

## Unit 7 – Transport Layer

### 2‑mark questions

**Q28. Name two main transport layer protocols in the TCP/IP suite and mention one key difference.**

**Ans:** Two main transport protocols are TCP (Transmission Control Protocol) and UDP (User Datagram Protocol). TCP is connection‑oriented and provides reliable, ordered delivery, whereas UDP is connectionless and does not guarantee delivery or ordering.

***

**Q29. What is meant by ‘flow control’ at the transport layer?**

**Ans:** Flow control is a mechanism by which a receiving host can limit the rate at which the sender transmits, preventing the sender from overwhelming the receiver’s buffer capacity. In TCP, this is implemented using a sliding window and an advertised receive window size in headers.

***

### 5‑mark questions

**Q30. With the help of a diagram, explain the three‑way handshake used by TCP to establish a connection.**

**Ans:**

- Step 1: Client sends a SYN segment with its Initial Sequence Number (ISN\_c = x) to the server, indicating desire to establish a connection.
- Step 2: Server responds with a SYN+ACK segment, acknowledging x+1 and providing its own ISN\_s = y.
- Step 3: Client sends an ACK segment acknowledging y+1; at this point the connection is established on both ends.

Diagram:

```text
Client                          Server
  SYN, Seq = x  --------------> 
                 <--------------  SYN+ACK, Seq = y, Ack = x+1
  ACK, Seq = x+1, Ack = y+1  -->
```

This handshake ensures both parties agree on initial sequence numbers and that the path is reachable in both directions, which helps avoid half‑open connections.

***

### 10‑mark question

**Q31. Compare TCP and UDP in terms of connection establishment, reliability, congestion control, overhead and typical applications.**

**Ans:**

- Connection establishment:
    - TCP uses three‑way handshake to establish a connection before data transfer; UDP is connectionless and does not establish a connection.
- Reliability:
    - TCP ensures reliable, in‑order delivery with retransmissions, sequence numbers, ACKs, and checksums; UDP does not guarantee delivery, order, or duplicate suppression (only an optional checksum for error detection).
- Congestion and flow control:
    - TCP implements flow control using sliding windows and receiver‑advertised window sizes, and congestion control using algorithms like slow start and congestion avoidance.
    - UDP has no built‑in congestion or flow control, leaving such logic to the application or relying on network fairness.
- Overhead:
    - TCP headers are larger (minimum 20 bytes, plus options), with more state to maintain; UDP headers are only 8 bytes and stateless in the network layer.
- Applications:
    - TCP is used by reliability‑sensitive applications like web browsing (HTTP/HTTPS), email (SMTP), file transfer (FTP), and remote login (SSH).
    - UDP is used by DNS, DHCP, VoIP, streaming media, online gaming, and other real‑time or simple request/response applications where small delays or losses are acceptable or handled at application level.

***

## Unit 8 – Application Layer: DNS, WWW, HTTP

### 2‑mark questions

**Q32. What is the function of the DNS protocol?**

**Ans:** DNS (Domain Name System) maps human‑readable domain names (like `www.example.com`) to IP addresses, enabling users to use names instead of numeric addresses.

***

**Q33. Name any two HTTP request methods and briefly state their typical use.**

**Ans:** Two HTTP methods are:

- GET – used to request a resource from the server without modifying it (e.g., fetching a web page).
- POST – used to send data to the server, typically to submit forms or upload data.

***

### 5‑mark questions

**Q34. Explain the basic steps that occur when a user enters a URL like `https://www.example.com` in a browser until the web page is displayed.**

**Ans:**

- The browser parses the URL to find protocol (HTTPS), host name (`www.example.com`), and path.
- It uses DNS to resolve `www.example.com` to an IP address, querying local cache and, if necessary, remote DNS servers.
- It establishes a TCP connection (and TLS/SSL for HTTPS) to the server’s IP and port 443 using the three‑way handshake.
- The browser sends an HTTP GET request specifying the path and host; the server processes the request and returns an HTTP response with status code and HTML content.
- The browser renders the HTML, fetching additional resources (images, CSS, JS) via further HTTP requests as needed.

***

### 10‑mark question

**Q35. Describe the structure and operation of DNS in detail. Include: DNS hierarchy, types of DNS servers, types of DNS records, and how a recursive query resolves a domain name.**

**Ans:**

- Hierarchy: DNS is organized as a tree with the root at top, below which are top‑level domains (TLDs) like `.com`, `.org`, `.in`, then second‑level domains (e.g., `example.com`), and hostnames (e.g., `www.example.com`).
- Server types:
    - Root servers (serve root zone data), TLD servers (e.g., `.com`), and authoritative name servers for specific domains (e.g., `example.com`).
    - Recursive/resolver servers (often at ISP) that perform queries on behalf of clients and cache results.
- Record types:
    - A/AAAA (IPv4/IPv6 address), CNAME (canonical name alias), MX (mail exchanger), NS (authoritative name server), TXT (text), etc.
- Recursive resolution of `www.example.com`:

1. Client asks its local recursive resolver.
2. Resolver checks cache; if no entry, it queries a root server for `.`, which points it to TLD servers for `.com`.
3. Resolver queries a `.com` TLD server for `example.com`, which returns NS records for the authoritative servers of `example.com`.
4. Resolver queries an authoritative server for `www.example.com`, which returns an A or AAAA record with IP address.
5. Resolver caches the result and replies to client, which can now open a TCP connection to the server.

***

If you want, I can now:

- Pull **only the questions** (without answers) into a separate block for self‑testing, or
- Create an ordered **unit‑wise PDF/Markdown “Question Bank”** that you can print and use alongside your notes.

<div align="center">⁂</div>

: https://www.recw.ac.in/v1.8/wp-content/uploads/2021/10/UNIT-1-DCS.pdf

: http://cectl.ac.in/images/pdf_docs/studymaterial/cse/s5/dc3.pdf

: https://mrcet.com/downloads/digital_notes/ECE/III%20Year/DIGITAL%20COMMUNICATIONS.pdf

: https://uomustansiriyah.edu.iq/media/lectures/6/6_2022_10_22!02_45_28_PM.pdf

: https://www.geeksforgeeks.org/electronics-engineering/digital-modulation-techniques/

: https://www.eecs.yorku.ca/course_archive/2010-11/F/3213/CSE3213_07_ShiftKeying_F2010.pdf

: https://www.freejobnotify.com/2025/08/tcp-ip-osi-model-mcqs-with-answers.html

: https://en.wikipedia.org/wiki/Internet_protocol_suite

: https://www.checkpoint.com/cyber-hub/network-security/what-is-the-osi-model-understanding-the-7-layers/osi-model-vs-tcp-ip-model/

: https://examradar.com/data-link-control-mcq-data-communication-networking/

: https://www.pluralsight.com/resources/blog/tech-operations/networking-basics-tcp-udp-tcpip-osi-models

: https://www.uninets.com/blog/osi-model-interview-questions-answers

: https://reck.ac.in/wp-content/uploads/2023/04/DCN_MCQ-Ashwini-.pdf

: https://examradar.com/switching-network-mcq-data-communication-networking/

: https://www.sanfoundry.com/network-security-assessment-questions/

: https://electronicspost.com/multiple-choice-questions-and-answers-on-telecommunication-and-switching-systems/

: https://www.geeksforgeeks.org/computer-networks/error-detection-in-computer-networks/

: https://www.youtube.com/watch?v=NbVJ3R1wUxE

: https://www.youtube.com/watch?v=zoyvTjxT9DI

: http://iete-elan.ac.in/QPDec08/AC12-7-J07.htm

: https://www.scribd.com/document/985359484/CN-unit-2

: https://www.geeksforgeeks.org/computer-networks/multiple-access-protocols-in-computer-network/

: https://bbsbec.edu.in/wp-content/uploads/2025/04/CN-QBank.pdf

: https://testbook.com/objective-questions/mcq-on-dns--5eea6a0939140f30f369d8ff

: https://gateatzeal.com/blogs/tcp-ip-layers-15-gate-level-questions/

: https://ssmahavidyalaya.edu.in/images/question_bank/computer_sc_question/Data%20communication_Networking%20Question_Bank.pdf

: https://www.scribd.com/document/820053633/Important-question-for-final-exam-DCCN

: https://www.scribd.com/document/916528275/Important-2-Mark-CN-Questions-1
