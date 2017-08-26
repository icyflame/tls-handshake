# TLS 1.2 Handshake - An explanation

> An effort to understand and explain TLS, at the _right_ level of abstraction

## Sections

* [Target audience](#target)
* [A New Session Negotiation: Explained!](#new-session-negotiation)
  * [How to read this explanation?](#how-to-read-this-explanation)
  * [Flow](#flow)
* [Abbreviations](#abbreviations)
* [References](#references)
* [Appendix](#appendix)
* [License](#license)

## Other pages

* [Packet trace of an actual new session negotiation](./SAMPLE_NEW.md)
* [Packet trace of a session resumption](./SAMPLE_RESUMPTION.md)
* [Looking at each message, in detail _WIP_](./MESSAGES.md)

## Target

My aim was to understand TLS v1.2, at an abstraction level that is above the
bare bones Alice / Bob sketch, and at one that is below the fully detailed IETF
specification, RFC 5246. The article [First few Milliseconds of
HTTPS](http://www.moserware.com/2009/06/first-few-milliseconds-of-https.html)
came close also, but unfortunately dealing with RSA and RC4, it was really
really outdated!

There was one [video](https://www.youtube.com/watch?v=cuR05y_2Gxc) which came
close to the ideal, but I wanted more detail. So, I decided to write my own.

**Who should read this?**

This explanation is specifically aimed at people who have taken a basic course
in cryptography covering the fundamentals of some of the common public-key
cryptosystems that are commonly used today (RSA, DHE, and a little bit of ECC).
More specifically, if you know the mathematics of these, then you are good to
go:

* [RSA: cryptosystem](https://en.wikipedia.org/wiki/RSA_(cryptosystem)#Encryption)
* [Diffie-Hellman Key Exchange](https://en.wikipedia.org/wiki/DH_key_exchange)
* [Digital signature](https://en.wikipedia.org/wiki/Digital_signature)

Thorough, on-your-finger-tips knowledge is not required. If you know enough to
make sense of what the paremeters of each of these are and what the goal of each
is, then you should be able to understand this explanation. (I feel into this
set before I started writing this explanation, if that helps!) If you are
doubtful about whether you know enough, delve into [Flow](#flow) and you will
find out! :)

# New Session Negotiation

## How to read this explanation?

### n. Message Name

> pre-conditions for this message being sent

**Purpose:** An informal purpose of the message

```txt
{
  a structure of how the message would look like in a presentation language
  (with annotations for some variables, if required)
}
```

## Flow

This is a flow of the handshake for a new session negotiation between a client
and a server. The client is generally a modern browser. The server might be
something like Nginx, Apache etc.

Before we begin, let's state the goal of this handshake.

**Goal:** To share a master secret between the client and the server, when the
only communication channel that is available to them is insecure and might have
talented, determined eavesdroppers who would like to implement a MITM attack and
hijack the connection the server and the client have. 

(This master secret will be used to encrypt the traffic that passes between the
client and the server using a symmetric cryptosystem, such as AES.)

### 1. Client Hello

> Required

Client -----> Server

**Purpose:** Hey, I want to make a new connection. This is the TLS version I am
using, a list of cipher suites I support, a list of compression methods I
support and some extensions I would love to have. Let's begin?

**Optional:** Back in the day, we connected with a session ID `session_id`, if
you have those settings cached, then let's continue with that. Saves both of us
some work.  Smile, smile.

```txt
{ 
  ProtVer, 
  { time, random_bytes[28] }, 
  session_id?, /* optional */
  cipher_suites[], 
  compression_methods[], 
  extensions
}
```

### 2. Server Hello: 

> Required

Server -----> Client

**Purpose:** Hey! Sure. I saw your list. Let's continue with this TLS version,
a cipher suite and a compression method from your list that I support. I
generated some random bytes for use later, a session ID that you can use for
resumption in a separate connection, and some extensions.

```txt
{
  ProtVer,
  { time, random_bytes[28] },
  session_id,
  cipher_suite,
  compression_method,
  extensions
}
```

### 3. Server Certificate 

> if this connection is NOT anonymous
>
> i.e. the selected cipher_suite does not start with `DH_anon`

Server -----> Client

**Purpose:** I am attaching a trust chain of certificates that I think you will
be able to verify and trust me with. My certificate might have some parameters
for the key exchange we will perform later.

```txt
{
  List of X.509v3 certificates in ASN.1 that represent a trust chain
}
```

The first certificate in the list must be the destination server's. It should
contain the following information, based on the type of key exchange and
signature algorithms, defined by the `cipher_suite`:

Cryptosystem | Certificate **MUST** contain
:---|:---:
RSA, RSA_PSK, DHE_RSA, ECDHE_RSA | `{ RSA_pub_key }`
DSA | `{ DSA_pub_key }`
Diffie-Hellman | `{ g, p, Ys}` where `Ys = g ^ x (mod p)`
Elliptic Curve Diffie-Hellman | ECDH capable public key, per the TLSECC spec
Diffie-Hellman Ephemeral or EC-DHE | Nothing specific

### 4. Server Key Exchange

> if this connection is going to be negotiated through DHE or DH_anon
>
> i.e this connection is DHE, ECDHE or DH_anon

Server -----> Client

**Purpose:** For the cipher suite that we agreed on, the certificate I sent you
didn't have all the data. So, here are some of the other parameters that you
will need for our key exchange.

```txt
{
  { g, p, Ys },
  DH params signed with client_random[32], server_random[32] -> if not DH_anon
}
```

`client_random` = `ClientHello.random`
`server_random` = `ServerHello.random`

Each `Hello` message's `random` struct contains a 4-byte `gmt_unix_time` and a
28-byte `random_bytes` field.

### 5. Certificate Request

> if the server would like to let only certified clients perform handshakes
>
> Dropped in this explanation

Server -----> Client

**Purpose:** Actually, I only allow clients that hold a valid certificate, so I
need to have a look at your certificate. Please send it over.

### 6. Server Hello Done

> Required

Server -----> Client

**Purpose:** My part of the Hello is done, I will wait for your response.

```txt
{ }
```

### 7. Client Certificate

> If the server requested a certificate and the client intends to comply
>
> Dropped in this explanation

Client -----> Server

**Purpose:** I see that you asked for my certificate. Here it is.

### 8. Client Key Exchange

> Required. Although, this message might be empty if the `cipher_suite` and
> Client certificate implicitly provide the DH parameters to the server

Client -----> Server

**Purpose:** Here are the parameters you need from me for a succesful key
exchange.

Depending on whether the server certificate was RSA or DH, there are two paths
here:

* RSA

    ```txt
    {
      Random 48-byte string, public-key encrypted pre-master secret
      (encrypted with the RSA pubkey sent by the server in SC)
    }
    ```

    The server holds the private key for it's certificate, and hence should be
    able to decrypt this message and find it's 48 byte pre-master-secret.

* DH, DHE, ECDH, ECDHE

    ```txt
    {
      enum { implicit, explicit } PublicValueEncoding,
      if explicit, { Yc }
      if implicit, { }
    }
    ```

    `Yc` is the client component in the DH key exchange.

    `Yc` is known implicitly if the client sent a `ClientCertificate` message,
    and that certificate was a `fixed_dh` certificate

    Using `Yc` and `Ys`, both client and server can now compute the value of the
    pre-master-secret.

### 9. Certificate Verify

> Dropped in this explanation

Client -----> Server

**Purpose:** I sent you my certificate before, this message will help you
explicitly verify that certificate. I hope you trust me now!

***

**Notes:** After CKE has been transmitted, both the client and the server have
the pre-master secret. Using this pre-master secret, both parties can now
[compute the `master_secret`](https://tools.ietf.org/html/rfc5246#section-8.1)
which will be used for bulk encryption.

After this computation is complete, each party must send a `ChangeCipherSpec`
and a `Finished` message to the other party (i.e Client -> Server and Server ->
Client). The client might send the CCS and Finished messages in the same frame
as the CKE.

***

### 10. Change Cipher Spec

> Required. Sent when the master secret has been calculated.

Client -----> Server

Server -----> Client

**Purpose:** I have calculated the master secret, the next message I send you
will be encrypted with that master secret. See you on the other side!

```txt
{ 1 }
```

This message indicates a "bridge" where the sender is moving from public-key
encryption to a symmetric bulk-encryption algorithm.

**Note:** This is not a handshake message and shouldn't be treated as such when
calculating the hash in the `Finished` message

### 11. Finished

> Required. Sent _after_ the CCS message.

Client -----> Server

Server -----> Client

**Purpose:** This message is encrypted with the new `master_secret` that we just
negotiated. If you can decrypt, verify and validate it, we can hand the baton
over to the application layer!

```txt
{ 
  PRF(master_secret, finished_label, Hash(handshake_msgs))[0...verify_data_len]
}
```

This handshake message is the first message that is encrypted with the just
negotiated `master_secret` and signals that the handshake has been completed
successfully by the sending party.

`verify_data_len` is 12 octets by default, but might change on the basis of the
negotiated the cipher suite.

Once a party has recieved the other party's `Finished` message, validated it and
sent it's own `Finished` message, it might start sending application data
encrypted using the just negotiated `master_secret`.

### 12. Bulk Encryption at the Application Layer begins

***

## Abbreviations

Abbreviation | Full-form
:---|:---
CH | Client Hello
SH | Server Hello
SC | Server Certificate
SKE | Server Key Exchange
CR | Certificate Request
SHD | Server Hello Done
CC | Client Certificate
CKE | Client Key Exchange
CV | Certificate Verify
CCS | Change Cipher Spec
DH | Diffie-Hellman Key Exchange
ECDH | Elliptic Curve Diffie-Hellman Key Exchange
DH_anon | Anonymous Diffie-Hellman (messages aren't authenticated)
DHE | Ephemeral DH
ECDHE | Ephemeral ECDH
RSA | Rivest, Shamir, Adleman public key cryptosystem

## References

* [IETF RFC 5246: TLS v1.2](https://tools.ietf.org/html/rfc5246)
* [First few milliseconds of HTTPS](http://www.moserware.com/2009/06/first-few-milliseconds-of-https.html)
* [TLS Handshake Protocol](https://www.cs.fsu.edu/~yasinsac/group/work/childs/TLS.html)

## Appendix

**Notice something that can be improved?** Please [open a pull
request!](https://github.com/icyflame/understanding-tls/pulls)

**Mistakes?** Please [open an
issue](https://github.com/icyflame/understanding-tls/issues/new) on the issues
dashboard right away!

## License

Licensed under MIT.

Copyright (C) 2017  Siddharth Kannan <kannan.siddharth12@gmail.com>
