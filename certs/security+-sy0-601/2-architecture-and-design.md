# 2 - Architecture and Design

## 2 - Architecture and Design

### 2.1 Explain the importance of security concepts in an enterprise enviroment

#### Configuration Management

* Congfigurations in your enviroment will be constantly changing.
*   If you need to restore from a config, your documentation should be thourough enough to get you back to the same place as before.

    **Diagrams**

    * Document the network including physical location of devices and cables.

    **Baseline config**

    * The basic settings an application is running:
      * Firewall settings
      * Patch levels
      * OS file versions
    * You can check your baseline is in compliance by doing an integrity measurement check.

    **Standard naming convention**

    * Giving all devices a specific pattern for different device and server types so devices are easier to identify. This applies to account names too.

    **IP Schema**

    * Standard IP ranges for different uses, such as servers or different offices.

#### Protecting Data

*   How data is secured.

    **Data sovereignty**

    * How data is protected in different countries.

    **Data masking**

    * Obfuscating data which hides some of the data, like on a receipt you can't see the full card number used.

    **Data encryption**

    * Encoding data from plaintext to ciphertext.

    **Diffusion**

    * Change one character of the input, this will completely change the ciphertext produced when encrypted.

    **Data at-rest**

    * Data on a storage device.
    * You can protect this data by applying permissions or encrypting the drive.

    **Data in-transit**

    * Data which is currently moving over the network.
    * It doesn't have much protection as it travels.
    * Can be encrypted to protect it

    **Data in-use**

    * Data that is actively processed in the memory.
    * Since it's in use it's almost always decrypyed.

    **Tokenization**

    * Replace sensitive data with a non-sensitive placeholder.

    **Information rights management**

    * Control how data is used.
    * Prevents unauthorised people from performing various actions.

    **Data Loss Prevention**

    * Preventing sensitive data from leaving the organisation.

#### Geographical Considerations

* Taking into account the fact that data regulations change from country to country.

#### Response and Recovery Controls

* The formal process when responding or recovering from an attack.
* This should be documented:
  * Identify the attack.
  * Contain the attack.
  * Limit the impact of a hacker.

#### SSL/TLS Inspection

* Used to examine outgoing SSL/TLS. Since the data is encrypted we can't see what's in it. So SSL/TLS inspection needs to be configured to help protect data from leaving the organisation.

#### Hashing

* Encoding data to represent a string of text as a random string of text.
* One-way trip

#### API Considerations

* API (Application Programming Interface).
* Secure and harden the login page, including the API.
* Attackers use an on-path attack to modify and replay API conversations.
  *   This then allows them to perform API injection.

      **API Security**

      * Requiring authentication.
      * Authorization - each user has a limited role.
      * WAF (Web Application Firewall) - Apply rules to API communication.

#### Site Resliency

*   The preperations taken for when the worst happens.

    **Hot site**

    * An exact replica, everything is duplicated.
    * It's quick to switch between sites.

    **Cold site**

    * An empty building with nothing in place.
    * No people so personel also need to be moved too.

    **Warm site**

    * Somewhere in the middle of the two.

#### Honeypots and Deception

*   Meant to attract the bad guys to get more information on them.

    **Honeynet**

    * Multiple honeypots.

    **Honeyfiles**

    * The bait within the honeypot, usually a file which looks interesting that will alert you when it's accessed.

    **Fake Telemetry**

    * Machine learning to identify fake data.

    **DNS Sinkhole**

    * A DNS that hands out an incorrect IP address.
    * This can redirect users to a malicious site.

### 1.2 Summarize virtualization and cloud computing concepts

#### Cloud Models

