# Network

## First Sight

### Bandwidth

​    Network bandwidth is the amount of data that can be transmitted in unit time (typically 1 second), the ability of a network system's communication link (as agreed with the channel or transmission medium) to transmit data.

​     In daily life, the word "bandwidth" and "throughput" in a computer network can easily be confused. The difference is 

+ bandwidth: It emphasizes the maximum data transmission rate of the network, namely the peak of transmission data rate theory.
+ throughput: emphasize the actual data transmission rate of the network.

### Devices

#### Switch

​    Switch is a communication system in the completion of information exchange function equipment, which has these basic functions:

+ Like hubs, switches provide a large number of ports for cable connections, which can be routed using a star topology.
+ Like a repeater, hub, and bridge, when it transmits a frame, the switch reproduces a true square electrical signal.
+ Like a bridge, a switch USES the same forwarding or filtering logic on each port. 
+ Like Bridges, switches divide lans into multiple conflict domains, each with a separate broadband, which greatly increases the bandwidth of lans. 
+ In addition to features such as Bridges, hubs, and Repeaters, switches offer more advanced features such as virtual local area networks (VLAN) and higher performance

#### Router

​    A router is a device that works on the network layer. The router is responsible for transferring data packets from the source host to the destination host via the optimal path. Routers are mainly used for similar or heterogeneous lans and the interconnection between lans and wans. A network interconnection device that connects different logical subnets. Routers have the capability of heterogeneous network interconnection, wan interconnection, and isolation of broadcast information.

## IP

### IPV4&IPV6

| Description | IPv4                                                         | IPv6                                                         |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| header      | A 32-bit (4-byte) address consists of the network and host parts, depending on the address class. Depending on the first few digits of the address, various address classes can be defined: A, B, C, D, or E. The total number of IPv4 addresses is 4 294 967 296. The text format of the IPv4 address is nnn.nnn.nnn, where 0<= NNN <=255, and each n is a decimal number. Leading zeros can be omitted. The maximum number of characters to print is 15, no mask allowed. | The basic architecture of 128-bit (16 bytes) is 64 and the host number is 64. Typically, the host portion of an IPv6 address (or part thereof) is derived from the MAC address or other interface identifier. Based on the subnet prefix, the architecture of IPv6 is more complex than the architecture of IPv4. The number of IPv6 addresses is 1028 (79 228 162 514 264 337 593 543 950 336) times greater than the number of IPv4 addresses. IPv6 address of text format for XXXX: XXXX: XXXX: XXXX: XXXX: XXXX: XXXX: XXXX, each of which x is a hexadecimal number, according to four. Leading zeros can be omitted. You can use a double colon (::) once in the text format of the address to specify any number of zeros. For example, :: FFFF :10.120.78.40 represents the ipv4-mapped IPv6 address |
| DNS         | The application USES the socket API gethostbyname() to accept the host name and then USES DNS to get the IP address.The application also accepts the IP address, and then USES DNS and gethostbyaddr() to get the host name.For IPv4, the reverse lookup field is in-addr-arpa. | IPv6 is also supported. Support for IPv6 using AAAA (four A) record type and reverse lookup (IP to name). Applications can choose to accept IPv6 addresses from DNS and then communicate using IPv6. The socket API gethostbyname() supports IPv4 only. For IPv6, use the new getaddrinfo() API to get IPv6 only or IPv4 and IPv6 addresses (on application selection). For IPv6, the domain used for reverse lookup is ip6.arpa, and if it cannot be found, ip6.int is used. |
| FTP         | FTP allows files to be sent and received over the network.   | FTP allows files to be sent and received over the network.   |
| ARP         | IPv4 USES ARP to find physical addresses associated with IPv4 addresses (such as MAC or link addresses) | IPv6 USES Internet control message protocol version 6 (ICMPv6) to embed these features into the IP itself as part of the stateless automatic configuration and neighborhood discovery algorithm. Therefore, there is no such thing as ARP6. |
| DHCP        | DHCP is used to dynamically obtain IP addresses and other configuration information. IBM I supports the use of DHCP servers for IPv4. | DHCP implemented through IBM I does not support IPv6. However, you can implement it using the ISC DHCP server. |
| socket API  | Applications use TCP/IP by using these apis. Applications that do not require IPv6 are not affected by socket changes made to support IPv6. | IPv6 USES the new address family: AF_INET6 to enhance the socket so that applications can now use IPv6. These enhancements have been designed so that existing IPv4 applications are completely free of IPv6 and API changes. Applications that want to support concurrent IPv4 and IPv6 communication or pure IPv6 communication can easily adapt the ipv4-mapped IPv6 address format :: FFFF: A.B.C.D, where A.B.C.D is the IPv4 address of the client. The new API also supports transforming IPv6 addresses from text to binary and from binary to text. |

### Address

​    IP header: a behavior of 32 bits (0~31), a total of five lines, a total of 20 bytes. Contains source IP address (32-bit) and destination IP address; It could be longer than 20 bytes; IPV4 characteristic;

![img](https://img-blog.csdn.net/20170713161451457?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzI4NjM2MzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

​    The IP address range: 000000000.000000000.000000000.000000000 ~ 11111111. 11111111. 11111111.11111111 is 0.0.0.0 to 255.255.255.255.

​    Routing is communication across the network

​    The number of all iP's is greater than 2 to the power 32;

​    Class A IP: the first number represents different network segment, behind three digits represent the host number, number change is not A network, the first three digits after random change, represent different hosts within the same network segment, the largest number of network 2 ^ 7-2, the largest host 24 - the number 2 ^ 2 (1.0.0.0 on behalf of the network itself cannot be assigned, 1.255.255.255 represent the current broadcast network address).

​    Class B IP: the first two Numbers represent different segments, the latter two digits represent the host number, maximum network number 2 ^ 14, the largest host number 2 ^ 16-2;

​    Class C IP: the first three number represent different segments, the largest number of network 2 ^ 21, the largest number of host 2 ^ 8-2;

![img](https://img-blog.csdn.net/20170713161522608?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzI4NjM2MzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## Building Connection

![这里写图片描述](https://img-blog.csdn.net/2018031615485873?watermark/2/text/Ly9ibG9nLmNzZG4ubmV0L2FhYV9hX2JfYw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)