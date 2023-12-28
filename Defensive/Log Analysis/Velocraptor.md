#Defensive #LogAnalysis #Tools 

# **INTRODUCTION TO VELOCIRAPTOR**

## **WHAT IS VELOCIRAPTOR**

Velociraptor is an Open Source Digital Forensic and Incident Response tool that is used to retrieve (Hunt) for digital data/evidence (Artifacts) from a fleet of endpoints. Velociraptor gives a Cybersecurity Analyst the ability to respond to a wide array of Cybersecurity investigations and data breaches. These include:

- The ability to reconstruct attacker activities through digital forensic analysis.
    
- The ability to hunt for evidence left by sophisticated adversaries.
    
- The ability to investigate malware outbreaks and other suspicious network activities.
    
- The ability to continuously monitor endpoints for any suspicious user activities, i.e., insertion and extraction of files via USB devices.
    
- The ability to investigate any possible disclosure of confidential information.
    
- The ability to retrieve and gather data over time that can be used for threat hunting and future investigations.

## **VELOCIRAPTOR QUERY LANGUAGE(VQL)**

What makes velociraptor powerful and effortlessly flexible, is VQL (Velociraptor Query Language). VQL is a query language similar to the common query languages like SQL, which is used to create, configure and customize **artifacts**. Velociraptor artifacts allow you to collect, query, and monitor almost any aspect of an endpoint, fleet of endpoints, or entire networks. VQL can also be used to create automated rules on the server and continuous monitoring rules on endpoints.

## **INSTALLATION AND CONFIGURATION**

To install and configure Velociraptor, three deployment methods exist:

- **SSL-Self Signed -** For on-premise deployments.
    
- **Cloud Deployment -** For remote/easy deployments.
    
- **Instant Velociraptor -** For self-contained client and server on your local environment/machine.
    

For a detailed guide on how to deploy the above-mentioned deployment strategies, use the official guides here https://docs.velociraptor.app/docs/deployment/#instant-velociraptor.

### Installation of Velociraptor on Windows

To install velociraptor, navigate to the Velociraptor GitHub page, and download the latest release. Ensure you select the **.msi** release.

Then, on the windows host, open a command prompt and run the following command:

```
msiexec /i <velociraptor.msi>
```

NB: Ensure you replace the .msi file with the executable of the Velociraptor version that you downloaded.

> **NOTE:** The installation and Configuration has already be done on the VM. The Installation and Configuration commands listed below are for reference purposes only.

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/a2da09ac_VeloInstall.png)

Allow the installation to complete.

### Configuration of Velociraptor on Windows

Once installation is done, the next step is to run the setup configuration. For this stage, navigate to the **Installation Folder(C:\Program Files\Velociraptor)** of velociraptor.

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/9a4648dc_veloconfig.png)

Then run the following command:

```
Velociraptor.exe config generate -i
```

This command will run the Velociraptor Configuration Generator. After selecting the installation server as **Windows** in the first prompt, match or customize, the below configuration to configure velociraptor:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/869f2362_VeloCOnfigure.png)

### Start Velociraptor.

After configuration is complete, next, we need to start Velociraptor. To do so, we will execute the following command:

```
Velociraptor.exe --config server.config.yaml frontend -v
```

At this stage, we have completed the installation and configuration of the Velociraptor server. For this scenario, we will be using this server as both Server and Client. When using the msi installer, by default the client service of velociraptor is installed, therefore, we will only need to copy the client configuration file that was generated during configuration. In a mass deployment, you may use Group Policies to in effect this.

To do so, run the following command and start the client service:

```
copy client.config.yaml Velociraptor.config.yml
```

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/a2b1874b_client.png)

Then start the services:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/5dc6dc5b_StartVELO.png)

At this stage, you have successfully installed and configured Velociraptor.

## **USING VELOCIRAPTOR**

For this next stage, we are going to look at using velociraptor. To follow along, login to **VelociraptorServer VM** and access the velociraptor instance on a browser via the webproxy**.** Let's quickly get familiar with the UI, on login in, you are met with the **Dashboard**:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/2ffa1ab7_dashboard.jpg)

