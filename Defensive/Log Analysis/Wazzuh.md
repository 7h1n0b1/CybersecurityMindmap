#Defensive #LogAnalysis #Tools #IDS 

# **HOST INTRUSION DETECTION SYSTEM WITH WAZUH**

## **INTRODUCTION**

### What is an intrusion detection system?

Intrusion detection systems are a set of devices or pieces of software that play a huge role in modern organizations to defend against intrusions and malicious activities. We have two major intrusion detection system categories:

`Host Based Intrusion Detection Systems (HIDS):` they run on the enterprise hosts to detect host attacks

`Network Based Intrusion Detection Systems (NIDS)`: their role is to detect network anomalies by monitoring the inbound and outbound traffic.

## **WHAT IS HIDS (HOST INTRUSION DETECTION SYSTEM)**

A HIDs monitors the computer infrastructure on which it is installed, analyzing the traffic and logging malicious behavior. The HIDs will give you visibility of what is happening on your critical security systems. HIDs helps you be able to detect any malicious activities, anomalies and be able to respond to them accordingly.

### HIDs Detection Methods

**Signatures Based Detection:**

Signature-based detection compares files against a database of signatures that are known to be malicious.

**Anomaly Based Detection:**

This method is used to detect abnormal behavior by comparing it against a model of normal behavior; they have higher false positive rates, but are capable of detecting brand-new attacks. Anomaly-based methods have been applied both to sequences of system calls and to other kinds of intrusion detection.

Now that we already understand what IDS and HIDs are, let's go ahead and learn the different features of wazuh that we will be using in our analysis.

## **WAZUH FEATURES EXPLAINED**

Wazuh is a free, open source and enterprise-ready security monitoring solution for threat detection, integrity monitoring, incident response and compliance. The Wazuh platform provides XDR and SIEM features to protect your cloud, container, and server workloads. These include log data analysis, intrusion and malware detection, file integrity monitoring, configuration assessment, vulnerability detection, and support for regulatory compliance.

Wazuh has the following main components:

- Wazuh server.
    
- Wazuh Indexer
    
- Wazuh Dashboard
    
- Wazuh agent.
    

**Wazuh Server**

This component analyzes data received from the agents. It processes it through decoders and rules, using threat intelligence to look for well-known indicators of compromise (IOCs). A single server can analyze data from hundreds or thousands of agents, and scale horizontally when set up as a cluster. This central component is also used to manage the agents, configuring and upgrading them remotely when necessary.

**Wazuh Indexer**

This component is a highly scalable, full-text search and analytics engine. This central component indexes and stores alerts generated by the Wazuh server.

**Wazuh Dashboard**

This component is the web user interface for data visualization and analysis. It includes out-of-the-box dashboards for security events, regulatory compliance (e.g., PCI DSS, GDPR, CIS, HIPAA, NIST 800-53), detected vulnerable applications, file integrity monitoring data, configuration assessment results, cloud infrastructure monitoring events, and others. It is also used to manage Wazuh configuration and to monitor its status.

**Wazuh Agent**:

Agents are installed on endpoints such as laptops, desktops, servers, cloud instances, or virtual machines. They provide threat prevention, detection, and response capabilities. They run on operating systems such as Linux, Windows, macOS, Solaris, AIX, and HP-UX.

In addition to agent-based monitoring capabilities, the Wazuh platform can monitor agent-less devices such as firewalls, switches, routers, or network IDS, among others. For example, a system log data can be collected via Syslog, and its configuration can be monitored through periodic probing of its data, via SSH or through an API.

Now that we understand what Wazuh is and the various components of Wazuh, we will go ahead and look at the features of a Wazuh manager and how it can be used for intrusion detection.

> Under servers, we have a Wazuh server that has a web service, go ahead and power it on to be able to access the Wazuh manager that has already been installed for you in this scenario

Once you load Wazuh, the first page you see is as shown below:

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/9b1d7d25_LP.jpg)

### Agents Panel

On the top panel, we see the following features:

**Total Agents:**

This is a sum of all the agents that have been configured to send logs to our Wazuh manager

**Active Agents:**

This is a total of all the Wazuh agents that have been configured to send logs to the Wazuh manager, and they are sending them as they should.

**Disconnected Agents:**

This shows the total number of agents that were connected to the Wazuh manager but for some reason went offline.

**Never Connected Agents:**

This shows the total of all the agents that were installed on different hosts but for some reasons they have never connected to the Wazuh manager. This could be due to some configuration errors or some firewall rules that are blocking the agent from connecting to the manager.

### Wazuh Modules Panel

Under Wazuh agent modules we have four modules as shown in the figure above.

- Security Information Management
    
- Auditing And Policy Monitoring
    
- Threat Detection and Response
    
- Regulatory Compliance
    

For this tutorial, we are going to focus on the Security Information Management module.

Under this module, we are able to see that we have 2 modules that are security events and integrity monitoring.

**Security Events**:

This module helps you browse through security alerts, identifying issues and threats in your environment.

**Integrity monitoring**:

This module contains alerts related to file integrity management. changes, including permissions, content, ownership and finally attributes.

We are going to be able to see how logs are displayed on the two modules later in this tutorial.

For now, let us access one of our active agents.

To do so, just click on the active agents, this should take you to the page with the list of all the active agents as shown in the figure below.

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/29389a23_www.png)

In our case, we only have one active agent as shown above with the name **workstation**.

If you want to see all the agents, that is all the active disconnected and never connected agents, then click on the total agents.

After you have identified the agent you want to analyze, click on it and that should take you to a similar page as shown below:

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/0d4d3842_LP1.png)

Click on the **Security Events** to see all the events, and on **Integrity monitoring** to see any file modifications.

Moving to the security events module, you should be able to see Dashboard and Events;

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/5f188dc1_das.png)

Under **Dashboard**, you are given a graphical representation of all the events that have been shipped to the Wazuh manager. This is mainly for management.

Under events, which is the module mainly used by analysts for log analysis, is where you find detailed information of particular events/logs.

Let us open the event module and understand how we go about the analysis process.

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/bf1a52e2_MicrosoftTeams-image19.png)

The labeled fields are some of the important fields used when carrying out your log analysis:

**Search**:

This is where you search for words or strings, you can use. For instance, when you want to search for a certain Source IP from the logs you use the following Syntax

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/28254f02_src.png)

**Time**:

This is where you customize your time to the time range in which you want to carry out your log analysis.

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/197b4aac_Wazzzz.png)

You can use the following already defined time ranges, or you can choose to customize your time further by defining the start and end time you want to use.

**Index**:

This will show you the different indices that have been configured. Different index collect different data.

**Filters**:

These are used to narrow down your search e.g. to a certain agent name or agent IP, making your results more accurate.

**Logs**:

This part here shows you a graphical representation of how logs were received and a detailed report of the logs.

Each log can be expanded to get more information regarding a certain log. This is done by clicking the ">" symbol at the beginning of each log.

The figure below shows some sample output of what can be seen when we expand a certain log:

![](https://cdn.cyberranges.com/public/user/628f1f83574e500007cda0b2/0397825c_savw.png)

The same filters are available when you open the integrity monitoring module.

Now that we have a basic understanding of how to use the different features of wazuh, in our next scenario, we will dive deeper into how we use wazuh as a HIDs.