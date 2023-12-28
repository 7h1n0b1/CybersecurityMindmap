#Defensive #LogAnalysis #NetworkLogs

# **ANALYSING NETWORK TRAFFIC USING ARKIME**

Arkime is an open source piece of software that can be used to capture live traffic and index very large PCAP files into Elasticsearch. Unlike other packet analyzers, Arkime comes with a simple and user-friendly

web interface that you can use for browsing, searching, and even decoding captured packets using Cyberchef (Cyberchef is  a web app for encryption, encoding, compression and data analysis).

It also has a feature called Hunt  which allows an analyst to search within the packets themselves rather than searching the session metadata. We will learn more about Cyberchef and Hunt in the next sections.

## **ARKIME COMPONENTS**

Arkime system is comprised of 3 components:

- **Capture** - A threaded C application that monitors network traffic, writes PCAP formatted files to disk, parses the captured packets, and sends metadata (SPI data) to elasticsearch.
    
- **Viewer** - A node.js application that runs per capture machine. It handles the web interface and transfer of PCAP files.
    
- **Elasticsearch** - The search database technology powering Arkime.
    

Arkime has been installed in this scenario. Under Servers, click on Arkime webproxy to access the Arkime web interface. When prompted for username and password enter the following credentials :

Username: admin

Password: password.

This web interface has 4 views of captured packets. These views include Session page, SPIView page, SPIGraph page and Connections Page. We are going to discuss more about these four views In the next section.

Note: Change your timetstamp from 21/12/2021 to 22/12/2021.

## **SESSIONS PAGE**

This is the primary view page that contains a list of sessions. The Sessions page displays a list of indexed sessions for the selected time period and search expression. It includes a timeline graph

and map of the session results. The screenshot below shows the Sessions Interface.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/1d442266_Selection_182.png)

The **Sessions** view has several controls that can be used to filter the sessions displayed from all sessions to specific sessions of interest. We are going to discuss about this controls in the next section.

### **SEARCH BAR**

The **search bar** is indicated by a magnifying glass  icon. This control allows you to define filters on session/log metadata. This is where search filters are entered. For example if you wish to filter for events related to this

IP 192.168.125.13, enter `ip == 192.168.125.13` query on the search bar as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/8f34523d_Selection_250.png)

### **TIME BOUNDING CONTROLS**

The **Time**, **Start**, **End**, **Bounding**, **Interval** fields, and the **date histogram** can be used to visually zoom and set time range per users wish. The **Time**, **Start**, **End**, **Bounding**, and **Interval** fields, and the **date histogram** are highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/b77fbca6_Selection_2523.png)

### **SEARCH BUTTON**

The **Search** button helps to re-run the sessions query with the filters currently specified. The Search button is highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/3292fc4c_Selection_2524.png)

### **VIEW BUTTON**

The view button is indicated by the eyeball  icon. Views allow overlaying additional previously-specified filters onto the current sessions filters. The view button is highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/af52ddd4_Selection_2525.png)

### **MAP**

A map helps in filtering sessions by IP-based Geo-location.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/49a11a34_Selection_2526.png)

You can expand this by clicking the globe  icon. You can click a country on the map to apply it as search criteria.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/d82fbcd7_Selection_2527.png)

You can also filter the traffic by country by clicking on the country on the map. For example we have clicked on United States hence the output will indicate traffic related to US as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/75eea04a_Selection_2609.png)

### **SESSION DETAIL**

The Session detail allows you to get more information about any session. You can view the session's more information by clicking the "+" button on the left side of each row highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/af6822f5_Selection_2528.png)

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/5101a332_Selection_2529.png)

Each row may contain multiple sections and controls. Clicking the field names and values in the details sections allows additional filters to be specified or summary lists of unique values to be exported.

### **TOGGLE VISIBLE COLUMNS**

The **Toggle visible columns** button, indicated by a grid  icon, allows toggling which columns are displayed in the sessions table.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/ee6fa09c_Selection_2532.png)

### **SAVE OR LOAD CUSTOM COLUMN CONFIGURATION**

The **Save or load custom column configuration** button, indicated by a columns  icon, allows saving the current displayed columns or loading previously-saved configurations. This is useful for customizing

which columns are displayed when investigating different types of traffic. Column headers can also be clicked to sort the results in the table, and column widths may be adjusted by dragging the separators between column headers.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/c5c060b8_Selection_2533.png)

## **SPIVIEW PAGE**

