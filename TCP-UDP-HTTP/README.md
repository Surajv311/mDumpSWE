
# TCP-UDP-HTTP

(From Opensource Github repos knowledge extraction section | system-design-primer):
TCP is a connection-oriented protocol over an IP network. Connection is established and terminated using a handshake. All packets sent are guaranteed to reach the destination in the original order and without corruption through:
- Sequence numbers and checksum fields for each packet
- Acknowledgement packets and automatic retransmission
If the sender does not receive a correct response, it will resend the packets. If there are multiple timeouts, the connection is dropped. TCP also implements flow control and congestion control. These guarantees cause delays and generally result in less efficient transmission than UDP.
To ensure high throughput, web servers can keep a large number of TCP connections open, resulting in high memory usage. It can be expensive to have a large number of open connections between web server threads and say, a memcached server. Connection pooling can help in addition to switching to UDP where applicable.
TCP is useful for applications that require high reliability but are less time critical. Some examples include web servers, database info, SMTP, FTP, and SSH.
Use TCP over UDP when:
- You need all of the data to arrive intact
- You want to automatically make a best estimate use of the network throughput

UDP is connectionless. Datagrams (analogous to packets) are guaranteed only at the datagram level. Datagrams might reach their destination out of order or not at all. UDP does not support congestion control. Without the guarantees that TCP support, UDP is generally more efficient. UDP can broadcast, sending datagrams to all devices on the subnet. This is useful with DHCP because the client has not yet received an IP address, thus preventing a way for TCP to stream without the IP address.
UDP is less reliable but works well in real time use cases such as VoIP, video chat, streaming, and realtime multiplayer games.
Use UDP over TCP when:
- You need the lowest latency
- Late data is worse than loss of data
- You want to implement your own error correction

Note: There is always a layer above TCP. The question is really about how much overhead the stuff above TCP adds. HTTP is relatively chunky because each transmission requires a bunch of header cruft in both the request and the response. It also tends to be used in a stateless mode, whereby each request/response uses a separate TCP session. Keep-alives can ameliorate the session-per-request, but not the headers.

(From: [rohan-paul/Awesome-JavaScript-Interviews _al](https://github.com/rohan-paul/Awesome-JavaScript-Interviews/blob/master/Web-Development-In-General/HTTP-and-TCP-Difference.md))
TCP (Transmission Control Protocol) vs HTTP (HyperText Transfer Protocol)

1. The most fundamental difference between the two is that TCP and HTTP works at different layers, i.e, they have independent (and radically different ) tasks to perform. TCP is a transport-layer protocol, and HTTP is an application-layer protocol that runs over TCP.
2. TCP is invisible to most end users, providing the standards for moving packets of information from one computer to another, whereas HTTP is an “application layer protocol” that makes itself known every time someone types in a URL
3. TCP works in the Transport layer while HTTP works in Application layer of TCP/IP model. This just means that HTTP works on top of TCP. TCP is in charge of setting up a reliable connection between two machines and HTTP uses this connection to transfer data between the server and the client. HTTP is used for transferring data while TCP is in charge of setting up a connection which should be used by HTTP in the communication process. Without TCP, HTTP cannot function (to be crisp).
4. HTTP is a top layer(application layer) protocol that takes the payload(data of user), adds it's own header bits(required for control purposes) and passes down the package to a layer below. TCP is a middle layer protocol whose main job is to chop the payload coming from above layers into multiple segments so that they can be transmitted(because there are packet size limitations, MTU-maximum transmission unit). TCP adds it's own header bits to each of the segments and then passes them to the layer below.
5. Also, Look at the steps below in a high level that occurs at the background when a user tried to access a website: DNS Resolution -> TCP Handshake -> HTTP using the connection to exchange information between two machines.
6. TCP is a protocol that controls reliable and smooth transfer of DATA from source host :port to a destination host:port. It takes care of in-order and reliable delivery of a BYTESTREAM of data. It does NOT interpret the bytes within the DATA. TCP also employs rate control mechanisms (cong. mgmt.) in order to use the network BW optimally while at the same time be not greedy. HTTP on the other hand is only interested in using the BYTESTREAM to demarcate it into messages between a WebServer and WebClient/browser. It uses TCP to transfer the messages, so it doesn’t have to worry about sequence, reliability or worry about the size of message. There are command primitives like GET, POST, etc., for client to communicate with server and request which data it wants from the server.
7. To use an analogy, TCP is your Postal Service, and HTTP is your letters, words, messages, requests and commands that go into the envelopes. The Postal Service just focuses on delivering the letter to the sender..

So, here is in some more details; To understand the difference (and a lot of other networking topics), you need to understand the idea of a layered networking model. Essentially, there are different protocols that let a computer talk at different distances and different layers of abstraction:
- At the very bottom of the network stack is the physical layer: This is where electrical signals or light pulses or radio waves actually transmit information from place to place. The physical layer doesn't really have protocols, but instead has standards for voltages, frequencies, and other physical properties. You can transmit information directly this way, but you need a lot of power or a dedicated line, and without higher layers you won't be able to share bandwidth.
- The next layer up is the link layer: This layer covers communication with devices that share a physical communications medium. Here, protocols like Ethernet, 802.11a/b/g/n, and Token Ring specify how to handle multiple concurrent accesses to the physical medium and how to direct traffic to one device instead of another. In a typical home network, this is how your computer talks to your home "router."
- The third layer is the network layer: In the majority of cases, this is dominated by Internet Protocol (IP). This is where the magic of the Internet happens, and you get to talk to a computer halfway around the world, without needing to know where it is. Routers handle directing your traffic from your local network to the network where the other computer lives, where its own link layer handles getting the packets to the right computer.
- The transport layer takes care (The home of TCP): Now we can talk to a computer somewhere around the world, but that computer is running lots of different programs. How should it know which one to deliver your message to? The transport layer takes care of this, usually with port numbers. The two most popular transport layer protocols are TCP and UDP. TCP does a lot of interesting things to smooth over the rough spots of network-layer packet-switched communication like reordering packets, retransmitting lost packets, etc. UDP is more unreliable, but has less overhead.
- The application-layer (home of HTTP): So we've connected your browser to the web server software on the other end, but how does the server know what page you want? How can you post a question or an answer? These are things that application-layer protocols handle. For web traffic, this is the HyperText Transfer Protocol (HTTP). There are thousands of application-layer protocols: SMTP, IMAP, and POP3 for email; XMPP, IRC, ICQ for chat; Telnet, SSH, RDP for remote administration; etc.

These are the five layers of the TCP/IP networking model, but they are really only conceptual. The OSI model has 7 layers. In reality, some protocols shim between various layers, or can work at multiple layers at once. TLS/SSL for instance provides encryption and session information between the network and transport layers. Above the application layer, Application Programming Interfaces (APIs) govern communication with web applications like Quora, Twitter, and Facebook.

----------------------------------------------------------------------





















