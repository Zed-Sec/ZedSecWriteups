# 3 - Implementation

## 3 - Implementation

### 3.1 Given a scenario, implement secure protocols

#### Voice and Video

*   Protocols used by voice and video services.

    **SRTP (Secure Real-Time Transport Protocol)**

    * Encrypts the voice/video flow.

#### NTP (Network Time Protocol)

*   Has no security features.

    **NTPsec**

    * A secure version of the protocol.

#### Email

*   Email protocols

    **S/MIME (Secure/Multipurpose Internet Mail Extensions)**

    * Uses public key encryption and digital signing of mail content.
    * Requires a PKI or similar organization of keys.

    **POP3**

    * Can use the STARTTLS extention to encrypt POP3 with SSL.

    **IMAP**

    * Can also be used with SSL.

    **SSL/TLS**

    * If using a browser to send email, should always be using SSL/TLS to encrypt that mail.

#### Web

*   Web protocols

    **SSL/TLS**

    * TLS is the newer version of TLS.

    **HTTPS**

    * HTTP over TLS / HTTP over SSL / HTTP Secure.
    * Uses PKI

#### IPsec (Internet Protocol Security)

* Security for OSI Layer 3.
* Authentication and encryption for every packet.
* Has packet signing for anti-relay.
  * Two core IPsec protocols:
    * Authentication Header (AH).
    * Encapsulation Security Payload (ESP).

#### File Transfer

*   File transfer protocols.

    **FTPS**

    * FTP over SSL
    * File Transfer Protocol Secure.
    * Not SFTP.

    **SFTP**

    * SSH File Transfer Protocol
    * Provides file system functionality

#### LDAP (Lightweigh Directory Access Protocol)

*   Used for reading and writing over an IP network.

    **LDAPS**

    * Unnofficialy securre version of LDAP.
    * Uses SSL.

#### Remote Access

*   Remote access protocol.

    **SSH (Secure Shell)**

    * Encrypted version of Telnet (and FTP).

#### DNS

*   By default DNS didn't have any security features.

    **DNSSEC**

    * Domain Name System Security Extensions.
    * Validates DNS responses.
      * Where the origin came from.
      * Data integrity.

#### Routing and Switching

*   Can be managed using SSH and SNMPv3.

    **SNMPv3**

    * Added encryption and authentication.

#### Network Address Allocation

* DHCP does not include built-in security by default.
*   There is no secure version of DHCP.

    **Rogue DHCP Servers**

    * In AD DHCP must be authorized.

### 3.2 Given a scenario, implement host or application security solutions

#### Endpoint Protection

*   How the users devices are protected.

    **Anti-virus**

    * Refers to software which blocks trojans, worms, macro viruses.

    **Anti-malware**

    * Stopes spyware, ransomware and fileless malware.

    **Endpoint detection and response (EDR)**

    * Uses a different method of detecting a threat other than signatures.
    * Can use behavioral analysis, machine learning, process monitoring.
    * Can often do a root cause analysis.
    * Can respond to a threat.

    **DLP**

    * Blocks sensitive data from leaving the organization.

    **Next-generation firewall (NGFW)**

    * Can detect applications operating over the network instead of just the IP address and port number.

    **Host-based firewall**

    * Local firewall on an endpoint, like Windows Firewall.

    **Finding intrustions**

    *   HIDS and HIPS can be used to find intrustions.

        **Host-based Intrusion Detection System (HIDS)**

        * Uses log files to identify intrusions.
        * Can reconfigure firewalls.

        **Host-based Intrusion Prevention System (HIPS)**

        * Recognize and block known attacks.
        * Secure OS and application config.
        * Often built into endpoint protection software.

#### Boot Integrity

*   Attacks on the boot section of an operating system.

    **Trusted Platform Module (TPM)**

    * A hardware module that has encryption functionality.

    **Secure boot**

    * A UEFI BIOS specification.
    * BIOS prevents unauthorised writes to the flash.
    * Only accepts digitally signed BIOS updates from the manufacturer.

    **Trusted Boot**

    * Bootloader verifies digital signature of the OS kernal to make sure the kernal hasn't been changed.

    **Measured Boot**

    * Makes sure nothing on the computer has been changed.

#### Application Security

*   Some security steps that can be taken for applications.

    **Dynamic Analysis (Fuzzing)**

    * Random data being put into an application. This is the attackers trying to prompt an error or something else which will give them a foothold into a vulnerability.

### 3.4 Wireless Security

#### Cryptographic Protocols.

*   An organizations wireless network can contain confidential information. This information must be encrypted.

    **Only people with the right encryption key can listen to activity on the network**

    * WPA 2 and WPA3.

    **WPA2 (WI-FI Protected Access 2)**

    * Uses CCMP Block Cipher Mode.
    * CCMP uses AES.
    * WPA2 has a PSK (pre-share key) brute-force problem.

    **WPA3**

    * Uses GCMP Block CipherMode.
    * Stronger encryption thatn WPA2
    * Still uses AES.

#### Wireless Authentication Methods

* Methods used when connecting to a wireless network.
* There are usually wo ways to connect to a wireless network:
  * Shared password (pre-shared key).
  *   Centralized authentication (802.1x).

      **Captive portal**

      * Requires guests to login to the WI-FI via a login page in their browser.