SPIView is an acronym for Session Profile Information View. This page allows the user to see all the unique values for each field that Arkime understands as shown in the screenshot below. It lists categories for general session metrics for protocol, source and destination IP addresses, sort and destination ports, as well as for all of various types of network understood by Arkime.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/0ac8985b_Selection_2608.png)

These categories can be expanded and the top unique values displayed, along with each value's cardinality, for the fields of interest they contain as shown below. Click the the plus **➕** icon to the right of a category to expand it.

The values for specific fields are displayed by clicking the field description in the field list underneath the category name.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/08de84ef_Selection_2540.png)

We are going to discuss several controls that can be used to during investigation under SPIView.

### **SEARCH**

Search is used to filter out a specific field name from a list of field names. This can be dome by typing part of the field name in the Search to display in this category.

For example, filtering for Src IP field, you will enter "Src IP" on the Search for field as my text input as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/fa33945c_Selection_2536.png)

### **THE LOAD ALL AND UNLOAD ALL BUTTONS**

This buttons can be used to toggle display of all of the fields belonging to that category. Once displayed, a field's name or one of its values may be clicked to provide further actions for filtering or displaying that field or its values.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/c0ff7975_Selection_2537.png)

### **OPEN [FIELDNAME] SPI GRAPH OPTION**

SPIView has an Open [Field Name] SPI Graph  Option which gives you an opportunity to open an SPIGraph using field names. To open, click on a field's name, for a example let's click on **Src IP** field name, then **Open Src IP SPI Graph** option as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/1a854d86_Selection_2538.png)

This will open a new tab with the SPI Graph populated with the Src IP field's top values as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/e8ed3ee6_Selection_2539.png)

### **CONNECTIONS PAGE**

Connections page allows you to see the relationship between different IPs, even on an internal network level. This feature is useful in different ways. Forexample, you can use this to see which hosts

are making the same type of connection to a known malicious host as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/5ebc2508_Selection_206.png)

Controls are available for specifying the query size , which fields to use as the source and destination for node values, a minimum connections threshold, and the method for determining the "weight" of the link between two nodes.

Clicking on a node or the link between two nodes can be used to modify query filters, and the nodes themselves may be repositioned by dragging and dropping them.

A node's color indicates whether it communicated as a source, a destination, or both. The black indicates source, green indicates destination and blue indicates both source and destination as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/a05aab6c_Selection_2541.png)

In the following section we are going to discuss some of the Connections View controls.

#####  **NODE INFO**

Hover over a node or a link to view more information or hide it as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/03c1603c_Selection_2543.png)

##### **CHANGE SOURCE/DESTINATION NODES**

By default source and destination fields are Src IP and Dst IP. The Connections view is able to use any combination of any of the fields populated by Arkime. You can make a selection from the Src and Dst

drop downs to visualize your data based on different captured field relationships. For example in the in screenshot below, we have changed the Source to be the Source IP and Destination to be destination Country.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/070aeada_Selection_2546.png)

##### **SAVE PNG**

This control helps to save/export the graph as a png or image. Clicking on the highlighted icon will pop up a window requesting to save a .png file.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/09ca707c_Selection_2542.png)

## **HOW TO INVESTIGATE WITH ARKIME**

Arkime has some built in functionality in the viewer to help you filter over different types of network traffic, and to filter by specific properties. For example, you can filter network traffic by type `“http”` and then filter by `“URL”` and many more. Arkime also gives you an option of decoding packets using Cyberchef and also create hunt jobs which allows an analyst to search within the packets themselves. In the next section we are going to discuss how to use Arkime to achieve the stated above. All of this filters will take place at the Sessions View page.

### **SETTING TIME DURATION**

By default Arkime displays the last one hour. This can be adjusted by clicking on the **🕘 icon** field shown below. This field has more default time settings such as Last hour, Last 6 hours, Last 12 hours, Last 24 hours, Last 48 hours, Last 72 hours and many more. For this section we will select the Last 1 hour as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/e97756f0_Selection_212.png)

You can also customize time by clicking on `Start` field to set date and time for the starting time then, click on `End` field to set the ending time as highlighted below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/df840e7a_Selection_213.png)

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/f8a172cf_Selection_215.png)

Once done, click button to query the the traffic based on the time range set as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/b0e8d7b7_Selection_219.png)

## **USING ARKIME FILTERS**

**Arkime has several filters that can be helpful in searching for specific traffic. In the next section we are going to discuss about those filters.**

**NOTE: == and = will display the same results.**

**You can use a filter with a spacing in between or you can ignore the spacing in between for example** `protocols == http` **and** `protocols==http` **will display similar results.**

