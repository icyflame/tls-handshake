## New Session Handshake

> The trace for an actual handshake with icons.duckduckgo.com:

### Summary of the handshake

```
Frame Number | Time | Source | Destination | Protocol | Length | Message Info
416	8.056860004	10.109.29.29	172.16.2.30	TLSv1.2	251	Client Hello
447	8.213087440	172.16.2.30	10.109.29.29	TLSv1.2	1514	Server Hello
448	8.213206002	172.16.2.30	10.109.29.29	TLSv1.2	1514	Certificate[TCP segment of a reassembled PDU]
450	8.213226658	172.16.2.30	10.109.29.29	TLSv1.2	566	Certificate Status, Server Key Exchange, Server Hello Done
451	8.217641126	10.109.29.29	172.16.2.30	TLSv1.2	180	Client Key Exchange, Change Cipher Spec, Hello Request, Hello Request
489	8.376575327	172.16.2.30	10.109.29.29	TLSv1.2	381	New Session Ticket, Change Cipher Spec, Encrypted Handshake Message, Application Data
Frame Number | Time | Source | Destination | Protocol | Length | Message Info
```

### Detailed packet trace of the handshake

```
416	8.056860004	10.109.29.29	172.16.2.30	TLSv1.2	251	Client Hello

Frame 416: 251 bytes on wire (2008 bits), 251 bytes captured (2008 bits) on interface 0
Ethernet II, Src: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61), Dst: Cisco_60:22:bf (c8:9c:1d:60:22:bf)
Internet Protocol Version 4, Src: 10.109.29.29, Dst: 172.16.2.30
Transmission Control Protocol, Src Port: 41640, Dst Port: 8080, Seq: 222, Ack: 96, Len: 197
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Client Hello
        Content Type: Handshake (22)
        Version: TLS 1.0 (0x0301)
        Length: 192
        Handshake Protocol: Client Hello
            Handshake Type: Client Hello (1)
            Length: 188
            Version: TLS 1.2 (0x0303)
            Random
                GMT Unix Time: Jul  3, 2032 17:38:24.000000000 IST
                Random Bytes: 2add1037c4908e45e39642358070f88f480b35e16b0be5da...
            Session ID Length: 0
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
            Extensions Length: 117
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
447	8.213087440	172.16.2.30	10.109.29.29	TLSv1.2	1514	Server Hello

Frame 447: 1514 bytes on wire (12112 bits), 1514 bytes captured (12112 bits) on interface 0
Ethernet II, Src: Cisco_60:22:bf (c8:9c:1d:60:22:bf), Dst: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61)
Internet Protocol Version 4, Src: 172.16.2.30, Dst: 10.109.29.29
Transmission Control Protocol, Src Port: 8080, Dst Port: 41640, Seq: 96, Ack: 419, Len: 1460
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Server Hello
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 74
        Handshake Protocol: Server Hello
            Handshake Type: Server Hello (2)
            Length: 70
            Version: TLS 1.2 (0x0303)
            Random
                GMT Unix Time: Sep 22, 1987 10:13:03.000000000 IST
                Random Bytes: 806e85fdd143c42de4be8d3908f784b9c97a95d28c434fbd...
            Session ID Length: 0
            Cipher Suite: TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (0xc02f)
            Compression Method: null (0)
            Extensions Length: 30
            Extension: renegotiation_info
            Extension: ec_point_formats
            Extension: SessionTicket TLS
            Extension: status_request
            Extension: Application Layer Protocol Negotiation
```

```
448	8.213206002	172.16.2.30	10.109.29.29	TLSv1.2	1514	Certificate[TCP segment of a reassembled PDU]

Frame 448: 1514 bytes on wire (12112 bits), 1514 bytes captured (12112 bits) on interface 0
Ethernet II, Src: Cisco_60:22:bf (c8:9c:1d:60:22:bf), Dst: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61)
Internet Protocol Version 4, Src: 172.16.2.30, Dst: 10.109.29.29
Transmission Control Protocol, Src Port: 8080, Dst Port: 41640, Seq: 1556, Ack: 419, Len: 1460
[2 Reassembled TCP Segments (2522 bytes): #447(1381), #448(1141)]
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Certificate
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 2517
        Handshake Protocol: Certificate
            Handshake Type: Certificate (11)
            Length: 2513
            Certificates Length: 2510
            Certificates (2510 bytes)
                Certificate Length: 1328
                Certificate: 3082052c30820414a0030201020210086c3b43e317c35eb7... (id-at-commonName=*.duckduckgo.com,id-at-organizationName=Duck Duck Go, Inc.,id-at-localityName=Paoli,id-at-stateOrProvinceName=Pennsylvania,id-at-countryName=US)
                Certificate Length: 1176
                Certificate: 308204943082037ca003020102021001fda3eb6eca75c888... (id-at-commonName=DigiCert SHA2 Secure Server CA,id-at-organizationName=DigiCert Inc,id-at-countryName=US)
```

