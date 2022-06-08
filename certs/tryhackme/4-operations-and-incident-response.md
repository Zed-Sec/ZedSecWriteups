# 4 - Operations and Incident Response

## 4 - Operations and Incident Response

### Reconnaissance and Discovery

#### Tracert

* Shows the route a packet changes by showing each hop the packet takes.

#### ipconfig and ifconfig

* Used to show the IP configuration on your machine.

#### Netstat

* Gives network statistics.

#### ARP

* Resolved a MAC address to an IP address.

#### CURL

* Get data using a URL

#### hping

* Ping that can send different types of packets.

#### nmap

* Network scanner that can perform a port scan and discover services running on those ports or OS.

#### theHarvester

* Gathers OSINT data.

#### sn1per

* Combines many recon tools into one framework:
  * dnsenum
  * metasploit
  * nmap
  * theHarvester

#### Cuckoo

* Malware sandbox.

### File Manipulation

* There are several tools for manipulation files:
  * cat - read a file.
  * head - view the first part of a file.
  * tail - view the last part of a file.
  * grep - finds text in a file.
  * chmod - changes file permissions.
  * logger - adds entries to the system logs.

### Forensic tools

* Tools that can be used in computer forensics.

#### dd

* Creates a bit by bit copy of a drive.

#### memdump

* Copy information from the system memory.

#### WinHex

* Windows based Hexadecimal editor.

#### FTK imager

* Mounts drives
* Images drives
* Can read encrypted drives if you have the password.

#### Autopsy

* Can view and recover data from storage devices including smart phones.

#### Data Sanitization

* Completely wipes data.

### 4.2 Incident Response

#### Incident Response Process

*   What happens during a security response.

    **Security Incidents**

    IE, a user has clicke a Phishing link.

    **Roles and Responsibilities**

    * Incident response team.
    * IT security management.
    * Compliance officers.
    * Technical staff.
    *   User community.

        **Incident Response Lifecycle**

        * The incident response lifecycle:
          * Preperation
          * Detection and analysis
          * Containment, Eradication and Recovery
          *   Post-incident Activity.

              **Preparation**

              * Planning who should be contacted and how.
              * Incident hardware and software.
              * Incident analysis resource.
              * Incident mitigation software.
              * Policies for an incident.

              **Detection**

              * Detection is tough due to how often these attacks change.

              **Isolation and Containment**

              * It's never a good idea to let an incident run its course.
              * If you want to see what a particular bit of makware does you can always run it in a sandbox.
              * Isolation is tough because some malware can detect this and start deleting files.

              **Recovery**

              * Get things back to normal.
              * Remove the bug.
                * Remove malware
                * Disable breached account
                * Fix vulnerabilities
              * Recover the system from backup

### Attack Frameworks