### **FILTERING BY PROTOCOL**

On the search bar, enter `protocols == (protocol name)` or `protocols = (protocol name).`

For example for http protocol , on the search bar, enter `protocols == http`. The session will display all packets related to http protocol as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/10d18e17_Selection_218.png)

You can also filter out or exclude a specific protocol by using ! symbol as shown below.

On the search bar, enter `protocols != (protocol name)` .

For example for http protocol , on the search bar, enter `protocols != http`. The session will display all packets except packets related to http protocol as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/1aea6d61_Selection_2560.png)

### **FILTERING BY USER AGENT**

On the search bar, enter `http.user-agent == (User Agent Name)`or `http.user-agent = (User Agent Name)`

For example, searching for `Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:95.0) Gecko/20100101 Firefox/95.0` on the search bar, enter `http.user-agent == "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:95.0) Gecko/20100101 Firefox/95.0"`. The session will display all packets related to the said user agent as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/583c390f_Selection_216.png)

You can also filter out or exclude a specific user agent by using ! symbol as shown below.

On the search bar, enter `http.user-agent != (User Agent Name)` .

For example to exclude `Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:95.0) Gecko/20100101 Firefox/95.0` user agent , on the search bar, enter `http.user-agent != "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:95.0) Gecko/20100101 Firefox/95.0"`. The session will display all packets except packets related to`Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:95.0) Gecko/20100101 Firefox/95.0` user agent as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/8f822cc9_Selection_2561.png)

### **FILTERING BY URI**

On the search bar, enter `http.uri == (URI Name)`or `http.uri = (URI Name)`.

For example for `bcsl6zsvwnwfe6kd8lbpweyavq.web.proxy.cyberranges.net/api/eshealth` URI , on the search bar, enter `http.uri == bcsl6zsvwnwfe6kd8lbpweyavq.web.proxy.cyberranges.net/api/eshealth`. The session will display all packets related to http protocol as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/bd3378f3_Selection_217.png)

You can also filter out or exclude a specific URI by using ! symbol as shown below.

On the search bar, enter `http.uri != (URI Name)` .

For example for `bcsl6zsvwnwfe6kd8lbpweyavq.web.proxy.cyberranges.net/api/eshealth` URI , on the search bar, enter `http.uri != bcsl6zsvwnwfe6kd8lbpweyavq.web.proxy.cyberranges.net/api/eshealth`. The session will display all packets except packets related to `bcsl6zsvwnwfe6kd8lbpweyavq.web.proxy.cyberranges.net/api/eshealth` URI as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/2820e19b_Selection_2568.png)

### **FILTERING BY IP**

Filtering query is helpful when you are filtering an IP without knowing whether an IP is a source or destination. To the filter out, on the search bar, enter `ip == (IP Address)`or `ip = (IP Address).`

For example `ip == 10.2.0.5`. The session will display all packets related to 10.2.0.5 as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/50659758_Selection_2584.png)

You can also filter out or exclude a specific ip by using ! symbol.

On the search bar, enter `ip != (IP Address)` .

For example for 10.2.0.5 ip , on the search bar, enter `protocols != 10.2.0.5`. The session will display all packets except packets related to 10.2.0.5 ip as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/51c519d9_Selection_2564.png)

### **FILTERING BY SOURCE IP**

On the search bar, enter `ip.src == (IP Address)`or `ip.src = (IP Address)`.

For example `ip.src == 10.2.0.5`. The session will display all packets originating from 10.2.0.5 as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/f832d074_Selection_2566.png)

You can also filter out or exclude a specific source ip by using ! symbol.

On the search bar, enter `ip.src != (IP Address)` .

For example for 10.2.0.5 ip , on the search bar, enter `ip.src != 10.2.0.5`. The session will display all packets except packets related to 10.2.0.5 ip as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/6f107171_Selection_2565.png)

### **FILTERING BY DESTINATION IP**

On the search bar enter `ip.dst ==(IP Address)` or `ip.dst = (IP Address)`.

For example `ip.dst == 192.168.125.13`. The session will display all packets going to 192.168.125.13 as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/a24d17ec_Selection_2583.png)

You can also filter out or exclude a specific destination ip by using ! symbol.

On the search bar, enter `ip.dst != (IP Address)` .

For example for 192.168.125.13 ip , on the search bar, enter `ip.dst != 192.168.125.13`. The session will display all packets except packets related to 192.168.125.13 ip as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/5f268dde_Selection_2567.png)

### **FILTERING BY PORT NUMBERS**

This filtering query is helpful when you are filtering a port without knowing whether it is a source or destination. To filter out, on the search bar, enter `port == (port number)`or `port = (port number).`

For example `port == 8005`. The session will display all packets related to 8005 as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/316ab935_Selection_2569.png)

You can also filter out or exclude a specific source port by using ! symbol.

On the search bar, enter `port != (port number)` .

For example for port number 8005 , on the search bar, enter `port != 8005`. The session will display all packets except packets related to 8005 port as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/ab5d7247_Selection_2570.png)

### **FILTERING BY SOURCE PORT NUMBERS**

On the search bar, enter `ip.dst == (port number)`. This will display all packets that contain a specified source port number.

For example `port.src == 0` as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/0d0e7128_Selection_2571.png)

You can also filter out or exclude a specific source port by using ! symbol.

On the search bar, enter `port.src != (port number)` .

For example for 0 source port , on the search bar, enter `port.src != 0`. The session will display all packets except packets related to 0 port as source port as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/748d824f_Selection_2582.png)

### **FILTERING BY DESTINATION PORT NUMBERS**

On the search bar, enter `port.dst == (port number)`. This will display all packets that contain a specified destination port number.

Example `port.dst == 8005` as shown in the screenshot below below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/8ee5e0b2_Selection_2572.png)

You can also filter out or exclude a specific source port by using ! symbol.

On the search bar, enter `port.dst != (port number)` .

For example for 0 source port , on the search bar, enter `port.dst != 8005`. The session will display all packets except packets related to 8005 port as destination port as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/b21dfcbf_Selection_2581.png)

### **FILTERING USING MULTIPLE QUERIES**

Arkime gives us an option of filtering packets using multiple queries by using and (&&), or or. In the next section we are going to cover some situations that we may require two use more than one Search query.

For example if you wish to filter for events originating from `10.2.0.5` whose destination address is `192.168.125.13`and the port number should not be 0. We will use this query `ip.src == 10.2.0.5 && ip.dst == 192.168.125.13 && port != 0`.

Note = and == signs gives the same results.

We will get the results as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/d113bac1_Selection_2573.png)

The next example we are going to use the or (||) to filter for events. This will match either of the specified filter. For example filtering for port number 80 or IP address 192.168.125.1, we will enter `port == 0 || ip == 192.168.125.1` as our query. We will get the results as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/523df6da_Selection_2575.png)

## **USING HUNT**

The **Hunt** feature allows an analyst to search within the packets themselves (search within session packets for text) rather than simply searching the session metadata. The search string may be specified using ASCII , hex codes, or regular expressions. Once a hunt job is complete, matching sessions can be viewed in the Sessions view.

To perform a hunt, users should start by narrowing down their search on the Sessions page. Then, switch to the Hunt tab where any new hunt will only search within the sessions searched for earlier.

### **CREATING A PACKET SEARCH JOB**

By default Hunt page is blank since we dont have any hunts created as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/dc879e9e_Selection_2585.png)

To begin creating your hunt job, Enter the search query on the search field as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/147e0a7b_Selection_2586.png)

Click on the "Create a packet search job" button on the top right of the page as highlighted below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/ee5fb3aa_Selection_2587.png)

Assign the Packet search job name. I will name it "Sample" as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/049e6ca2_Selection_226.png)

Assign Max number of packets to examine per session. I will assign "1000" as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/6346ac3f_Selection_227.png)

Enter search text. I will enter "http" as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/606d1433_Selection_2589.png)

Click "Create" button highlighted below to create the Packet search job

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/0a56d0aa_Selection_2590.png)

Once a hunt job is submitted, it will create Packet search job as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/6539015d_Selection_229.png)

The hunt job will be assigned a unique hunt ID (a long unique string of characters like 5KypSX4BlMA789MBDi9S) and its progress will be updated periodically in the **Hunt Job Queue** with the execution percent complete, the number of matches found. More details for the hunt job can be viewed by expanding its row with the plus **➕** icon on the left as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/0d449bbb_Selection_2591.png)

### **VIEWING HUNT JOB**

To view more details about the Hunt job, click the + sign drop down icon on the left (highlighted highlighted on the screenshot below ) to expand its row .

This will display the status, the number of sessions found per search text, the time it was created, number of packets being examined per session, the session query, session

query time range and whether hunt is being shared or not as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/a72d44f2_Selection_230.png)

We will discuss few hunt controls in the next section.

### **THE REPEAT THIS HUNT CONTROL**

This control gives the Arkime user an opportunity to create another hunt job using the time frame and search criteria of the existing hunt selected as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/423db06c_Selection_2593.png)

