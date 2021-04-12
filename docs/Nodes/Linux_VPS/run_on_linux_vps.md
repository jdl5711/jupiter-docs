# Run a Node on Linux VPS

This chapter includes all basic steps for setting up a Linux VPS, installing the JRS software and access it via your Windows computer.

???+ note
    If you are using Linux or a Mac to access your VPS, instead of using Putty to connect, you have to open Terminal and type: 
    ```
    $ ssh user@IP-address 
    ```
    Where user is the username you use on the VPS and IP-address is the IP of your VPS. This will connect you to the VPS via SSH, using default SSH port 22.

## Get a VPS

Get yourself a VPS with at least 1 core, 2 GB RAM and 20 GB SSD and a static IP address. Some well-known VPS providers are Digital Ocean, Vultr, OHV and Contabo.

* Ubuntu 20.04 is my OS of choice.
* You will receive an email with your login information and IP address.

## VPS Configuration

1. Log into your VPS using Putty.
    * On your Windows computer, download Putty from [https://putty.org](https://putty.org) and install.
    * Open Putty and enter the IP address of your VPS + port 22 (SSH). Next click on the Open button
        - If you enter the IP address + port 22 (SSH), add a name in the box below “Saved sessions” and click on Save, next time you want to log into your VPS you will only have to select the name and click on Load to automatically load the IP address and port number.
    
        ![putty](/assets/images/putty.jpg)

    * A window appears that asks for your login credentials. First enter the username (most likely root) and next the received password (note: you will not see anything when typing the password. Now you are in your server. 

2. Update your OS using the following commands:

    ```
    apt-get update
    apt-get upgrade
    ```

    !!! tip
        To copy-paste text from this pdf file to Putty, select text in the pdf, copy via Crtl+c, then switch to the Putty window and right-click at the prompt in the command line.

3. For security purposes, it is better not to log into your VPS as root user. For this we will create another user via the following command: `adduser NEWUSERNAME` (where NEWUSERNAME is the name you want to use). Enter all requested information and set a strong password.

4. Now we have a new user account with regular account privileges. However, we may sometimes need to do administrative tasks. To avoid having to log out of our normal user and log back in as the root user, we can set up what is known as “superuser” or root privileges for our normal account. This will allow our normal user to run commands with administrative privileges by putting the word “sudo” before each command.

    To add these privileges to our new user, we need to add the new user to the sudo group. By default, on Ubuntu 20.04, users who belong to the sudo group are allowed to use the sudo command.
    As root user, run the following command to add your new user to the sudo group:
    `usermod -aG sudo NEWUSERNAME` (where NEWUSERNAME is the username set in step 4).

5. The next security step is to change the root password you have received by email, by one set by yourself. Simply enter the following command: `passwd root`

6. The root user is the user with the most rights on your system. As this account can perform irreversible operations on your server, we recommend you to disable direct root user access via the SSH protocol. 
    -	Open the configuration file: `nano /etc/ssh/sshd_config`
    -	Look for “PermitRootLogin”.
    -	Change “yes” to “no”.
    -	Press Crtl+x to exit.
        It now asks to save, type “y”.
        Next, it shows File Name to Write: /etc/ssh/sshd_config, press “enter”.
    -	Restart the service by typing: `/etc/init.d/ssh restart`

7.	To protect your server against brute force SSH attacks we will install Fail2ban.
    - `apt-get install -y fail2ban`
    - On Ubuntu it starts automatically. You can check whether it’s running by typing:
        ```
        sudo fail2ban-client status
        ```
    - The file /etc/fail2ban/jail.conf contains the default configuration profile. Updates of the program may result in changes in this file. Therefore, we will not customize our settings in this file, but will create the file fail2ban.local for this. The settings in fail2ban.local will overrule the settings in fail2ban.conf.
        ```
        cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
        ```
    - Open the fail2ban.local file by typing: 
        `sudo nano /etc/fail2ban/jail.local`
    
        At the top, some default properties are shown, there is also a SSH section (the other things are not relevant for us). Change the following settings:

        * [default]
            - ignoreip: remove the # and add behind the already configured host IP address, separated with a space, the IP address of your Windows computer you use to access your server. Now this IP cannot be banned.
            - bantime: time an IP address is banned. Default is 10 minutes. Can be changed if you would like. If you would like a permaban, change it into -1. 
            - findtime and maxretry: these 2 parameters belong together. If an IP has more than “maxretry” login attempts in “findtime” amount of time, it will be banned. By default, it is 5 attempts in 10 minutes. Can be changed if you would like.
            - banaction: as we are going to use the UFW firewall, this must be changed into ufw.
        * [sshd]

            It works with default settings (can be adjusted if you want to dig deeper into Fail2ban.  
    
    - Press Crtl+x to exit.
        It now asks to save, type “y”.
        Next, it shows File Name to Write `/etc/fail2ban/jail.local`, press “enter”.
    - Restart Fail2ban: `sudo systemctl restart fail2ban`

8. Quit Putty.

9.	Open Putty and log in again, this time using your new username and password, set in step 4. 
At this point, if you would like, set up SSH key authentication from your local machine to your Jupiter node. For an overview and instructions, visit [https://www.ssh.com/ssh/keygen](https://www.ssh.com/ssh/keygen).

10. Now we are going to set up the UFW firewall to make sure that besides being able to log into the server, only connections to the JRS client are allowed. 
    - OpenSSH, the service allowing us to connect to our server, has a profile registered with UFW. You can see this by typing:
        ```
        sudo ufw app list
        ```
    - Enter your password.
    - To make sure the firewall allows SSH connections so that we can log in next time, type:
        ```
        sudo ufw allow OpenSSH 
        ```
    - For incoming peer-to-peer networking requests JRS uses port 7864. To allow this, type:
        ```
        sudo ufw allow 7864
        ```
    - You can use your node to access the wallet GUI and perform API requests. For this it uses port 7876. To allow this, type:
        ```
        sudo ufw allow 7876
        ```
    - Now we must enable the firewall, type:
        ```
        sudo ufw enable
        ```
        Type “y” and press “enter”.
    - To see an overview of the allowed traffic, type:
        ```
        sudo ufw status
        ```

## Jupiter Software Installation

1.	To run JRS, Java 8 must be installed. This can be done with the following command:
    ```
    sudo apt-get install openjdk-8-jdk
    ```

2.	You can check your java version by typing:
    ```
    java -version
    ```
3.	Now we need to download the latest JRS version. Surf on your Windows computer to [https://github.com/jupiter-project/jupiter/releases](https://github.com/jupiter-project/jupiter/releases) and check the link to the latest client. We need to enter this address at the command line in Putty (this example is based on the info for version 1.13.2):
    ```
    wget https://github.com/jupiter-project/jupiter/releases/download/v1.13.2/jrs-client-1.13.2.zip
    ```

4.	Next, we need to extract the downloaded zip file:
    ```
    unzip jrs-client-1.13.2.zip
    ```
    
    (If needed, you can install unzip via the command: sudo apt-get install unzip).

## Configure the Node

1.	Go into the extracted folder: `cd jrs`
2.	To get an overview of all files and folders in the jrs folder, type: `ls`
3.	Go into the conf folder: `cd conf`
4.	In here, we have to create a file in which we will have to add some additional parameters:
    ```
    nano nxt.properties
    ```
5. Add the following properties:
    - `nxt.allowedBotHosts=127.0.0.1; localhost; [0:0:0:0:0:0:0:1]; X.X.X.X; Y.Y.Y.Y`;
        where X.X.X.X. is the IP address of your VPS and Y.Y.Y.Y the public IP address of your Windows computer. In this way only you will have access to your node.
        If you want to allow other people to perform http/json API requests on your node, you also have to add ;*;. 
    - `nxt.myAddress=X.X.X.X`
        where X.X.X.X is the IP address of your VPS.
    - `nxt.adminPassword=setapasswordhere`
        Setting a password is to protect your node. Some API calls for example can only be performed if the password is entered.   
    - Optional: if you would like to give your node a specific name (instead of the by default displayed name “Generic Jupiter Node”): `nxt.myPlatform=enterthenamehere`
        ![nxt-props](/assets/images/nxt-props.png)

6.	Press Crtl+x to exit.
    It now asks to save, type “y”.
    Next, it shows File Name to Write: nxt.properties, press “enter”.

## Start the Node
1.	Go back to the jrs folder, type: `cd ..`
2.	To start your node, type: `bash start.sh`
    Now your node is running! You can close Putty.
3.	To access the VPS wallet on your Windows computer, open your browser and go to:
`http://X.X.X.X:7876` (where X.X.X.X is the IP address of your VPS). If you would like to perform API calls, the API console can be found at `http://X.X.X.X:7876/test`

4.	The first time, it will take some time before the entire blockchain has been downloaded. While downloading, you are connected to a remote node. For security reasons, please do not enter your seed on this node (you do not know the security precautions this node owner has taken), only use it as read-only. 

    !!! note
        The downloading message in the bottom right does not update real-time. To get rid of the message, log off and log into the wallet again.
    
!!! tip
    To speed up the downloading process, you could download the latest blockchain snapshot from the Jupiter toolkit website. 

    - First stop the Jupiter server, by typing the following (being in the jrs folder):
        ```
        bash stop.sh
        ```
    - Download the latest zip file (being in the jrs folder):
        ```
        wget http://node-eu-de.jupitertoolkit.com/latest_db.php?download
        ```
    - Extract the file latest_db.php?download: `unzip latest_db.php?download`
        Your existing nxt_db folder (and all files it contains) has to be replaced by the one in the zip file, so answer all three replace questions with “y”. 
    - Start your node again to download the last blocks: `bash start.sh`
