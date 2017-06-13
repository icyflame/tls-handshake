# Understanding TLS

### Client Hello

```c
struct {
  ProtocolVersion client_version;
  Random random;
  SessionID session_id;
  CipherSuite cipher_suites<2..2^16-2>;
  CompressionMethod compression_methods<1..2^8-1>;
  select (extensions_present) {
    case false:
      struct {};
    case true:
      Extension extensions<0..2^16-1>;
  };
} ClientHello;
```

- **Sent:** Client -> server 
- **Purpose:** To initiate / resume a secure connection
- **client_version** is the highest TLS version that the client supports
- **Session ID** might be empty or an old session ID or a currently active session
    ID.
    - **Old Session ID:** Server will try to resume that connection. Client must
        be ready to negotiate the complete handshake nonetheless.
    - **Currently active session:** Client is trying to open multiple
        connections with the same security parameters.
    - **Empty:** Client wants to open a new connection

- **Cipher Suite** decides the Key Exchange algorithm, bulk encryption algorithm
    alongwith secret key bit size, a Message Authentication Code (MAC)
    algorithm, and a Pseudo Random Function (PRF)
