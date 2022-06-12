# 1 - Threats, Attacks and Vulnerabiliites

## 1 - Threats, Attacks and Vulnerabiliites

https://www.certblaster.com/wp-content/uploads/2020/11/CompTIA-Security-SY0-601-Exam-Objectives-1.0.pdf

### 1.1 Compare and contrast different types of social engineering techniques

#### Phishing

*   Phishing is when an attacker sends an email impersonating someone to try and trick somebody into doing something.

    Phishing emails will often:

    * Often try to get a user to click a link to a credential harvesting site.
    * Check where URLs are actually leading.
    * Copy the branding of a legitimate brand
    * Use typosquating
    * Use urgency to get wwhat they want

    **Pharming**

    * Pharming is to harvest credentials from multiple people.

    **Vishing**

    * Phishing over the telephone.

    **Smishing**

    * Phishing over SMS text message

#### Impersonation

*   Impersonation is when an attacker pretents to be somebody else.

    These often include:

    * An actor
    * A story
    * Technical jargon to confuse you

#### Dumpster Diving

*   Looking through the bins to find sensitive information that hasn't been disposed of properly.

    To stop dumpster diving:

    * Shred your documents.
    * Lock bins up.

#### Shoulder Surfing

*   Looking over somebodies shoulder to see them type in their password.

    This can be used to:

    * Get passwords.
    * Read sensitive documents that you're also reading.

#### Hoaxes

* A threat which isn't real. Like tricking a user into sending them gift cards or claiming that they've won a competition.

#### Watering Hole Attack

* Breaching a third part which users will visit. This third party becomes a **watering hole**.

#### Spam

* Unsolicited and unwanted messages.
  *   Phishing can be a type of spam.

      You can prevent spam by using a spam filter on your mail gateway and configuring some of the following:

      * Allowed list - Only allow emails from specific senders through.
      * SMTP Standards Checking - Block messages that don't follow RFC standards.
      * rDNS - Block email where the sender's domain doesn't match the IP address.
      * Tarpiting - Throttle mail transfers which slows down how quickly emails can be sent to users.
      * Recipient Filtering - Blcok all emails not addressed to a valid email address in the organisation.

#### Influence Campaign

*   Trying to sway public opinion

    This can be achieved via:

    * Fake social media users creating content related to a specific message.

#### Tailgating

* When somebody follows an authorized user into a building, piggybacking off their access.

#### Invoice Scams

* Sending a fabricated bill to the finance department to get them to hand over money.

#### Credential Harvesting

*   Collecting passwords from users.

    This can be done via:

    * Phishing
    * Collecting them from cached credentials on the users local machine.

### 1.2 Given a scenario, analyze potential indicators to determine the type of attack

#### Malware

*   Malware is malicious software, software designed to do something bad.

    **Viruses**

    * A virus is a type of malware that can reproduce itself.
    * Needs user interaction to run.
    *   Can cause issues or sit undetected, collecting information

        **Virus Types**

        * Program Virus - part of a program.
        * Boot sector virus - embeds itself within the boot sector of a hard drive.
        * Script Virus - runs as a script.
        * Macro - runs inside another application
        * Fileless - Doesn't save itself as a file on your system. Operates in memory.

    **Worms**

    * Doesn't need user interaction.
    * Self-replicates.
    * Can be mitigated with IDS/IPS if you know the signature of the worm.

    **Ransomware**

    * Displays a ransom message until a specific sum is paid.

    **Crypto-Malware**

    * Newer version of Ransomware, encrypts computer contents until a ransom is paid.
    * The decryption key will be sent to you once the ransom has been paid.
    * To mitigate this take a regular backup that isn't connected to your system.

    **Trojan Horse**

    * When a piece of malware is hiding within a normal file.
    * Trojans often download PUP (Potentially Unwanted Software).

    **RAT**

    * A Remote Access Trojan (RAT) is a tool which can be accessed remotely by an attacker.
    * Can log keystrokes, record screens and download files.

    **Rootkit**

    * Modifies the kernel isntead of the files.
    * Invisible to anti-virus software.
    * Can be mitigated by using a machine with Secure Boot enabled.

    **Adware**

    * Causes ads to pop up on your machine.

    **Spyware**

    * Spies on you, captures keystrokes, credentials and other sensitive information.

    **Bots**

    * An infected computer that is remotely controlled by a C\&C (Command & Control Center).

    **Logic Bomb**

    * An attack that triggers on a pre-defined event.

#### Password Attacks

