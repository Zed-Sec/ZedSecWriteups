# SOC147 - SSH Scan Activity

### Video Write-Up

{% embed url="https://www.youtube.com/watch?v=dfPdOaW3Ho8" %}

### Written Write-Up

**Initial Notes**

So we've got an incident for SSH Scan Activity. We can see that a machine has done what looks like an nmap scan and we need to confirm whether this is expected activity or not and then close the alert off.

![](<../../.gitbook/assets/image (2) (2).png>)

Start off by taking a note of some of the important details in the ticket:

* Event Time - June 13. 2021. 4:23PM
* Source Address - 172.16.20.5
* Source Hostname - PentestMachine

The first thing that I pick up when I see this is that the scan came from a hostname **PentestMachine** this is interesting because it's possible that this could be regular activity, especially from a Pentesting box, but we still need to confirm this.

**The File**

There's a file attached that we can take a look at. VirusTotal can be used to compare a file against a few popular virus scanning engines to see if they pick up anything malicious within the file. One thing to note with VirusTotal is that anything you submit there will be available to the public so you have to be careful about what you're submitting. You shouldn't submit anything that might contain confidential company data within.

Once we submit the file it's not picking it up as malicious. This doesn't mean that the file is 100% safe, it just means nothing malicious has been detected.

![](<../../.gitbook/assets/image (4).png>)

**Firewall Logs**

There's a logging tab we can access within LetsDefend to look for the traffic we're investigating. Searching for the source IP of the PentestMachine and scrolling down to the date and time of the event we can see 4 IPs were scanned on the date of the event on port 22, which is SSH.

![](<../../.gitbook/assets/image (5).png>)

**PentestMachine**

We can also check the **EndPoint Security** tab to investigate the machine that triggered the alert. Looking at the logs for the machine we can see that it ran an nmap scan on the 172.16.20.0/24 range of IP addresses, scanning for version detection and a ping scan on that port. This is the same range we saw scanned in the firewall logs so we can confirm it's this machine that caused the alert.

**Confirming Expected Activity**

Heading over to the **Mailbox** tab and doing a search for pentest in the search box displays a result for an email from ellie@letsdefend.io mentioning that there will be some planned scanning coming from that box on the date we're investigating. This means that this is expected activity.

**Closing the alert**

Going back to the alert we can select **Actions** and then **Close**, mark the incident as a false positive and add in some closing notes:

![](<../../.gitbook/assets/image (6).png>)

Once you've closed the alert you should be awarded some points for getting the answer correct!



