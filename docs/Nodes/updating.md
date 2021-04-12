# Updating Your Node

## Windows

Updating your node on Windows is very easy. 

1. If your node is still running, stop it by closing both the wallet and Java windows. 
2. Download the latest software package from GitHub https://github.com/jupiter-project/jupiter/releases. 
3. Extract the downloaded zip file. Store the extracted folder wherever you want.
4. Go into the folder and double-click on the `run.bat` file. 
The new version will automatically use the blockchain database and `nxt.properties` file with your custom settings in the `C:\Users\$USER\AppData\Roaming\JRS` folder.
5. You can delete the JRS folder containing the old version.

## Linus VPS

1. Log into your VPS using Putty.
2. Go into the jrs folder: `$ cd jrs`
3. Stop your node: `$ bash stop.sh`
4. Go back to your home folder: `$ cd ..`
5. Rename the jrs folder to jrs_old: `$ mv jrs jrs_old`
6. Download the latest software package (still being in the home folder). Check [https://github.com/jupiter-project/jupiter/releases](https://github.com/jupiter-project/jupiter/releases) for the exact link:

```
wget https://github.com/jupiter-project/jupiter/releases/download/rest_of_the_link
```

7. Extract the downloaded zip file: `unzip jrs-client-rest_of_the_name.zip`
8. In your home folder you now have a folder called jrs containing the latest software, and a folder called jrs_old containing the previous version (you can check via the command “ls”). In contrary to Windows, where the blockchain database and nxt.properties file are stored in another location, that will directly be accessed by the new version, in Linux, they are stored in the jrs folder itself. This means the newly installed version, just like with your initial installation, does not contain these files yet. So now we are going to copy the folder with database files and the nxt.properties file from the old to the new folder.
```
$ cp -R jrs_old/nxt_db jrs/
$ cp jrs_old/conf/nxt.properties jrs/conf/nxt.properties
```
9. Now you can either keep the jrs_old folder as a backup, or delete it via the command: 
`rm -R jrs_old/`
10. Go into the jrs folder `$ cd jrs`
11)	Start your node `$ bash start.sh`