*   An attack that targets passwords.

    **Spraying Attack**

    * When an attacker tries a few common passwords before moving onto trying to break into a different account.

    **Brute Force**

    * Trying every combination of usernames and passwords until it finds the correct credentials.

    **Dictionary Attack**

    * Use a list of common words to make bruteforcing easier.

    **Rainbow Table**

    * A set of pre-built hashes. Since hashes aren't reversible it can be useful to have a Rainbow Table to make hashes easier to look up.

    **Salt**

    * Adds an extra piece of data to the password when hashing. This allows users with the same passwords to have different hashes. This helps slow down a brute-force and a rainbow table attack.

#### Physical Attacks

* Attacks with a physical element.

**Malicious USB Cable**

* A cable that looks like a normal USB that downloads malicious software when inserted.

**Malicious Flash Drive**

* Deploys malware when plugged into a machine.

**Skimming**

* Copying the information on a card when you use it in a card machine.

#### Adversal Artificial Intelligence

* Using false information to confuse machine learning.

#### Supply Chain Attacks

* A supply chain attack is an attack on a large operation.

#### Cloud Based Attacks

* Attacks on data and infrastructure in the cloud.

#### Cryptographic Attacks

* Attacking encrypted data.

**Birthday Attack**

* A hash collision is when two plaintext strings have the same hash.

**Downgrade Attack**

Forcing a system to downgrade to a weak version of encryption that's been cracked. Then a conversation can be cracked.

### 1.3 Given a scenario, analyze potential indicators associated with application attacks

#### Privilege Escalation

* Using a logic flaw or bug to gain higher access.

#### Cross-site Scripting (XSS)

* Uses browser flaws to run scripts on a user device.
* Requires user input often.

#### Injection Attacks

* Adding your own code to an input, often via an input field.

**SQL Injection**

* Uses SQL query language to get information directly from the backend database.

#### Buffer-overflow

* Overwiting a buiffer of memory to spill into other exploit areas.

#### Replay Attack

* Capturing network data then replay credentials or information then using it to impersonate.

#### Request Forgeries

* A cross site request is loading inforamtion from another request. Like an embeded YouTube video on a site that isn't YouTube.
* A cross-site request forgery si when an application takes advantage of the trust a website has for you.

#### Driver Manipulation

* Antivirus usually blocks malware based on known malware signatures which can then be blocked.
* A driver runs the software on your machine and tells it what to do.

#### SSL Stripping

* Stripping away SSL while data is in transit between two hosts. The SSL on the HTTPs encryption is stripped away so it's just HTTP.

#### Race Conditions

* A race conditions is when things happen at the same time when not planned for.

### 1.4 Given a scenario, analyze potential indicators associated with network attacks

#### Wireless

*   Network attacks associated with wireless.

    **Rogue Access Points**

    * An unauthorized wireless access point.
    *   Added to the network without authorization.

        **Wireless Evil Twin**

        * A rogue access point isn't always malicious. But a wireless evil twin is an AP that looks legitimate but is actually malicious.

    **Bluejacking**

    * An unsolicicited message sent via Bluetooth.
    * Bluetooth is short range (around 10m).

    **Bluesnarfing**

    * Accessing a Bluetooth-enabled device and transferring data.
    * Can access contacts, calendar, emails, pictures, video, etc.
    * Modern phones aren't vulerable to this.

    **Wireless Dissasociation**

    * When a wireless connection keeps dropping and causes a DoS attack.

    **Wireless Jamming**

    * Prevent wireless communication.

#### Layer 2 attacks

*   Attacks that happen on layer 2.

    **Mac Flooding**

    * The MAC table on a switch only has so much space, so an attacker can fill up a MAC table on a switch then the switch will start flooding all interfaces.

    **MAC Cloning**

    * Spoofing a legitimate device that is already allowed on the network.

#### DNS

*   Attacks manipulating DNS (Domain Name System).

    **DNS Poisoning**

    * Modify the hosts file on a device or modify the information on a DNS server to have a legitimate hostname to resolve to a malicious IP.

    **Domain Hijacking**

    * Get access to the domain registration so the attacker can control the traffic.

    **Domain Reputation**

    * Many sites online track and categories all IPs they come across. This allows malicious IPs to be spotted easily.

#### Denial of Service

* Causing a service to become unavailable.

#### Malicious Scripts

* Scripts which have malicious intent.
* Common scripting languages are:
  * PowerShell
  * Python
  * Bash
  * Macros
  * VBA

### Threat Actors

#### Actors and Threats

*   The person responsible for an event.

    **Advanced Persistent Threat**

    * A threat which is there until you remove it.

    **Insider**

    * A threat from within the organisation.

    **Nation State**

    * A threat actor that a goverment from a country.

    **Hacktivist**

    * Somebody hacking for a goal to make change. After social change or a political message.

    **Script Kiddies**

    * Somebody who is using pre-packed tools and doesn't have a lot of knowledge next.

    **Organized Crime**

    * Professional criminals mostly after financial gain.

    **Hackers**

    * Expert with technology. Can be good or bad.

    **Shadow IT**

    * A person or team within an organization who bypasses the IT department.

    **Competitors**

    * Somebody who is a rival to the company.

