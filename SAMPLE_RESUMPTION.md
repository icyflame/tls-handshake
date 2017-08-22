## Session Resumption during the Handshake

> The trace of a session resumption with github.com

### Summary of the handshake

```
Frame Number | Time | Source | Destination | Protocol | Length | Message Info
29	0.924125949	10.109.29.29	172.16.2.30	TLSv1.2	273	Client Hello
40	1.205647629	172.16.2.30	10.109.29.29	TLSv1.2	210	Server Hello, Change Cipher Spec, Encrypted Handshake Message
41	1.206335824	10.109.29.29	172.16.2.30	TLSv1.2	105	Change Cipher Spec, Hello Request, Hello Request
Frame Number | Time | Source | Destination | Protocol | Length | Message Info
```

### Detailed packet trace of the handshake

```
29	0.924125949	10.109.29.29	172.16.2.30	TLSv1.2	273	Client Hello

Frame 29: 273 bytes on wire (2184 bits), 273 bytes captured (2184 bits) on interface 0
Ethernet II, Src: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61), Dst: Cisco_60:22:bf (c8:9c:1d:60:22:bf)
Internet Protocol Version 4, Src: 10.109.29.29, Dst: 172.16.2.30
Transmission Control Protocol, Src Port: 42280, Dst Port: 8080, Seq: 202, Ack: 96, Len: 219
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: github.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Client Hello
        Content Type: Handshake (22)
        Version: TLS 1.0 (0x0301)
        Length: 214
        Handshake Protocol: Client Hello
            Handshake Type: Client Hello (1)
            Length: 210
            Version: TLS 1.2 (0x0303)
            Random
                GMT Unix Time: Nov  5, 2008 17:17:49.000000000 IST
                Random Bytes: 32a22253e45f3d34adf984e4914a304011f662837e21d6f1...
            Session ID Length: 32
            Session ID: 9bb2a500b3263bc881d1d54718d2e706361f7af4c478a30b...
            Cipher Suites Length: 30
            Cipher Suites (15 suites)
                Cipher Suite: TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (0xc02b)
                Cipher Suite: TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (0xc02f)
                Cipher Suite: TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (0xcca9)
                Cipher Suite: TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (0xcca8)
                Cipher Suite: TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (0xc02c)
                Cipher Suite: TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (0xc030)
                Cipher Suite: TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA (0xc00a)
                Cipher Suite: TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA (0xc009)
                Cipher Suite: TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (0xc013)
                Cipher Suite: TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (0xc014)
                Cipher Suite: TLS_DHE_RSA_WITH_AES_128_CBC_SHA (0x0033)
                Cipher Suite: TLS_DHE_RSA_WITH_AES_256_CBC_SHA (0x0039)
                Cipher Suite: TLS_RSA_WITH_AES_128_CBC_SHA (0x002f)
                Cipher Suite: TLS_RSA_WITH_AES_256_CBC_SHA (0x0035)
                Cipher Suite: TLS_RSA_WITH_3DES_EDE_CBC_SHA (0x000a)
            Compression Methods Length: 1
            Compression Methods (1 method)
                Compression Method: null (0)
            Extensions Length: 107
            Extension: server_name
            Extension: Extended Master Secret
            Extension: renegotiation_info
            Extension: elliptic_curves
            Extension: ec_point_formats
            Extension: SessionTicket TLS
            Extension: Application Layer Protocol Negotiation
            Extension: status_request
            Extension: signature_algorithms

```

```
40	1.205647629	172.16.2.30	10.109.29.29	TLSv1.2	210	Server Hello, Change Cipher Spec, Encrypted Handshake Message

Frame 40: 210 bytes on wire (1680 bits), 210 bytes captured (1680 bits) on interface 0
Ethernet II, Src: Cisco_60:22:bf (c8:9c:1d:60:22:bf), Dst: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61)
Internet Protocol Version 4, Src: 172.16.2.30, Dst: 10.109.29.29
Transmission Control Protocol, Src Port: 8080, Dst Port: 42280, Seq: 96, Ack: 421, Len: 156
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: github.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Server Hello
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 100
        Handshake Protocol: Server Hello
            Handshake Type: Server Hello (2)
            Length: 96
            Version: TLS 1.2 (0x0303)
            Random
                GMT Unix Time: Aug 27, 1986 08:55:34.000000000 IST
                Random Bytes: cd83b9ec2e5e564410cbf11dded7052bed9685a00b3a41b7...
            Session ID Length: 32
            Session ID: 9bb2a500b3263bc881d1d54718d2e706361f7af4c478a30b...
            Cipher Suite: TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (0xc02f)
            Compression Method: null (0)
            Extensions Length: 24
            Extension: renegotiation_info
            Extension: Extended Master Secret
            Extension: Application Layer Protocol Negotiation
    TLSv1.2 Record Layer: Change Cipher Spec Protocol: Change Cipher Spec
        Content Type: Change Cipher Spec (20)
        Version: TLS 1.2 (0x0303)
        Length: 1
        Change Cipher Spec Message
    TLSv1.2 Record Layer: Handshake Protocol: Encrypted Handshake Message
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 40
        Handshake Protocol: Encrypted Handshake Message
```

```
41	1.206335824	10.109.29.29	172.16.2.30	TLSv1.2	105	Change Cipher Spec, Hello Request, Hello Request

Frame 41: 105 bytes on wire (840 bits), 105 bytes captured (840 bits) on interface 0
Ethernet II, Src: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61), Dst: Cisco_60:22:bf (c8:9c:1d:60:22:bf)
Internet Protocol Version 4, Src: 10.109.29.29, Dst: 172.16.2.30
Transmission Control Protocol, Src Port: 42280, Dst Port: 8080, Seq: 421, Ack: 252, Len: 51
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: github.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Change Cipher Spec Protocol: Change Cipher Spec
        Content Type: Change Cipher Spec (20)
        Version: TLS 1.2 (0x0303)
        Length: 1
        Change Cipher Spec Message
    TLSv1.2 Record Layer: Handshake Protocol: Multiple Handshake Messages
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 40
        Handshake Protocol: Hello Request
            Handshake Type: Hello Request (0)
            Length: 0
        Handshake Protocol: Hello Request
            Handshake Type: Hello Request (0)
            Length: 0
```
