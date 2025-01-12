During the Cold War, America had built a program called the ARPA ( Advanced Research Projects Agency) to get ahead of Soviet Union in technical discoveries.

Now as a part of ARPA, there were 4 Research centers located in 4 American colleges namely : MIT, Stanford, UCLA and University of Utah. Now for these 4 research centers needed to communicate with each other so they developed a system called the ARPAnet.

## Ports:

MongoDB runs on port 27017, local host runs on port 8080, 3000

Ports help to distinguish different services or applications running on the same device allowing multiple services to coexist and communicate simultaneously.

Ports are 16 bit numbers, so they can range between 0 to (2^16 - 1) 65535, and they are divided in three categories:

1. Well Known Ports: 0 → 1023: reserved for standard services like http (port 80) , https (port 443) and ftp port 21. These ports are standardized and well known across different systems.
2. Registered Ports : 1024 to 49151 ( used for various application and services, postgres 5432, redis 6379)
3. Dynamic or private ports: 49152 to 65535: used for temporary or private purposes. Applications often dynamically choose ports from this range when they need to communicate

## Mbps

Q: What does it mean if my speed is 1 mbps ( download)

⇒ Mbps stand for megabits per second, and its a unit of measurement used to describe data transfer speed in a network. When speed is 1 mbps, it means that your network connection is capable of transmitting 1 million bits of data per second.

## Submarine Cable Map

Your home and office are 2km away, what you do is you lay out a cable from your office direct to your home, that connects the office computer and your home computer, this is basically what Internet is. Now you can communicate as much as you want with your office computer, therefore ( Internet) is free, what’s costly is laying out that cable and maintaining that cable.

Internet at the end of the day is basically a network of computers/servers. So if I want to connect to a server that is located in US, how would I do that, there are two ways:

1. Satellite: Costly, they cannot carry terabytes of data for less than a billion dollars
2. Physical Connections ⇒ Submarine Cables

