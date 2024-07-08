**Title:** IPSec
**Tags:** [[cybersecAnalyst]]
**Topics:** #IPSec 

---
# IPSec (Internet Protocol Security)
IPSec (Internet Protocol Security) is a framework that helps us to protect IP traffic on the network layer.

- **Confidentiality:** Encrypt our data. Nobody except the sender and receiver will be able to read our data.
- **Integrity:** Make sure that nobody changes the data in our packets. By calculating a hash value, the sender and receiver will be able to check if changes have been made to the packet.
- **Authentication:** The sender and receiver will authenticate each other to make sure that we are really talking with the device we intend to.
- **Anti-replay:** Even if a packet is encrypted and authenticated, an attacker could try to capture these packets and send them again. By using sequence numbers, IPsec will not transmit any duplicate packets.

Use cases:
- Between two routers to create a site-to-site VPN that “bridges” two LANs together.
- Between a firewall and windows host for remote access VPN.
- Between two Linux servers to protect an insecure protocol like telnet.

## IKE (Internet Key Exchange)
### IKE phase 1
Two peers negotiate about the encryption, authentication, hashing and other protocols that they want to use and some other parameters that are required.
ISAKMP (Internet Security Association and Key Management Protocol) session is established.
The tunnels is used for management traffic. This tunnel is used as a secure method to establish the second tunnel called the IKE phase 2 tunnel or IPsec tunnel.

[AKA]: IKE phase 1 tunnel.
[//]: Collection of parameters is called SA (Security Association).

![[Assets/Pasted image 20220617083119.png]]

### IKE phase 2
Protect user's data that will be sent thought that second tunnel. Here is only one mode to build the IKE phase 2 tunnel, which is called quick mode.
Negotiate about:
- **IPSec Protocol:** AH or ESP.
- **Encapsulation Mode:** Transport or Tunnel mode.
- **Encryption:** DES, 3DES or AES.
- **Authentication:** MD5 or SHA
- **Lifetime:** How long tunnel will be valid. Refresh keying material?
- **(Optional) DH exchange:** used for PFS (Perfect Forward Secrecy)
![[Assets/Pasted image 20220617083601.png]]

```ad-important
IKE builds the tunnels for us but it doesn’t authenticate or encrypt user data.
```

## IPSec Protocols
### AH (Authentication Header) 
AH offers authentication and integrity, but it doesn’t offer any encryption. It protects the IP packet by calculating a hash value over almost all fields in the IP header. The fields it excludes are the ones that can be changed in transit (TTL and header checksum).
```ad-warning
AH is obsolete because it does not provide confidentiality and has problems with NAT/PAT.
```

![[Assets/Pasted image 20220617084023.png]]
![[Assets/Pasted image 20220617084002.png]]

### ESP (Encapsulating Security Payload)
Provides data confidentiality (encryption) and authentication (data integrity, data origin authentication, and replay protection). ESP can be used with confidentiality only, authentication only, or both confidentiality and authentication.
![[Assets/Pasted image 20220617084729.png]]
![[Assets/Pasted image 20220617084736.png]]