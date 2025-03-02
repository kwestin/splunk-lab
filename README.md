# ELI 211 Splunk Lab


##Intalling Splunk

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