#### Attack Vectors

*   The method that the attacker used.

    **Direct Access**

    * Physical access to a machine or system.

    **Wireless**

    * Vectors on wireless technology, these could be:
      * Default login credentials.
      * Rogue access point.
      * Evil twin.
      * Protocol vulnerabilities.

    **Email**

    * Vectors on email:
      * Phishing.
      * Attach malware to a message.
      * Social engineering

    **Supply Chain**

    * Tampering with the underlying infrastructure:
      * Gaina access to netowrk using a vendor.
      * Malware can modify the manufacturing process.
      * Counterfeit networking equipment.

    **Removable Media**

    * Using media which can be removed to get around the firewall:
      * USB drive

    **Cloud**

    * Vectors using publicly facing applications and services:
      * Security misconfigurations.
      * Brute force attacks.
      * Orchestration attacks.

#### Threat Intelligence

*   Researching threats

    **Open-source intelligence (OSINT)**

    * Data which is publicly available.

    **Closed/proprietary intelligence**

    * Somebody has already compiled the intelligence and you can buy it as a service.

    **Vulnerability Databases**

    * A database full of vulnerabilities.

    **Public/private information sharing centers**

    * Sometimes the goverment will releast threat intelligence.
    * Private companies can also provice intelligence.

    **Automated indicator sharing**

    * Automating the sharing of threat information.

    **Dark web intelligence**

    * Intelligence that is sourced from the dark web.

    **IOC (Inidcator of Compromise)**

    * Seeing an event on the network which could indicate an intrusion.

    **Predictive Analysis**

    * Trying to analyse data to see where an attack might happen next.

#### Research sources

* Where to do threat research:
  * Vendor websites
  * Vulnerability feeds
  * Conferences
  * Academic Journals
  * Request for comments
  * Local industry groups
  * Social media
  * Threat feeds

### 1.6 Explain the security concerns associated with various types of vulnerability

#### Vulnerability types

*   The types and characteristics of vulnerabilities.

    **Zero day attack**

    * Attacks that don't have a patch or fix yet.

    **Open Permissions**

    * When no steps have been taken to secure data.

    **Unsecured Root Account**

    * An administrator account on Linux that has no password or a very easy password set.

    **Errors**

    * Sometimes errors give away too much information.

    **Weak encryption**

    * Using encryption which has been cracked already.

    **Insecure Protocols**

    * Some protocols aren't encrypted:
      * Telnet
      * FTP
      * SMTP
      * IMAP

    **Default Settings**

    * Using weak default security settings or default login credentials.

    **Open ports and services**

    * Using ports and services which don't need to be open or running which make a larger attack surface.

    **Patch Management**

    * Not keeping up to date on patch management.

    **Legacy Passwords**

    * Using outdated systems.

### Third Party Risks

*   Risks that come from an outside party.

    **System integration risk**

    * Professionals integrating a system have elevated access often so could perform a malicious action.

    **Lack of vendor support**

    * Not all vendors have good patch management or care for security.

    **Supply chain risk**

    * Youc can't control security at a third party location.

    **Outsourced code development**

    * How is the data accessed?
    * Is the remote development enviroment isolated from the production side of the network?

    **Data storage**

    * Not applying proper controls around what is stored or how it's stored at a third party location.

#### Vulnerability Impacts

* Some impacts of a vulnerability can be:
  * Data loss
  * Data breaches
  * Data exfiltration
  * Identity theft
  * Financial
  * Reputation
  * Availibility loss

### 1.7 Sumamarize the techniques used in security assessments.

#### Threat Hunting

*   Threat hunting is trying to find the threats and the strategies used to do this.

    **Intelligence Fusion**

    * The biggest issue is the amount of data needed to sift through is so massive.
    * Intelligence fusion is puting all the security data together and using big data to make it useful.

#### Vulnerability Scanning

*   Scanning a network for vulnerabilities.

    **Non-intrusive scans**

    * Tries to gather information on a vulnerability but doesn't try to exploit it.

    **Intrusive Scan**

    * Tries the vulnerablity to see if it works.

    **Credential Scans**

    * A non-credentialed scan can't logon to the remote device but if you supply credentials it can emulate an insider attack.

#### Security Information and Event Management (SIEM)

* Collects security events and information then can alert and report on it.

### 1.8 Explain the techniques used in penetration testing.

*   Penetration testing is the act of simulating an attack on a network.

    #### Rules of engagement\*\*

    * A document which defines what the penetration tester is and isn't allowed to do during the test. What is in scope.
