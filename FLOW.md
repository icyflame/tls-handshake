# Flow

This is a flow of the handshake, and an abbreviated list of the things that are
sent alongwith each of the messages.

### 1. Client Hello

  > Required

  ```
  { 
    ProtVer, 
    { time, random_bytes[28] }, 
    session_id?, 
    cipher_suites[], 
    compression_methods[], 
    extensions
  }
  ```

### 2. Server Hello: 

  > Required

  ```
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

  > if this connection is NOT anonymous, i.e. NOT `DH_anon`

  ```
  {
    List of X.509v3 certificates in ASN.1 that represent a trust chain
  }
  ```

  The first certificate in the list must be the destination server's. It should
  contain the following information, based on the type of key exchange:

  * RSA                      : `{ RSA_pub_key }`
  * Diffie-Hellman           : `{ g, p, Ys}` where `Ys = g ^ x (mod p)`
  * Diffie-Hellman Ephemeral : Nothing specific

### 4. Server Key Exchange

> if this connection is going to be negotiated through DHE or DH_anon
> i.e this connection is DHE_RSA, DHE_DSS or DH_anon

```
{
  { g, p, Ys },
  DH params signed with client_random[32], server_random[32] -> if not DH_anon
}
```

### 5. Certificate Request

> Dropped in this explanation

### 6. Server Hello Done

> After SKE or CR, SHD indicates that server is now done and is waiting for a
> response from the client

```
{ }
```

### 7. Client Certificate

> Dropped in this explanation

### 8. Client Key Exchange

> client sends params to the server to compute a common pre-master secret, and
> subsequently, a common master secret

Depending on whether the server certificate was RSA or DH, there are two paths
here:

* RSA

    ```
    {
      Random 48-byte string, public-key encrypted pre-master secret
      (encrypted with the RSA pubkey sent by the server in SC)
    }
    ```

* DH

    ```
    {
      enum { implicit, explicit } PublicValueEncoding,
      if explicit, { Yc }
      if implicit, { }
    }
    ```

    `Yc` is the client component in the DH key exchange.

    `Yc` is known implicitly if the client sent a `ClientCertificate` message,
    and that certificate was a `fixed_dh` certificate

### 9. Certificate Verify

> Dropped in this explanation

***

**Notes:** After CKE has been transmitted, both the client and the server have
the pre-master secret. Using this pre-master secret, both parties can now
compute the `master_secret` which will be used for bulk encryption.

After this computation is complete, each party must send a `ChangeCipherSpec`
and a `Finished` message to the other party (i.e Client -> Server and Server ->
Client) The order of this is not defined in the spec.

***

### 10. Change Cipher Spec

> This message lets the recipient know that the master_secret has been
> calculated by the sender and they are now switching over to the bulk encryption.

```
{ 1 }
```

**Note:** This is not a handshake message and shouldn't be treated as such when
calculating the hash in the `Finished` message

### 11. Finished

> This is a handshake finalization message and is encrypted with the just
> negotiated `master_secret`. 

Once a party has recieved the other party's `Finished` message, validated it and
sent it's own `Finished` message, it might start sending application data
encrypted using the just negotiated the `master_secret`.

```
{ 
  PRF(master_secret, finished_label, Hash(handshake_msgs))[0...verify_data_len]
}
```

`verify_data_len` is 12 octets by default, but might change on the basis of the
negotiated the cipher suite.