#### Wireless Authentication Protocols

*   Types of wireless authentication protocols.

    **Extensible Authentication Protocol (EAP)**

    * An authentication framework.
    * EAP integrates with 802.1X
      * Prevents access to the network until the authentication succeeds.

    **IEEE 802.1X**

    * Port based network access control.
    * You don't get access until the authentication is successful.
    * Used in conjunction with a database access table.
      * RADIUS, LDAP, TACACS+

    **EAP-FAST (Flexible authentication via tunnel)**

    * Authentication server and supplicant share a protected access credentail (PAC) secret.
    * Supplicant receives the PAC.
    * Supplicant and AS mutually authenticate and negotiate a TLS tunnel.

    **PEAP (Protected Extensible Authentication Protocol)**

    * Protected by EAP
    * Encapsulated EAP in a TLS tunnel.
    * User authenticates with MSCHAPv2.

    **EAP TLS**

    * Strong security, wide adoption.
    * Required digital certificates for mutual authentication.
    * TLS tunnel is then built for the authentication process.

#### Installing Wireless Networks

*   Some considerations when installing wireless networks.

    **Site Surveys**

    * Determine current range and signal strenth of WIFI in various locations.
    * Identify existing access points.
    * Work around existing frequencies.
    * Plan for ongoing site surveys.

    **Wireless Survey Tools**

    * Signal coverage.
    * Potential interferance.
    * Spectrum analyzer.
    * Third-party tools.

    **Wireless Packet Analyser**

    * Wireless networks are easy to monitor, you just need a listener device.

    **Access Point Placement**

    * You need minimum overlap with low interference but also maximum coverage.

    **Wireless Infrastructure Security**

    * Wireless controllers can be used to manage access points.

### 3.5 Secure Mobile Solutions

### 3.6 Apply Cybesecurity Solutions to the Cloud

#### HA Zones

* Availability zones (AZ) are locations within a cloud region commonly over multiple regions. So you can set up HA across multiple zones to provide failover.

#### Resource Policies

* Identity and Access Management (IAM).
  * Who gets access.
  * What they get access to.
* Map job function to roles.

#### Secrets Management

* Cloud computing requires many secrets such as:
  * API keys
  * Passwords
  * Certificates
* This can become difficult to manage so there are cloud services available to manage these secrets.

### 3.9 Public Key Infrastructure

#### PKI

*   PKI is the act of managing digital certificates.

    **Key Management**

    * Key generation
      * The keys will have a particular strength and cypher.
    * Certificate generation
      * Allocate the key to a user.
    * Distribution
      * Make the key available to the user.
    * Storage
      * How the keys are stored securely.
    * Revocation
      * Manage keys that have been compromised.
    * Expiration
      * Manage keys that have expired or will be expiring soon.

    **Digital Certificates**

    * A public key certificate
      * Binds a public key with a digital signature.
      * Contains details about the key holder.
    * A digital signature adds trust.
      * PKI uses CA for additional trust.
      * Web of trust adds other users for additional trust.

    **Commercial Certificate Authorities**

    * Your browser maintains a list of trusted CAs.
    * These commercial CAs allow you to purchase a certificate from them so your site can be trusted,
      * Usually with this you generate a keypair then send the public key to the CA to be signed.
        * Sending the public key is referred to as a certificate signing request (CSR).

    **Private Certificate Authorities**

    * If your applications and services are just running internally you can be your own CA.
    * Your device must trust the internal CA.

    **PKI Trust Relationships**

    * In a single CA everybody receives their certificate from one CA.
    * In a larger org a hierarchical CA is used:
      * Single CA issues certs to intermediate CA.
      * Distributes the certificate management load.
      * Easier to deal with revoking the intermediate CA than the root CA.

    **Registration Authority**

    * The entity requesting a certificate needs to be authorised.
    * The RA authenticates and authorises the requester then either approves or rejects.

    **Certificate Attributes**

    * Common Name (CN) - The FQDN for the certificate.
    * Subject alternative name - Additional hostnames for the cert.
    * Expiration - When the cert expires.

#### Certificates

**Web Server SSL Certificates**

* Used to encrypt a website and validate the owner of the website.
  * A wildcard allows multiple hostnames to be associated with the domain, allowing for subdomains to still be encrypted.

**Code Signing Cert**

* Allows you to receive software, install it and know that the software hasn't changed since it was deployed by the manufacturer.

**Root Certificate**

* The public key certificate that identifies the root CA.
  * Everything starts with this certificate.
* The foundation of your PKI.

**Self-signed certs**

* Allows you to sign your own cert for internal devices. These don't need to be signed by a public CA.

**Machine and computer certificates**

* A device connected to the network needs to be able to know whether it is trusted or not.

**Email Certificates**

* Use cryptography in an email platform.

#### Certificate File Formats

*   Different formats that certificates can take.

    **X.509 Digital Certificates**

    * The structure of the cert is standardised.

    **DER (Distinguished Encoding Rules)**

    * Designed to transfer syntax for data structures.

    **PEM (Privacy Enhanced Mail)**

    * A base 64 encoded DER certificate.
    * Generally the format provided by most CAs.