```
450	8.213226658	172.16.2.30	10.109.29.29	TLSv1.2	566	Certificate Status, Server Key Exchange, Server Hello Done

Frame 450: 566 bytes on wire (4528 bits), 566 bytes captured (4528 bits) on interface 0
Ethernet II, Src: Cisco_60:22:bf (c8:9c:1d:60:22:bf), Dst: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61)
Internet Protocol Version 4, Src: 172.16.2.30, Dst: 10.109.29.29
Transmission Control Protocol, Src Port: 8080, Dst Port: 41640, Seq: 3016, Ack: 419, Len: 512
[2 Reassembled TCP Segments (484 bytes): #448(319), #450(165)]
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Certificate Status
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 479
        Handshake Protocol: Certificate Status
            Handshake Type: Certificate Status (22)
            Length: 475
            Certificate Status Type: OCSP (1)
            Certificate Status
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Server Key Exchange
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 333
        Handshake Protocol: Server Key Exchange
            Handshake Type: Server Key Exchange (12)
            Length: 329
            EC Diffie-Hellman Server Params
                Curve Type: named_curve (0x03)
                Named Curve: secp256r1 (0x0017)
                Pubkey Length: 65
                Pubkey: 04d8273e23ecb5a95bea8ea8c1462574b637f28b58f06db5...
                Signature Hash Algorithm: 0x0601
                    Signature Hash Algorithm Hash: SHA512 (6)
                    Signature Hash Algorithm Signature: RSA (1)
                Signature Length: 256
                Signature: 5307039e8fd75c523d744b3b186fe777851110b4332ecbf0...
    TLSv1.2 Record Layer: Handshake Protocol: Server Hello Done
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 4
        Handshake Protocol: Server Hello Done
            Handshake Type: Server Hello Done (14)
            Length: 0
```


```
451	8.217641126	10.109.29.29	172.16.2.30	TLSv1.2	180	Client Key Exchange, Change Cipher Spec, Hello Request, Hello Request

Frame 451: 180 bytes on wire (1440 bits), 180 bytes captured (1440 bits) on interface 0
Ethernet II, Src: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61), Dst: Cisco_60:22:bf (c8:9c:1d:60:22:bf)
Internet Protocol Version 4, Src: 10.109.29.29, Dst: 172.16.2.30
Transmission Control Protocol, Src Port: 41640, Dst Port: 8080, Seq: 419, Ack: 3528, Len: 126
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Client Key Exchange
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 70
        Handshake Protocol: Client Key Exchange
            Handshake Type: Client Key Exchange (16)
            Length: 66
            EC Diffie-Hellman Client Params
                Pubkey Length: 65
                Pubkey: 041b38df5082e2d51058757bab3a5ca7c093d7635ec0c1c9...
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


```
489	8.376575327	172.16.2.30	10.109.29.29	TLSv1.2	381	New Session Ticket, Change Cipher Spec, Encrypted Handshake Message, Application Data

Frame 489: 381 bytes on wire (3048 bits), 381 bytes captured (3048 bits) on interface 0
Ethernet II, Src: Cisco_60:22:bf (c8:9c:1d:60:22:bf), Dst: Dell_9f:ae:61 (ec:f4:bb:9f:ae:61)
Internet Protocol Version 4, Src: 172.16.2.30, Dst: 10.109.29.29
Transmission Control Protocol, Src Port: 8080, Dst Port: 41640, Seq: 3528, Ack: 953, Len: 327
Hypertext Transfer Protocol
    [Proxy-Connect-Hostname: icons.duckduckgo.com]
    [Proxy-Connect-Port: 443]
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: New Session Ticket
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 202
        Handshake Protocol: New Session Ticket
            Handshake Type: New Session Ticket (4)
            Length: 198
            TLS Session Ticket
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
    TLSv1.2 Record Layer: Application Data Protocol: http2
        Content Type: Application Data (23)
        Version: TLS 1.2 (0x0303)
        Length: 64
        Encrypted Application Data: 45fc752efa554003199d0c49925f4a0502099a9ea9eb7488...
```
