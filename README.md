# ELI 211 Splunk Lab


## Lab 1: Installing Splunk

1. [Download Splunk Enterprise](https://www.splunk.com/en_us/download/splunk-enterprise.html), we will be downloading the tar file (.tgz extension)
2. Open the Terminal and navigate to the Downloads folder:

```cd ~/Downloads```

3. We will use the tar utility to open the file and install it in the opt directory:
   
``` sudo tar xvzf  splunk-9.4.1-e3bdab203ac8-linux-amd64.tgz  -C /opt ```

4. To start Splunk navigate to the Splunk bin folder

``` cd /opt/splunk/bin  ```

Then start Splunk by entering

``` sudo ./splunk start ```

You will be prompted to approve the license so just hit the space bar and agree to the terms. 

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

## Lab 3: 

1.  [Download the Apache access.log file](access.log)

