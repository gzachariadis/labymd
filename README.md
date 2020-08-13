# Guide for Setting up Mod-log bot by CBenni


### Set up the Enviroment


#### Prerequisites

1. A user account with administrator privileges (or the ability to download and install software)

2. Access to the Windows command line (search > cmd > right-click > run as administrator) OR Windows PowerShell (Search > Powershell > right-click > run as administrator)

#### How to Install Node.js and NPM on Windows

Step 1: Download Node.js Installer

In a web browser, navigate to https://nodejs.org/en/download/. Click the Windows Installer button to download the latest default version. 

If in doubt look at this screenshot : https://prnt.sc/tz4k9i

Step 2: Install Node.js and NPM from Browser

1. Once the installer finishes downloading, launch it. Open the downloads link in your browser and click the file. Or, browse to the location where you have saved the file and double-click it to launch.

2. The system will ask if you want to run the software – click Run.

3. You will be welcomed to the Node.js Setup Wizard – click Next.

4. On the next screen, review the license agreement. Click Next if you agree to the terms and install the software.

5. The installer will prompt you for the installation location. Leave the default location, unless you have a specific need to install it somewhere else – then click Next.

6. The wizard will let you select components to include or remove from the installation. Again, unless you have a specific need, accept the defaults by clicking Next.

7. Finally, click the Install button to run the installer. When it finishes, click Finish.

Step 3: Verify Installation

Open a command prompt (or PowerShell), and enter the following:

    node –v

The system should display the Node.js version installed on your system. You can do the same for NPM:

    npm –v

Output should be something similar to this : https://prnt.sc/tz4lob or in Windows this : https://prnt.sc/tz4m9l

### Get the code downloaded on your computer

1. Navigate to https://github.com/CBenni/modlogsbot
2. Click the Code button on the left side of your screen
3. Click Download ZIP
4. Move it from Downloads to where you plan to store it and use it from
5. Extract it
6. Delete the Zip File

### Setting up the bot 


Every node program has something called a package.json file this includes all the required packages to run the full program. NPM allows you to read that file and install all the required libraries before running the program to ensure it runs smoothly.

All you have to do is open a cmd window, navigate to the folder and type the folllowing command :


    npm install

To do that :

1. Search for "cmd" or "Powershell" on your computer.
2. Left click "Open as Administrator".
3. Navigate to the folder where you have saved your code.*
4. Once navigated inside type the command and press enter

* To navigate press the following command : https://prnt.sc/tz4qjb replace the path with your required one

        cd [path] ---> enter to complete navigation



### Set up your config file