The dashboard gives a brief metrics of the CPU, Memory and Disk Space utilization of the server hosting Velociraptor (In this scenario, the host server is an Ubuntu server). The next important page to look at, is the client view. To see all the clients that Velociraptor is monitoring, click on the drop-down icon next to the search bar, then select **show all**:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/5adb3ed2_clients.png)

From this page, we can look at all the clients that Velociraptor is monitoring.

Each host/client has a unique Client ID that I used by velociraptor to identify each of the clients. If we click on **Workstation001**'s client ID, we are presented with a new page that gives us more information regarding this particular client:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/7ecf1059_cleintID.jpg)

The next important page, is the **VFS (Virtual File System) :** This gives you the ability to look at the file system of the client you are investigating. You are able to download folders/files should you wish to retrieve evidence from the client. However, this ability is only restricted to users with the Administrator roles.

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/05f8a72b_VFS.png)![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/8b433845_FilesC1.jpg)

You may need to click on the **Refresh Folder** icon that's on the right, to sync the files:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/bbffdaf7_refresh.png)

Now that we have some basic understanding of the GUI, let's proceed to next stage.

## **VELOCIRAPTOR ARTIFACTS**

Artifacts are what makes Velociraptor such an important tool to use. To utilize efficiently Velociraptor's artifacts, we need to get acquainted with the building blocks of these artifacts, and that is, the Velociraptor Query Language(VQL). Velociraptor packages the VQL (act as an engine for VQL) queries in artifacts. These artifacts are:

- Human Readable
    
- Stored in YAML files
    
- Can take parameters
    
- House or package VQL queries referred to as "sources"
    

### Artifacts

To understand the above concepts better, on the left pane of the Velociraptor GUI click on the **Artifacts** windows (circled in red in the picture below)**,** then select the first Artifact listed on the right side of the page:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/faf61fe5_artifacts.png)

Under the **Source** field, is where the VQL source query can be seen. The bonus of using Velociraptor is, we are able to modify the VQL queries of each artifact, as well as, create our own or source new ones from the community.

### Hunts

Now let us take a look at how the artifacts work, for this demo, we are going to retrieve the network statistics of the Ubuntu workstation (Workstation001). To do so, we will use the artifact **Linux.Network.Netstat**. This particular artifact will query the host and parse the **/proc** directory to reveal information about the current network connection. To access the hunts window, click on the "bullseye" icon on the left navigation pane:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/70202e24_hunt.jpg)

Next, click on the **+** icon to create a new hunt:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/2ead7902_net1.png)

Fill in the description, leave everything else to the default values and proceed to the **Select Artifacts:**

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/7d7ebca6_netstat2.png)

In the search field, search of either **Linux.Network.Netstat**, or by the keywords Netstat. Then select on **Linux.Network.Netstat** to select the artifact that will be used for this hunt. The next stage is to configure the parameters, click on the **Configure Parameters** :

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/fae7eaea_config.png)

The above artifact has one parameter that we can configure. **StateRegex**, this parameter houses the keywords we will be looking for, from the parsed network statistics, in our cases, we are seeking for Listening and/or Established ports/connections on the host. If we only wanted Established, connections, we could remove the Listening portion. However, for this example, we will leave everything as is. Next, we wont modify the resources, we will jump to the **Review** pane to review the artifact(s) we have selected:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/dd8d8d2b_review.png)

This pane shows as, in JSON, the artifact(s) we have selected, the conditions we have set and the name/description of our hunt. Next will click on Launch. Note, after clicking Launch, our hunt won't be running, all hunts by default are always set in a **Paused** state, so, in order to run the hunt, you must click on the hunt you created, the click the run icon (**Play Icon)**:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/ee6dfcb8_runit.png)

Each hunt and artifact contained within it, have varying scale on the amount of time and resources they will take to run. For our demo, we are running the hunt on a demo environment with no real concern of the cost of resources, however, in the real world, you should factor this in, and configure the resource tab of each hunt effectively. Keep in mind, certain artifacts are resource intensive while others are not. When creating a hunt, always plan a head on the type of artifact you will be using and the effect/cost of this artifact on the system.

Once the hunt has finished running, let's review the results:  
To review our results, we will click on the **Notebook** tab. Each hunt will have its own Notebook tab. This tab is populated with the results of our hunt. When a hunt is running, you can access the tab to see the results as they are populated. Once a hunt is complete, all the results will be displayed on this tab:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/6aa9ffc3_rest.png)