Big private companies of the world have laid out cables all over the sea bed, which they call the internet. These are the tier 1 companies. [Tier 1 network - Wikipedia](https://en.wikipedia.org/wiki/Tier_1_network)

So if you want to connect to any website which has its server outside india, then your request will go through any of the landing stations in India. ( Mumbai, Cochin, Trivandrum, Tuticron, Chennai)

Then their are tier2 ISP’s like ( Vodafone, Easynet, Jio, Airtel, BSNL) and then there are tier-3 ISP’s like (tikona, siti cable etc)

The Submarine cable map have optical fibres inside them. These fibre optic cables carry DWDM laser signals ( TCP/IP packets).

Each fibre is exactly the size of strand of hair ( it is made up of exiquistly high quality glass)

> For one, ruptures aren’t exactly an anomaly. One of the [estimated](https://blog.telegeography.com/frequently-asked-questions-about-undersea-submarine-cables) 428 undersea cables worldwide is damaged every couple of days. Nearly all faults aren’t intentional. They’re caused by underwater earthquakes, rock slides, anchors, and boats. That’s not to say that humans are incapable of purposefully messing with the cables; off the coast of Vietnam in 2007, fishermen [pulled up](https://www.computerworld.com/article/2541664/networking/fishermen-pull-the-plug-on-vietnam-s-web--steal-cable-for-scrap.html) 27 miles of fiber cords, disrupting service for several months. (It wasn't cut off completely, because the country had one more cable that kept the internet going.)

These are not attacked by sharks because they are protected heavily by stainless steel. polyethylent protective yarn layer is also present on these cables. There are also a lot of backup cables, even if one cable gets damaged.

You could see where is request is going when you type [zebpay.com](http://zebpay.com) in your broswer

```bash
=> **tracert zebpay.com**

Tracing route to zebpay.com [2606:4700:8393:a242:f139:14a:e672:3f72]
over a maximum of 30 hops:

  1     3 ms     4 ms     3 ms  2401:4900:1c53:6793:b6a7:c6ff:fe25:fd48 => (Delhi, India, Bharti Airtel)
  2     6 ms     6 ms     6 ms  2401:4900:1c0a:8fff::1 => (Delhi, India, Bharti Airtel)
  3     7 ms    36 ms     6 ms  2404:a800:1a00:209::39 => (Delhi, India, Bharti Airtel)
  4     7 ms     6 ms     5 ms  2404:a800::208 => ( Mumbai, Maharashtra, India, Bharti Airtel)
  5    12 ms     7 ms    39 ms  2404:a800:0:29::cf => (Mumbai, Maharashtra, India, Bharti Airtel)
  6    10 ms     5 ms     8 ms  2606:4700:8393:a242:f139:14a:e672:3f72 => ( San Francisco, California, US, CloudFlare Inc.)

Trace complete.
```

## LAN, MAN, WAN

1. LAN: Local Area Network , small house . office ( connected using ethernet, wifi)
    1. One can create a local area network (LAN) without internet access for the sole purpose of connecting computers and transferring files between them. This type of network is often referred to as an "offline LAN" or an "isolated LAN.”
2. MAN: Metroplitan Area Network
3. WAN: Wide Area Network ( connected using optical fibre cables)

**The internet is the WAN.**

## Modem

A modem is short for “modulator-demodulator”. Its primary function is to modulate (convert) digital data from your computer into analog signals for transmission over the communication medium (eg phone lines, cable lines, fiber optics) and demodulate incoming analog signals back into digital data that your devices can understand. Essentially a modem connects your local network to your Internet Service Provider (ISP) network.

## Routes

Routers move data packets between devices on local network and also between local network and external network. It moves data packets between Ip addresses.

→ The modem is responsible for sending and receiving signals from the ISP, while the router disperses the signal to the devices on the network.

→ general: myself -> router -> modem -> internet

## Topologies

1. BUS
    
    1. All devices are connected on a single central cable.
    2. Data transmission is bi-directional.
    3. Pros: Simple and inexpensive to setup, works well for small networks with low traffic
    4. Cons: prone to collisions (two devices try to send data at the same time), not scalable for larger networks, if the central cable fails entire thing can go down
2. RING
    
    1. devices are connected in a circular fashion, with each device connecting two more devices, forming a closed loop.
    2. data travels in one direction around the ring
    3. Pros: Easy to install, no collisions, predictable path of data
    4. Cons: If one device fails, it can disrupt the entire network, adding or removing devices can be challenging
3. STAR
    
    1. Each device is connected to a central hub of switch.
    2. All communication pass through central hub or switch
    3. Pros: Easy to install and manage, failure of one device does not lead to failure of other devices
    4. Cons: Central Hub is SPOF
4. TREE (BUS + STAR)
    
    1. devices are arranged in a hierarchical structure, similar to a tree.
    2. happens in large networks multiple star networks are connected via a bus.
    3. provides scalability and organization but complex to set up.
    
    ![[Pasted image 20250112162950.png]]
5. MESH
    
    1. Every device is connected to every other device in the network.
    2. Two types of mesh: full mesh (every device connects every other) and half mesh (only some devices connect to others)
    3. Pros: Redundancy and fault tolerance, if one link or device fails, traffic can be rerouted via other paths
    4. Cons: increasing cost and complex to manage as network grows

## OSI Model

The Open-Source Intercommunication (OSI) model describes the seven layers that computer systems use to communicate over a network.

This model is basically used to understand how data is transferred from one computer to another in a computer network.

![[Pasted image 20250112162901.png|400]]

1. Application Layer
    
    1. Application Layer is used by Network applications (firefox, chrome, outlook, skype)
    2. Network Applications can also be called end user software.
    3. It provides protocols that allow software to send and receive information and present meaningful data to users.
        1. File Transfer→ FTP
        2. Web Surfing → Http, Https
        3. Emails → SMTP
        4. Virtual Terminals → Telnet
    4. Application layers provide services for network applications, with the help of protocols to perform user activities.
2. Presentation Layer
    
    1. Presentation Layer receives data from application layer, this data is in the form of characters and numbers
    2. Presentation layer basically performs three different functions, Translation, Data compression, Encryption/Decryption
    3. This layers converts these characters and numbers into machine understandable binary format, e.g. ASCII to EBCDIC (Extended Binary Coded Decimal Interchange Code). This is called **Translation**
    4. Before transmitting presentation layer reduces the number of bits to represent that data, this bit reduction process is called **Data Compression**. Data compression can be lossy or loseless
        1. The key difference between lossy and lossless compression is the tradeoff between size reduction and data quality preservation.
        2. Lossless compression retains all data, resulting in smaller but identical files, while lossy compression sacrifices some data to achieve greater file size reduction, with a potential impact on quality, which is often imperceptible to the human senses in practice.
    5. To maintain the integrity of data, before transmission the data is **encrypted** using SSL protocol.
        1. SSL Protocol → It is a deprecated cryptographic protocol that was designed to provide secure communication over a computer network, particularly for a web traffic.
        2. SSL was designed to encrypt data transmitted between a web browser and a web server. It ensures that the data exchanged between these endpoints such as login credentials, credit card information and other sensitive data is kept confidential and secure.
        3. It was succeeded by the more secure Transport Layer Security ( TLS) protocol, which is commonly referred as SSL/TLS
3. Session Layer
    
    1. The session layer creates communication channels, called sessions, between devices. It is responsible for opening sessions, ensuring they remain open and functional while data in being transferred and closing them when communication ends. The session layer also sets up checkpoints during the data transfer- if the session is interupted, devices can resume data transfer from last checkpoints
        
    2. Some of its functionalities are:
        
        1. **Session Establishment** : It handles the setup and initiation of communication sessions. This involves negotiating session parameters such as session duration, security mechanisms and synchronization points between devices
        2. **Data Synchronization:** Data transmitted between devices should be properly synchronized. It manages checkpoints and synchronization points to enable retransmission of data in case of network failures
        3. **Dialog Control**: This layer manages the orderly exchange of data between devices by controlling the dialog. It define who can transmit at a given time for how long, preventing both devices from attempting to transmit simultaneously
        4. **Session Maintenance**: It monitors the session and can perform various tasks to keep it acitve, such as detecting idle sessions and taking action to prevent them from timing out
        5. **Session Termination**: When the communication session is complete, the Session Layer is responsible for terminating it gracefully. This includes cleaning up resources , ensuring all data is transmitted, and releasing any session related state information
    3. Transport layer
        
        1. Transport layer provides end to end communication between devices in different networks.
        2. Data unit at this layer is called segments
        3. Segmentation and Reassembly
            1. The transport layer takes the data transferred in the session layer and breaks it into “segments” on the transmitting end.
            2. It is responsible for reassembling the segments on the receiving end, turning it back into data that can be used by the session layer.
        4. Flow Control
            1. The transport layer carries out flow control, sending data at a rate that matches the connection speed of the receiving device.
            2. This prevents congestion(excessive data transfer) and ensures efficient data transfer. Server can send at a speed of 100mbps and receiver can only recieve at 10 mbps, so if the server is sending it 100, transport layer will bring down the data transmission rate to 10, and in case if the server is sending at 5, it can bring up the data tranmission rate to 10 mbps.
        5. Error Control:
            1. It has error detection mechanisms to identify any errors that may occur during data transmission.
            2. If errors are detected, some transport layer protocols (e.g. TCP) can request retransmission of the affected data to ensure its integrity.
        6. TCP and UDP are two common protocols of transport layer
4. Network Layer
    
    1. The network layer is responsible for routing data packets between devices in different networks and ensuring data reaches its destination
    2. Data unit layer at this level is called a Packet
    3. Logical addressing is done at network layer where senders and receivers IP addresses are joined with the segment to form a data packet
    4. Routers exist in this layer.
    5. Routing : Determines the best path for data to travel from source to destination using routing algorithms. It also takes into account network topology and traffic conditions.
5. Data Link Layer
    
    1. Data unit in data link layer is called a frame
        ![[Pasted image 20250112162836.png]]
    2. The Data link layer is divided into two sub layers: LLC and MAC.
        
    3. Media Access Control Layer (MAC )
        
        1. Addressing/ Frame Encoding and Decoding
            - Physical addressing is done at data link layer where mac addresses of sender and receiver are attached to the data packet to form the frame
            - MAC address is a 12 digit alphanumeric number embedded in Network interface card of your computer by the computer manufacturer
            - These frames also contain information about error detection and correction codes that help ensure the integrity of the data as it is transmitted over the physical medium
            - It sends those frames bit-by-bit to the underlying physical layer.
            - When receiving the data, it decodes these frames to extract the original packets.
        2. The data link layer also manages the access to the physical medium when multiple devices share it. This is crucial in networks like Ethernet, where multiple devices contend for access to the same cable or wireless channel. MAC Protocols determine when device can transmit data at a given time to avoid collisions
    4. Logical Link Control (LLC)
        
        1. The LLC sub layer deals with network layer protocols and ensures that multiple network layer protocols can co-exist on the same physical medium.
        2. It ensures synchronization, multiplexing ( multiple analog and digital signals combined into one), flow control and even error checking functions of data link layer.
    5. Physical Layer
        
        1. The primary role of physical layer is to define the physical characteristics of the communication medium and the means of transmitting raw data bits over that medium,
        2. Physical Medium Definition
            1. Physical layer defines the physical medium used for the data transmission
            2. This can include copper wires, optical fibers, wireless radio waves and more.
        3. Data Encoding and Signaling
            1. It is responsible for encoding data into electrical, optical or radio wave signals that can be transmitted over the chosen medium.
        4. Bit Synchronization
            1. The Physical Layer ensures that the sender and receiver are synchronized in terms of when a bit starts and ends. This synchronization is essential for the receiver to accurately interpret the received data
        5. Data Transmission Rate (Bit Rate):
            1. It defines the data transmission rate or bit rate which is the rate at which raw data bits are sent over the medium.
            2. The bit rate can vary depending upon the technology and medium used.

→ The first four layers are responsibility of the host and the bottom 3 layers are the responsibility of the network

→ Data moves like this,

→ Data segmented by transport layer.

→ Placed into packets by network layer.

→ and then framed by data link layer which is a sequence of binary 0’s and 1’s

→ Physical layer converts this binary sequence into signals that can transmit over local media

→ at the client side, signals received are converted into binary sequence then frames, then packets and then segments.

![[Pasted image 20250112162713.png]]
## TCP/IP Model

> A host at its core is basically a computer which runs 24/7

## Client Server vs Peer to Peer

1. **Client server architecture** is a computing model in which the client and server are two distinct entities that communicate with each other over the network. The client is responsible for requesting services from the server while the server is responsible for providing those services.
2. **Client server network:** The physical implementation of the client server architecture is called the Client server network. The network can be local area network, wide area network or the internet. The network provides the communication path between the clients and the servers.
3. **Peer to Peer Architecture:** It is a computing model in which individual devices, often referred to **peers**, connect directly to each other to share resources, data or services without the need for a centralized server or authority. In a P2P network, all participating devices have equal status and **can act as both clients and server**, facilitating direct communication and collaboration between them.
4. **Peer to Peer Network:** It is a physical implementation of the peer-to-peer architecture. It allows peer nodes to connect, communicate and share resources directly. It can be LAN, MAN or WAN network. The network provides the communication path between the peers.

## Networking devices

1. **Repeater:**
    1. As data travels over long distances in network cables, it can lose strength and clarity (become weak and corrupted) due to factors like attenuation (signal loss) and noise interference.
    2. A repeater is typically placed on the physical layer along the transmission medium (such as a network cable) where it can amplify and regenerate signals. The primary purpose of a repeater is to receive the incoming signals, from one section of the cable, amplify and clean those signals, and then retransmit them to another section of the cable, effectively extending the reach of the network.
2. **Hub**
    1. A hub is network device that connects multiple devices together. It also operates on the physical layer of the network.
    2. If there are 4 devices connected to hub, 1,2,3,4. Whenever any of the devices sends a data packet to the hub , it is transmitted to all three other devices. When a hub receives a data packet, it broadcasts it to all of its ports. This means all devices connected to the hub can see the packet even it was not intended for them. This can lead to network congestion and performance problems.
    3. It is not intelligent and has security concerns
    4. There are 3 different types of hubs
        1. Passive hub: It does not amplify or regenerate incoming signals. Simply broadcasts the incoming data to all other connected ports
        2. Active hub: It is also known as multiport repeater. Amplifies and regenerates the incoming signals before forwarding them to all other ports
        3. Intelligent hub: