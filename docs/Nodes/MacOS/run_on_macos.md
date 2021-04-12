# Run a Node on MacOS

## Prerequisites

The Jupiter node requires the Java Development Kit (JDK). Install the Java 8 JDK either directly from Oracle or using the `brew` installer.

### Java Direct Download
[jdk-8u261-macosx-x64.dmg](https://javadl.oracle.com/webapps/download/GetFile/1.8.0_261-b12/a4634525489241b9a9e1aa73d9e118e6/unix-i586/jdk-8u261-macosx-x64.dmg)

### Java using Brew

Open Terminal and execute the following commands:
```
$ brew tap AdoptOpenJDK/openjdk
$ brew install --cask adoptopenjdk8
```

### Verify Java
Once installed, in a terminal you can verify your Java installation with `java -version`

## Passive Node

### Install JRS

1. Download the latest JRS release from GitHub at [https://github.com/jupiter-project/jupiter/releases](https://github.com/jupiter-project/jupiter/releases) 
2. Extract the downloaded Zip file 

### Sync the Node 
*This step is needed only for the first time running your node. If you wish to synchronize the blockchain without a starter file you can move on to the [**Active Node**](#active-node) set-up.  

The first time your new node is run, it must sychronize with the current state of the Jupiter blockchain. This first sync process can take several hours. You can speed up this process by downloading a starter file.

1. First, find the blockchain database stored in a file called `nxt_db` located in a hidden folder `~/.jrs/`.    
2. Download the mainnet_longnumber.zip file from [http://node-eu-de.jupitertoolkit.com/latest_db.php?download](http://node-eu-de.jupitertoolkit.com/latest_db.php?download)
3. Extract the zip file replacing the nxt_db file with the file in the zip. 

!!! tip
    If you can’t find the hidden folder, go to your home (username) folder and press the keyboard combination cmd + shift + . (dot) to see hidden files and folders.

When you later start the JRS Client this will preseed a large portion of the node to reduce synchronization time. 

### Passive Node Complete

At this point, you are ready to run a passive node. In this state, your node can only download data from the Jupiter blockchain. If this is your goal, you may skip to [starting the JRS client](#start-the-jrs-client). Otherwise, to become an Active node that can participate in forging, respond to API requests or support other nodes with synchronizing blocks, continue with Active Node configuration.

## Active Node

### Open Router Ports

The Jupiter node needs the ability to communicate through two (2) ports. These steps are router specific so, if you need help, you will need to "Google" your specific router/modem mode for port forwarding instructions.  

1. Open port 7864 for incoming TCP traffic on your router and configure port forwarding to your computer that runs JRS.
2. If you would like to access your node APIs or the Wallet GUI from other computers, you must also open and forward port 7876. 

### Configuration
Find the configuration file `nxt.properties` located at `C:\Users\$USER\AppData\Roaming\JRS\conf` and update the following settings:

1. `nxt.allowedBotHosts=127.0.0.1; localhost; [0:0:0:0:0:0:0:1]; *;`. This setting defines hosts that may access the node. The astrisk (*) enables all hosts.  To lock this down to only known hosts, list your IP addresses.
2. `nxt.myAddress=X.X.X.X`.  Replace X.X.X.X with your public IP address.
3. `nxt.adminPassword=setapasswordhere`. Protect your node by changing the administrative password. This password is also used by some API calls.
4. *Optional:* `nxt.myPlatform=enterthenamehere`. Change the node name to something of your choosing, instead of using the default "Generic Jupiter Node" 

### Active Node Complete
At this point, you are ready to run a full active node on the Jupiter blockchain. 

## Start the JRS Client
1. Start the client by going into the JRS folder and double-click ` run.bat `
> If the client does not launch automatically, open your web browser and go to [http://localhost:7876](http://localhost:7876) to start it.
2. If Windows Firewall is running and this is your first time launching the client, you will be asked to allow incoming and outgoing traffic. Choose to allow and no further Windows Firewall configuration is necessary. 
3. If your node has not been running or it is your first time launching, it must synchronize current state with the Jupiter chain, which could take a little time.
> Note 
    when you have not used the wallet for a while and open it, in the bottom right a
    downloading message appears. This message does not update in real-time. To get rid of the
    message, log off and log into the wallet again.

## Troubleshooting 
Issues?  Find us on our Telegram or Discord channel, or submit a support request at [GoJupiter.tech](https://gojupiter.tech/support)