Each individual artifact will give you a results similar to the one shown above. Becuase of the query language (VQL) the results are formated into a table with columns and rows.

### Examples:

For this next segment, we are going to look at some more artifacts as well as create our own custom artifacts.

**File Finder**

In any DFIR investigation, getting any remnants or files that were used during an attack, is absolutely vital in aiding our investigation. For that purpose, we are going to learn how we can use the artifacts related to searching and acquisition of files within the clients. The first on the list, is the **Windows.Search.FileFinder.** This artifact is a great start when trying to locate select files, this artifact and many others like it, allow us to:

- Utilize wildcards to search all over/**"glob"** the directories
    
- Utilize Yara to search keywords within the contents of files
    
- Filter out our search scope by dates/time
    
- Upload matching files to the server, for further analysis.
    

For this example, login to **Workstation002** using the provided Lab Access Credentials. Create a file on the Desktop and name it **whereisfilo.txt**:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/37ac8833_fileo.jpg)

Next, on the hunt page, create a new hunt and name it **find file**. Then proceed to the select artifacts, and select **Windows.Search.FileFinder:**

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/230f2e16_filefind.jpg)

Now lets configure our parameters as shown below:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/377720ef_whereisfile.png)

To shorten the search time, we only asked Velociraptor to search within one users directory. In the real world, you might not be so lucky.

Before we proceed, let's review one or two more useful features about this particular artifact.

- **Upload_File -** This option will upload the files that match your search to the server for analysis.
    
- **Calculate_Hash -** This particular option will calculate the hash of the file (MD5 and SHA).
    
- **MoreRecentThan and ModifiedBefore** - To specify a time range, use either or both of this two options.
    

Now review your hunt and run it. Remember, all hunts by defualt are in the paused state so after setting up your hunt, remember to run it. This particular hunt is a good example of hunts that take fair amount of time and resources to execute. Once the hunts is done, review the results:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/21fc5dfe_filofoundo.jpg)

**User Information**

For our next example, we are going to show case how we can use Velociraptor's artifacts, to reveal some user information i.e., home directory, from the /etc/passwd folder. And while we are at it, we will introduce new concept of chaining more than one artifact, within a hunt. For this example, in the hunts menu, create a new hunt and name it **Basic User Info**, next, let's modify our hunt to be a little more effecient. In the New Hunt window, after typing in the description, modify the **Include Condition** by clicking on the drop down icon and select **Operation System.** Next, in the **Operating System Included** select **Linux:**

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/32ca75d4_basic.png)

Now lets select our artifacts, in the Select Artifacts window, choose these two artifacts:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/2bacaf94_select2.png)

NOTE: When chaining more than one artifact, a select artifact while always be highlighted in blue.

Now that we have selected our two artifacts, open the configure parameter. Here we will leave everything as is, and proceed to run the hunt. We should get results as shown below:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/52c945d1_Syslast.jpg)![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/d0aa0204_sysusers.jpg)

**Custom Artifacts**

Our last example, we wiill look at creating our own custom artifacts. Assume that we wanted to confirm whether or not a given executable is signed. To do this, we are going to create our own custome artifact, we will set the path to the executable file, in our case, the executable of the Velociraptor, and finaly, we will run the hunt. To do this, navigate to the Artifacts window and click on add:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/16bdcf3e_custom.png)

You are now presented with the defualt setup template for a custom artifact. Remember, artifacts use YAML and VQL Syntax:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/9c03d302_syntax.png)

Before we proceed, note the following:

- **Name and Description block** - the name block will house the name of your artifact. For best practice, use unique names and append the **Custom** keyword at the start, that way you aritifact will not overwrite and existing one and can be identified as a custom artifact. The description block house the a brief description of what your artifact does.
    
- **Parameter** - here is where you define all the parameter that the user can modify. Also asing a defualt value should they choose not to modify it.
    
- **Sources** - this is where your VQL query goes. VQL and Velocirpator come equiped with a variery of functions. Visit the main docs pages for a full guide https://docs.velociraptor.app/vql_reference/.
    

Now delete everything and paste the following code:

```
name: Custom.PE.Parser
description: |
   A custom artifact to parse executable files

type: CLIENT

sources:
  - precondition:
      SELECT OS From info() where OS = 'windows'

    query: |
      SELECT parse_pe(file='''C:\Program Files\velociraptor\Velociraptor.exe''')
      FROM scope()
```

Save your work. The new artifact should appear as follows:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/3adcda3f_final.jpg)

Next, navigate to the hunt window, create a new hunt, and on the **Select Artifact**, search for and select the custom artifact you created:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/dd1c93aa_CustomPE.jpg)

Because we didnt create any paramater, will skip the configure parameter and Launch our aritifact. Remember to run the aritifact. You should observe the following results:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/12674b69_signer.png)

As you can see, we have parsed the Velociraptor executable, the next to do, is open the **Authenticode** to see if this executable has been signed:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/6864f8c6_sigocdes.png)

As you can see, the executable has been signed.

Now before we wrap up, lets go through one last example, in this example, we are simply going to modify our previous custom artifact. Always note, all artifacts can be customized, however, its important to create a new custom artifact using the source "code" of the old artifact. This way, you can preserve and retain the functionality of prexisting artifacts. Therefore, navigate to the Artifacts window, and click on create a new artifact. Then paste in the following (remember to delete the exisiting default guidlines before pasting):

```
name: Custom.PEwithParam.Parser
description: |
   A custom artifact to parse executable files

# Can be CLIENT, CLIENT_EVENT, SERVER, SERVER_EVENT
type: CLIENT

parameters:
   - name: FilePath
    

sources:
  - precondition:
      SELECT OS From info() where OS = 'windows'

    query: |
      SELECT parse_pe(file=FilePath)
      FROM scope()
```

In the above snippet, we have added the parameter **FilePath** which will allow us to specify a file path to the file we wish to investigate. Save the new custom artifact, and run the a new hunt based of the newly created artifact:

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/857d6fcc_custom2.jpg)

Next, configure the parameters and add the following file path:

```
C:\Program Files\velociraptor\Velociraptor.exe
```

![](https://cdn.cyberranges.com/public/user/62666b5d574e500007c97d43/0d99e0d3_customparam.jpg)

Finaly, Launch and run your hunt. Your results will be similar to the previous hunt.

At this stage, you have completed this introduction.

# **THREAT HUNTING WITH VELOCIRAPTOR**

## **INTRODUCTION**

Velociraptor is a powerful open source DFIR and Endpoint monitoring tool. In this scenario, we are going to highlight how a cybersecurity analyst can use Velociraptor for threat hunting.

## **OUR ENVIRONMENT**

In this scenario, we have one velociraptor server and two workstations; A Windows workstation (Workstation001) and a Linux workstation (Workstation002). Each of these two workstations are being monitored by our velociraptor server. Each workstation has a set of unprivileged users as well as files and data that you will interact with through the velociraptor WebUI.

## **LET'S GO HUNTING**

Velociraptor is an open source DFIR and Endpoint monitoring tool kit that's built off GRR, OSQuery and Google's Rekall tools. It allows us as cybersecurity analysts to collect Forensic Evidence, by running **Hunts**. Each hunt consists of a **VQL (Velociraptor Query Language)** script, often referred to as an **Artifact**. VQL is highly customizable and is a query language similar to SQL, thus, enables us as analysts to modify existing artifacts or share with the community through the **Artifact Exchange** portal (https://docs.velociraptor.app/exchange/). In this scenario, we will go through a couple of examples to quickly highlight how we can utilize velociraptor for threat hunting.

### Hunt 1 – Knowing our environment.

In order to perform a successful threat hunt, we need to first understand our environment. As such, these set of examples will showcase how we can **Interrogate** our clients, identify unique details such as IP Address and any relevant information including users on a given client.

**Example 1:** Client Details

On the velociraptor instance, under the **Home Page,** click on the drop-down icon and select **Show All:**

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/6f6595ef_allclients.png)

We can see a list of the **Clients** we are actively monitoring:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/aab08ec1_clients.png)

Select **Workstation001** by clicking on the **Client ID,** we have navigated to the **Host Information** page:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/713cd5ce_w001info.png)

From this page we can see some information about our host, including the IP address, operating system and the version of windows running on the host. Clicking on the **Interrogate** button will refresh the details provided here.

On the far right, we have a couple of other options that we can use to get more information regarding our host.

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/9c15f1c6_Velociraptor1.png)

Currently, the landing page of the Host Information page, is the **Overview**:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/713cd5ce_w001info.png)

Under the **VQL Drilldown** we can see further statistical details including the run times of our client, CPU and memory usage, agent information and active users:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/016968d6_vqldrilldown.png)![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/e458f1c4_vqgl.png)

In the **Shell** section, you can run specific commands against the client. Keep in mind that, there are limited commands. Run the **ipconfig** command and click on show to see the results:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/e0e35131_ipconfig.png)![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/fa543686_ipconf.png)

Now let's grab some details of the users present in your client. Under the **Hunt** menu, create a new **hunt** and name it with a suitable name:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/2f7a5db4_hunt.png)

Modify the **Include Condition** to only run our hunt on a specific operating system, for our case windows:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/43bc4acc_include.png)

Under the **Select Artifacts**, we will use **Windows.Sys. Users** artifact. Select it and click on **Launch.** We won't be configuring our artifact:

> Linux equivalent artifact **- _Linux.Sys.Users_**

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/d3d7016d_firtL.png)

Remember to run your scenario:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/5e35377d_runit.png)

Under the **Notebook** section, we can review the results of our hunt:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/013efa7b_users.png)

### Hunt 2 – Getting Browser History and Cookies

Now let's see how we can get some browser history of users on our endpoints. Create a new hunt and use the artifact **Windows.Applications.Chrome.History**:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/d77fc244_chromehist.png)

Run this hunt against your windows client and see which results you get:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/6f44e80c_kellyhist.png)

**Note:** Your results might differ.

### Hunt 3 – Looking for PUPs

A PUP refers to a Potentially Unwanted Program, for this session, we have a couple of the executables we are going to search, they have been spread around our hosts. Don't worry, these are not malicious however, we will use them to simulate how you can go about searching for PUPs within your environment or during an Incident Response activity.

Our PUPs in this scenario will be the **velociraptor** binary. Our Workstation001 will act as our host with a PUP. First, let's check for any outbound connections. Velociraptor uses port 8000 for client server communications, hence we will use this our simulation of PUP setting up a network connection:

For this, we will use the artifact **Windows.Network.Netstat,** set up your hunt and run it:

> Linux equivalent artifact **- _Linux.Network.Netstat_**

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/7856e397_velo.png)

As we can see, we have an established connection made between our workstation and Velociraptor server.

> Please note, you will need to navigate through the results to identify the velociraptor executable.

Now that we have identified our "PUP", let us get more details about it.

Create Another Hunt, for this, we will use **Windows.Forensics.Prefetch** Artfact. This artifact will retrieve properties about our executable, including the last time it was run.

We will configure this artifact to specifically target our PUP, **Velociraptor.exe** as shown below,

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/4a80546e_prefetch.png)

Under the **binaryRegex** field, type in the name of our executable, **Velociraptor.exe**. Run the artifact and let's review the results:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/7761b706_prefe2.png)

We have identified the details about our executables, including the **last time it was run**, **run counts** as well as the **creation time**.

Now let's gets some more details that we can use to build an IOC, for this, we will use **Windows.System.Pslist**. This artifact allows us to collect running process and their equivalent binaries:

> Linux equivalent artifact **- _Linux.Sys.Pslist_**

Remember to configure the artifact, under the **processRegex** type in the name of our executable:

Under the **processRegex** field, enter **Velociraptor.exe** which is the name of our executable. Run the artifact and let's review the results:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/21c06fcf_Velociraptor2.png)

Reviewing our results, we can see:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/8e1c2ed1_psres.png)

We have collected more details regarding our executable, including the **cmd** arguments, **hashes** as well as the digital signing details of the binary (**Authenticode**).

### Hunt 4 – VFS

Our final hunt will focus on gaining access to our remote host, via the Virtual File System feature offered by Velociraptor. There are situations where you may not be able to remotely log in to a host, as such, we can use VFS, to remotely view the file system of our endpoints. To do so, we are going to select Workstation001, then navigate to **Virtual File System**:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/e1eac472_vfs.png)

Click on **Recursively refresh** to sync the client files to velociraptor:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/33768203_vfssynch.png)

Depending on how large the system is, syncing files might take a fair chunk of time:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/d4aaa20c_synching.png)

Now click **ntfs** to open the client's file system. You may have to click on **Refresh this directory/Recursively refresh** to sync the data:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/b2327452_vfsopen.png)

Then click on **\\.\C:** , navigate to **Users\kelly\Desktop:**

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/3e6fe285_kellyDesktop.png)

We can see, a couple of files are present on the workstation.

VFS allows us to **Collect** files, this means, we can upload the remote files onto our Velociraptor server, and download them for further analysis. To showcase this, open the **Personal** folder under kelly's desktop files:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/de03db4e_personal.png)

On the right pane, click on **Vac.png**:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/68495950_collect.png)

When you select a file, you will be presented with various options:

1. **Stats:** is a quick brief of the file properties.
    
2. **Textview:** allows you to see any text withing a compatible file.
    
3. **HexView:** allows you to view hexadecimal structure of a compatible file.
    
4. **Collect from the client:** the selected file will be uploaded to the server, and you can download it.
    

> **Note:** Use the Collect function sparingly. Uploading of content depends on the storage capability of the server hosting the velociraptor instance.

On clicking **Collect from the client**, a download icon should appear under the **Last Collected** field:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/fe4a2d9a_collecting.png)

You can then click the **Download Icon** to download the collected evidence:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/29a4b357_downloaded.png)

You can then proceed to investigate the downloaded file.

### Hunt 5 - Creating Custom Artifacts

On this segment, we will look at creating custom artifacts. VQL is a powerful query language, we can customize existing queries to craft some custom artifacts.

**Example:**

How can we identify if a windows executable is a legitimate program written by the purported developer and not a malware? Microsoft had introduced a standard called Authenticode, designed to sign trusted binaries, so they can be identified by the operating system. Additionally, recent versions of Windows will not load any unsigned device drivers, therefore maintaining the kernel integrity.

To view whether a binary has been signed, navigate to the **Properties** section of the binary, and click on **Digital Signature** tab:

![](https://cdn.cyberranges.com/public/user/62e3bc1724b42e00074b569d/ec0296e0_sign.png)

**Basic Syntax**

Before we can create a custom artifact, let's first have a quick rundown on the VQL language.

VQL has a basic set of functions and plugins which allow you to manipulate data and implement some custom logic. There are three key ways of running a VQL query:

1. Via the command line as a velociraptor query (Shell)
    
2. Inside the Notebook
    
3. Via an artifact.
    

In our case, we are going to focus on the last method, as we have interacted with artifacts in this scenario.

The basic syntax of a VQL query has the **SELECT _x,y,z_ FROM _plugin(arg=1)_** AND **WHERE x=1** clauses, with your column selectors and filter conditions being added in between the clauses. The structure is almost identical to SQL.

**Understanding the VQL syntax**

**Plugins**: VQL is similar to SQL however, the data sources are not static tables. Data is generated by plugins that produce rows. These plugins are always placed after the **From** clause. VQL plugins use parameters to customize and control their operations. VQL Syntax requires all arguments to be provided by name (these are called keyword arguments). Depending on the specific plugins, some arguments are required while others maybe optional.

**Functions:** VQL functions are not be mistaken for plugins, functions return a single value, instead of rows and often come after the **Select** clause.

> VQL does not place any restrictions on the use of whitespace in the query body and semicolons are not required.
> 
> The **?** can be used to view a list of possible completions/combinations for a keyword.

Alright, now, navigate to the **View Artifacts** window, and click on **Add:**

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/c9ccf099_custom1.png)![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/15fca118_notebook.png)

Velociraptor provides us with a **notebook** text editor that is used to write/create our custom artifacts. VQL syntax is written in YAML format, so bare that in mind when writing your own artifacts. Beyond creating our own custom artifacts, you can also customize existing ones as well, though this is highly discouraged. Best practice When building new artifacts, use the **Custom** keyword before the descriptive name of the artifact.

Speaking of artifacts, lets create our own, we want our artifact to scan an executable and get the authenticode details:

```
name: Custom.Parse.PE
description: |
   This is a custom artifact to parse PE

# Can be CLIENT, CLIENT_EVENT, SERVER, SERVER_EVENT
type: CLIENT


sources:
  - precondition:
      SELECT OS From info() where OS = 'windows' 
      
    query: |
      SELECT FullPath, parse_pe(file=FullPath), authenticode(filename=FullPath)
      FROM glob(globs="C:/Program Files/Velociraptor/Velociraptor.exe")
```

The above will do the following:

- Name: we specify the name of our artifact.
    
- Description: We provide a description of our artifact.
    
- Type: we specify where our artifact is intended to run (on our Velociraptor server host, or against the monitored endpoints).
    
- Sources: Where our queries will be dictated.
    
    - Precondition: We can define a condition that will determine whether our query should execute. For the below, we have set the condition to only check for a windows operating system and only run on those hosts/endpoints.
        
    - Query: where our custom VQL query will go.
        

Now back to our query, **FullPath** is a local variable that we use to store the filepath of our file. **parse_pe** is used to parse our executable. **authenticode** this plugin parses authenticode information from PE files. **glob** plugin allows as to search for files by their names or even use a wildcard.

Now copy the above and paste it in the notebook section of our custom artifact:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/f14238bc_pe.png)

Save the artifact and run it as hunt:

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/8e8b0e73_res.png)

As you can see, parsed our executable and retrieved the authenticode details. We can see that the executable is signed.

**Hash Artifact - File search by hash**

Let's look at our final example and introduce **parameters** as well as show case the usage of the **where** clause. This custom artifact will search the system for a given file by matching the file to a hash and size. Searching for a file by its hash is the most common DFIR practice during an incident investigation or threat hunt. In our case, velociraptor can do the same. However, because of the computational needs, we will avoid having velociraptor manual search through each file, calculate the hash, then check if it matches our hash. For that, we will use the file size. Granted, this scenario assumes you have the file size, in a real-life situation, you might not be so lucky. In our case, we are using the Velociraptor executable, we have its file size and sha256 hash:

```
name: Custom.Hash.Search
description: |
   This is a custom artifact to find a file by hash

# Can be CLIENT, CLIENT_EVENT, SERVER, SERVER_EVENT
type: CLIENT

parameters:
   - name: SizeofFile
     type: int
     default: 46098856
   - name: FileHash
     default: "df93462351b227368d2398f94964ede6e19c694b19bc82ce9908ea8754beb5ce"

sources:
  - precondition:
      SELECT OS From info() where OS = 'windows' 
      
    query: |
      SELECT *, hash(path="C:/" + FullPath) AS Hash
      FROM parse_mft(filename="C:/$MFT", accessor="ntfs")
      WHERE FileSize = SizeofFile AND Hash.SHA256 = FileHash
```

The Parameters field houses our variable information, so if we wanted to adapt our artifact later on for another purpose apart from searching for velociraptor, we can simply do so under the **Configure Parameters** field:

- **name:** the name of our parameter
    
- **type:** we specify the type of variable we are using, integer, float, etc. If we are working with Integers, i.e., the file size which is in **kilobytes,** we will use the **int** keyword.
    
- **default:** if no input is provided, the default will act as our default input.
    

Now Add this new artifact and run it, you should get similar results to the one shown below:

> **Note:** _This type of artifact might take some time to execute as Velociraptor will need to calculate the hashes to match our hash._

![](https://cdn.cyberranges.com/public/user/62df8d3224b42e000749997b/97c2024f_res2.png)

As shown, you can create your own custom artifacts, from the two examples, while limited, they quickly show case how an analyst can customize and create a custom artifact suitable to their needs. For more details on the various plugins and functions offered by velociraptor, you can visit the VQL Reference page (https://docs.velociraptor.app/vql_reference/) where you can get to search through the many functions and plugins available.

### Notable Artifacts

While the above example used a few artifacts as samples, here are a couple of noteworthy artifacts that can be used. Keep in mind, you can explore velociraptor's array of artifacts to identify what data they collect.

- **Linux.Syslog.SSHLogin** - identify all SSH logins on Linux.
    
- **Windows.Detection.BinaryHunter** - A powerful artifact that hunts through binary attributes. Highly customizable.
    
- **Windows.Forensics.SAM** - get user account information from the SAM hive.
    
- **Linux.Network.Netstat** - parse through /proc on Linux and identify any network connections.
    

To name but a few.

Congratulations, you have successfully completed this scenario.