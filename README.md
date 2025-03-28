# ELI 211 Splunk Lab


## Lab 1: Installing Splunk

1. [Download Splunk Enterprise](https://www.splunk.com/en_us/download/splunk-enterprise.html), we will be downloading the tar file (.tgz extension)
2. Open the Terminal and navigate to the Downloads folder:

```cd ~/Downloads```

3. We will use the tar utility to open the file and install it in the opt directory:
   
``` sudo tar -xvzf splunk-9.4.1-e3bdab203ac8-linux-amd64.tgz  -C /opt ```

4. To start Splunk navigate to the Splunk bin folder

``` cd /opt/splunk/bin  ```

Then start Splunk by entering

``` sudo ./splunk start ```

 (hit the space bar to scroll through the license and approve)

5. Create a new Splunk administrator account name it "admin" and create a password and write it down. 
6. Once Splunk has started up open Firefox and go to 127.0.0.1:8000 and log into Splunk with the admin username and password you just created. 

![Splunk Login](/img/splunk1.png)

7. Let's make it so that Splunk starts with the system boots, navigate back to the Splunk bin folder and enter this command: 

```sudo ./splunk enable boot-start ```

## Lab 2: Onboarding Data & Basic Searching

Reference: Splunk SPL (
[Splunk SPL (Search Processing Language)](https://docs.splunk.com/Documentation/SplunkCloud/9.2.2403/SearchReference/UnderstandingSPLsyntax)

1. We will onboard a CSV file of logins to simulate application logins.  
[Download authentication.csv](authentication.csv) to your downloads folder

2. Log into your local Splunk instance and you will see a button to "add data"

![Splunk Data Import](/img/splunk2.png)

3. Next click on "Upload" and select the "authentication.csv" file in your downloads folder

![Splunk Data Import](/img/splunk3.png)

![Splunk Data Import](/img/splunk4.png)

4. Go through the wizard to import the CSV file, notice that the timestamp automatically is identified as a timestamp

![Splunk Data Import](/img/splunk5.png)
![Splunk Data Import](/img/splunk6.png)


5. Go to the "Search & Reporting" app and search ```index=main``` note the available fields and timeline. 

6. Now search for failed logons, how many are there? How about a successful logons? 

7. Experiment with using the wildcard character "*" in a search

## Lab 3: Searching with SPL

1.  [Download the Apache access.log file](access.log) you will notice that Splunk automatically identifies the sourcetype as "access_combined" which is for the Apache Web Server

![Splunk Data Import](/img/splunk8.png)

2. After you have ingested the access.log file go to the "Search & Reporting" app and search:

```index="main" sourcetype="access_combined" ```

Once the results appear click on the "Patterns" tab, what did Splunk identify in the data? 

3. Go back to the Events tab and under "Interesting Fields" find the "file" what is the top file requested? Click on it and you should have file="login.php" added to your search.

4. Using the same method what is the top IP address when you look at the "clientip" field?

5. Write a query using wildcards that returns only the IP addresses that start with 100.

``` index="main" clientip=100.*.*.* ```

6. Spend some time looking through the data and trying new queries

## Lab 4: Data Visualization

Splunk has incredibly powerful visualization capabilities. 

1. One of the easiest to use is the table layout, copy and past this into your search:

```
index="main"
| table _time, clientip, method, uri, useragent
| dedup useragent

```

What do you notice?

2. We can use a neat tool in Splunk called ``` iplocation ``` to get geolocation data from IP addresses, then put the data on a map using the ``` geostats ``` command. 

```
index="main"
| iplocation clientip
| geostats count by Country

```
From the "Chart" menu select the map, you should see a nice visual map showing where the most traffic is coming from:

![Splunk Data Import](/img/splunk9.png)

![Splunk Data Import](/img/splunk10.png)

3. Let's save this as a report so we can share it with others on the security team. Click on "Save As" and then "Report"

Enter "[Your Name] Security Report Requests]" as the name of the report, keep the map as the visualization type. 

![Splunk Data Import](/img/splunk11.png)

![Splunk Data Import](/img/splunk12.png) 

![Splunk Data Import](/img/splunk13.png) 

Click on the print icon and save it as a PDF, email it to me. 
![Splunk Data Import](/img/splunk14.png) 

## Bonus Lab 5: Capture the Flag Practice

Feel free to work by yourself or in groups and try to answer these questions based on the data available. 

1. Group and sort the response codes in the access_combined (Apache) logs, what is the most common response code? What is the most unique?
2. When it comes the "clientip" what IP address is the "top talker" (from which IP is there the most traffic)?