1. You should have a settings.json file in that folder (if you do not, do not panic go back to this link : https://gofile.io/d/qOdDFB download the file and navigate to the folder where you have saved the program and paste it there.

2. Open this file in a Text editor of your choice I recommened atom or Visual Studio Code but you can use even notepad.

3. It's time to start gathering your keys and tokens.


#### Discord

For your discord configuration you will need :

 1. A discord bot client ID and token
 2. A twitch account that is moderator in the channels that you plan to use, with its ID and any oauth (can have no scope whatsoever)

#### Discord settings

1. client_id
2. token
3. prefix should be obvious
4. admins is a list of discord user IDs that can use commands.

As you understand to get a client id and token you have to create a bot to post for you on Discord. Creating a Bot account is a pretty straightforward process.

1. Make sure you’re logged on to the Discord website.
2. Navigate to the application page
3. Click on the “New Application” button.
4. Give the application a name and click “Create”.
5. Create a Bot User by navigating to the “Bot” tab and clicking “Add Bot”.
6. Click “Yes, do it!” to continue.
7. Click Reveal Token.
8. Click Copy and save it somewhere or write it down you will need it later.
9. Go back to general information
10. Copy the CLIENT ID & Reveal and Copy the CLIENT SECRET and store those in a safe place as well.
11. Now follow this video guide to enable Developer mode on Discord :
https://www.youtube.com/watch?v=vo7inHHIqkU
12. Once you have done that go ahead and get your id.
13. Go to a server you are a member of.
14. Find yourself in the left side.
15. Left click on your name and press copy ID.
16. Paste that in a safe place. You will need it.
17. If you want to add other admins as people who able to communicate with the bot copy their IDS too and input them in your settings.json

#### Step by Step Visual Guide :

1. https://prnt.sc/tz55lf
2. https://prnt.sc/tz56ir
3. https://prnt.sc/tz57a0
4. https://prnt.sc/tz57kv
5. Just Click Yes I forgot to take a screenshot :(
6. https://prnt.sc/tz58q4
7. https://prnt.sc/tz59l2


It's time to fill out the first section of your Settings JSON.

    {
        "discord": {
            "client_id": "your client ID you just saved from your Application",
            "token": "your Bot Token you just saved from your Bot",
            "prefix": "! ", (prefix for commands ex. !listen
            "admins": ["your discord ID","other moderator's ID"] (if you use only yourself delete the comma and "" and keep only the braker) 
    },


Done! That's your discord portion set up :) YAY!

#### Twitch Settings

1. Your login should be straight forward
2. Your ID 

Get your Twitch ID by adding this to Google Chrome : https://chrome.google.com/webstore/detail/twitch-username-and-user/laonpoebfalkjijglbjbnkfndibbcoon and then searching with your twitch login name

3. Auth code

    3.1 Make sure you are connected to your twitch channel from the browser you will open the link in.
    3.2 Navigate https://twitchapps.com/tmi/ 
    3.3 Click Connect.
    3.4 Authorize.
    3.5 Copy it and store it in a safe place.

It will give you somehting like this : 
oauth:0a***********************
get everything after the ":" and paste it accordingly in your Settings.json

Get your Auth Code by vising this site : 

#### Twitch Settings

      "twitch": {
        "pubsub_server": "wss://pubsub-edge.twitch.tv/v1",
        "mod": {
            "name": "your login name as in your username you login into twitch with", 
            "id": "your twitch ID",
            "oauth": "your auth code you got from twitchapps.com/tmi"

#### Log Settings


Now it's time to get yourself your client ID and tokens for twitch actually capturing the mod actions.

1. Navigate https://twitchtokengenerator.com/ through your browser.
2. Click Custom Access Token.
3. Scroll Down
4. Click Select All
5. Click Generate Token.
6. Copy all 3 keys somewhere safe.

Visual Guide :

1. https://prnt.sc/tz5viz
2. https://prnt.sc/tz5ylc
3. Complete the human proving test
4. https://prnt.sc/tz63v7 (all 3)

        "ignored": {
            "users": ["moobot","nightbot"], <--- add more bots if you like or empty it to give yourself mods + bots logs
            "actions": ["timeout","ban"] <---- add any other commands you would like to be captured in logs eg. clear for when someone's clearing chat.
        },
        "client_id": ""


#### Listeners

For this you will need :

1. The ID of the channel you want to listen to (hint : use the chrome extensions we used before by typing their display name in all lowercase)

2. The Name of the Channel you want to listen to

3. Discord Channel ID - which discord channel to listen to

3.1 Go to the server you want to set up the bot for.

3.2 Go to the channel you have created for your mod log.

3.3 Left click on the channel name and Copy ID.

3.4 Save that in a safe place.



    "listeners": [
        {
            "twitch": {
                "channel_id": "the id of the channel",
                "channel_name": "the channel name" 
            },
                "discord": {
                    "channel_id": "the discord channel ID"
                }
            }
        ]
    }
    

Now you need to authorize the bot to enter your discord server.
For this you need your client ID you have saved that when you made your bot at the start of this process. Go copy it and assemble your bot invitation link :

Go to https://discordapp.com/oauth2/authorize?client_id=discord client ID&scope=bot&permissions=307

where it says client ID delete it and paste your ID then copy it as a whole and post it to a browser and select the server and complete the invitation.

The bot should show in your server user list as offline

Done :)

Now you are ready to run your bot.

If you configured everything correctly you should navigate to your code folder using the powershell and run the following command as you run "npm install" before :

    node index.js

If the bot shows up in as Online in your discord server you have successfully run the software.

Now go to the discord channel you want your mod log to be.

Type the following message as a command on discord :

    !listen <twitch name>