As shown in the screenshot below, the highlighted fields has the same search criteria as the existing hunt selected.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/2267cec4_Selection_2594.png)

By clicking "Create" button, another Hunt Job will be created as shown below,

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/da8d9875_Selection_2595.png)

### **RERUNNING THE EXISTING HUNT CONTROL**

The rerun icon gives the Arkime user an opportunity to rerun another hunt job using the time frame and search criteria of the existing hunt selected by clicking the highlighted icon in the screenshot shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/6fea9912_Selection_2602.png)

As shown in the screenshot below, the highlighted fields has the same search criteria as the existing hunt selected.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/2267cec4_Selection_2594.png)

Note that the timestamp of the created hunt has changed from the Last hour to custom. This is because the hunt job created used the time frame of the existing hunt job selected.

By clicking "Create" button, another Hunt Job will be created as shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/ac8985d3_Selection_2596.png)

### **OPENING RESULTS IN A NEW SESSIONS TAB USING HUNT ID**

When clicking on a folder icon highlighted in the screenshot below,

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/4dd9d102_Selection_2598.png)

When a folder icon is clicked, another Sessions tab with ID hunt filter on the search bar will be opened as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/0c632296_Selection_2597.png)

**Note:** ES takes a while to update sessions, so your results might take a minute to show up depending with the available data.

### **REMOVING THE HUNT JOB**

Click on the delete icon to delete the selected hunt job as highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/999f4f6c_Selection_2599.png)

For our case we are removing the hunt job with ID B49dJn4BSR381ukl7ULK. Clicking on the delete icon, the hunt job will be deleted.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/a012a331_Selection_2600.png)

As shown in the screenshot below we have successfully removed the hunt job with the ID B49dJn4BSR381ukl7ULK.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/918d1034_Selection_2601.png)

## **USING CYBERCHEF**

Cyberchef is a web app for encryption, encoding, compression and data analysis. During traffic analysis we may come across some packets that are encoded or encrypted in different formats. Arkime web interface has Cyberchef that helps the packet analyzer in decrypting, formatting decoding captured packets.

### **HOW TO USE CYBERCHEF IN ARKIME**

On the Sessions view page, Click on plus sign (+) drop down icon to expand the packet to view more information about the packet as shown below:

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/53eb4b7d_Selection_2603.png)

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/f7a28ac3_Selection_2604.png)

Scroll down to "Packet Options" tab shown below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/7e176b72_Selection_2605.png)

Click on "Packet Options" drop down to view more options.

We will get several options which includes,Show Raw Packets, Show Packet Info, Enable Uncompressing, Show Images and Files, Open src packets with CyberChef, and Open dst packets with CyberChef as shown in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/012890b2_Selection_2607.png)

For example, to open Cyberchef by Source packets, click "Open src packets with Cyberchef" option.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/94678dc7_Selection_2606.png)

This will open a new tab for Cyberchef web app and display the decoded content if we had any encoded data.

### **DOWNLOADING FILES WITH ARKIME**

On the Sessions view page, expand a session of your preference by clicking on plus sign (+) drop down icon to expand the session.

Then click on **Packet Options** drop down highlighted below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/4a2a9099_Selection_200.png)

Then click on **Show Files and Images** highlighted below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/ff83f86e_Selection_201.png)

This will display all files and images available as shown in the sample below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/8fe6d7da_Selection_202.png)

Click on the file or image name to download it.

### **EXPORTING PCAP FILES**

Unlike other packet analyzers, Arkime gives you an option to export search results as PCAP or CSV. the **PCAP Export** feature allows you to create a new PCAP file from the matching Arkime sessions, including controls for which sessions are included and whether or not to include linked segments.

To export or download a PCAP , open session by clicking the plus + sign, this will expand the session.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/152590e4_Selection_2576.png)

Under sessions, move t o Actions and click the drop down, then click **Export PCAP** button to generate the PCAP, after which you'll be presented with a browser to enter the PCAP file name download dialog to save or open the file.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/8f2e990e_Selection_2577.png)

Enter the PCAP filename as highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/ca43f740_Selection_2578.png)

Then click on Export PCAP to download the PCAP file as highlighted below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/8768aa45_Selection_2579.png)

You can also download the PCAP file of the session by clicking on the Download PCAP option highlighted in the screenshot below.

![](https://cdn.cyberranges.com/public/user/61b34dee16e4af00075e1c78/4b13becc_Selection_2580.png)

This brings us to the end of this tutorial.