*   There are several different cloud models.

    **Infrastructure as a service (IaaS)**

    * Outsourcing your physical equipement.
    * The provider owns the hardware but you manage the hardware and the security on it.

    **Software as a service (SaaS)**

    * The software is on demand such as a payroll system. You just pay for use of the service and don't have to manage the underlying platform or the infrastrucure.

    **Platform as a service (PaaS)**

    * No servers, no software. Somebody else handles the platform, you just handle the developement on top of that.

    **Anything as a Service (XaaS)**

    * Everything delivered over the cloud, mostly a catch-all term.

    **Public Cloud**

    * Available to everyone on the internet.

    **Community**

    * Several organizations share the same resources.

    **Private**

    * Your own virtualized local data center.

    **Hybrid**

    * A mix of public and private.

#### Edge Computing

* Usually IoT devices. Devices with a very specific function.
* The events that occur on these devices are known as edge computing.

#### Fog Computing

* A cloud that's close to your data.

#### Virtualization

*   Run many operating systems on the same device.

    **VM Sprawl Avoidance**

    * Returning all of the virtual machines to a useable state. VMs should be documented properly and decomissioned when not needed to avoid sprawl.

    **VM Escape Protection**

    * Sometimes some exploits can escape a VM.

#### Containers

* One single operating system running many applications in containers.

#### Infrastructure as Code

* Define servers, network and applications as code in a virtualized instance.

### 2.3 Summarize secure application development, deployment and automation concepts.

#### Secure Coding Techniques

*   Common steps taken when programming to make applications more secure.

    **Stored Procdeures**

    * Creating procedures that can be called to the back-end. This stops attackers being able to see SQL queries to the database.

    **Code Reuse**

    * This can cause security vulnerabilities. If a piece of code is vulnerable and you use it in multiple apps this can spread the vulnerabiility.

### 2.4 Summarize authentication and authorization design concepts.

#### Authentication

*   There are many different types of authentication.

    **Directory Services**

    * Collating all of an organizations usernames and passwords in a single database.
    * Active Directory is an example of this and can be accessed via Kerberos or LDAP.

    **Federation**

    * Allow somebody to connect to your network using credentials that are stored by a third party. Being able to log into other sites with your Twitter account is an example of this.

    **Attestation**

    * Prove that the hardware is really yours.

    **Technologies**

    * Authentication technologies:
      * SMS
      * Authentication apps
      * TOTP (Time-based One Time Password Algorithm)
      * HOTP - One time password
      * Phone call
      * Static codes (like your debit card pin number)

#### Biometrics

*   Something you are, like a fingerprint.

    Types of biometrics are as follows: \* Fignerprint \* Retina (back of the eye) \* Iris (Texture and colour of the eye) \* Facial \* Voice \* Vein \* Gait Analyaia (how you walk)

    **False Acceptance Rates**

    * How often an unauthroised user will be accepted.

    **False Rejection Rate**

    * How often authorised users are rejected.

    **Crossover Error Rate**

    * A happy medium between the two.

#### Multifactor Authentication

*   When you use an additional factor before you can authenticate.

    **Factors**

    * Something you know - like a password
    * Something you have - a smart card
    * Something you are - biometrics

    **Attributes**

    * Somewhere you are - provide a factor based on where you are, like only allowing access if you're in the UK
    * Something you can do - a personal way of doing things such as a signature
    * Something you exhibit - something you exhibit like the way you walk, or the way that you type
    * Someone you know - who you know

### 2.6 Explain the security implications of embedded and specialized systems

### 2.7 Explain the impoortance of physical security controls

### 2.8 Summarise the basics of cryptographic concepts

*   Making information secretive and authenticate users.

    **Plaintext**

    * Data in unencrypted form.

    **Ciphertext**

    * An encrypted message.

    **Cipher**

    * The algrithm used to encrypt and/or decrypt.

    **Cryptanalysis**

    * The art of cracking encryption.

#### Cryptographic Keys

* Add the key to the cypher to encrypt.

#### Key Stretching

* Hashing a password multiple times, this is helpful if you're using a weak key.

#### Symmetric Encryption

* Uses a single key to encrypt and decrypt the data.

**Asmmetric**

* Uses a different key for encrypting and decrypting.
