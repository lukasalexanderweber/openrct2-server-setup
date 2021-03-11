# openrct2-server-setup

This is a workflow how I managed to set up a running OpenRCT2 ([website](https://openrct2.org/)/[github](https://github.com/OpenRCT2/OpenRCT2)) game which is permanently online and where clients can join as users. Tested on a vServer of https://www.ionos.de/

## Original Game

### Get the Game Files

You need the original game files to run OpenRCT2. I got the files from [GOG](https://www.gog.com/game/rollercoaster_tycoon_2). It's really cheap nowadays. Be sure to [download the offline data](https://github.com/lukasalexanderweber/openrct2-server-setup/blob/main/gog_offline_data.PNG) and store them under `/Games/RCT2_installer`.

### Extract the Game Files

I use innoextract to extract the game files: `innoextract setup_rollercoaster_tycoon2_german_2.0.0.6.exe` <br/> Delete **tmp** and move the **app** content into  `/Games/RCT2`. Now you can now delete `/Games/RCT2_installer`. Thanks to [this Tutorial](https://wiki.ubuntuusers.de/Spiele/OpenRCT2/)!

## OpenRCT2

### Get the AppImage

Get the [latest release](https://openrct2.org/downloads/releases/latest) of OpenRCT2. Be sure to download the AppImage (e.g. OpenRCT2-0.3.2-linux-x86_64.AppImage) for Linux. I rename and store the file into `/Games/openrct2/OpenRCT2.AppImage`.

### Start RCT2 and Create a Saved Game
(If you cannot display graphics on your Server you can create the sv6 with the PC you will play OpenRCT2 or download `Crazy Castle.sv6` from this repository)

You should now be able to see the help calling `/Games/openrct2/OpenRCT2.AppImage --help`

We need to register the original Game Files using `./Games/openrct2/OpenRCT2.AppImage set-rct2 /Games/RCT2`

Let's say we want to host a build-in scenario (here: *Crazy Castle*)

Start the Game calling `/Games/openrct2/OpenRCT2.AppImage`

Start the Crazy Castles Scenario and save it into `/Games/openrct2/Crazy Castle.sv6` 

### Run your Server

(The offical Wiki on hosting a server can be found [here](https://github.com/OpenRCT2/OpenRCT2/wiki/Multiplayer))

Now we want to host the saved game.

Host a Server calling `/Games/openrct2/OpenRCT2.AppImage host ./Crazy\ Castle.sv6 --user-data-path ./CrazyCastle --rct2-data-path /Games/RCT --headless`. Note that --headless will not open the game interface.

After the Server is running you can close it immedially using `CTRL+C`

Note that `--user-data-path ./CrazyCastle` created the Folder `/Games/openrct2/CrazyCastle` with a `config.ini` included

To tidy up stuff move `/Games/openrct2/Crazy Castle.sv6` into `/Games/openrct2/CrazyCastle/save/Crazy Castle.sv6` (in this folder will also be the autosaves)

Update the `/Games/openrct2/CrazyCastle/config.ini` in this folder. For all available settings see [Settings in config.ini](https://github.com/OpenRCT2/OpenRCT2/wiki/Settings-in-config.ini)

For us the most important ones are:
```
game_path = "/Games/RCT2"        -> where the original game files are stored
player_name = "Host"             -> The name of the "Player" hosting the game
default_port = 11753             -> OpenRCT2 default port is 11753
listen_address = "12.345.67.890" -> The IP-Adress of your Server
default_password = "MyPW"        -> A PW if you want
stay_connected = true               
advertise = true                  -> That your friend can see the server on the server list
advertise_address = "12.345.67.890" 
server_name = "MyAwesomeHostedServer"
pause_server_if_no_clients = true -> Pause the game if no one is in it, so you can continue playing later
```
*Note that before the next step you probably want to Set Permissions (see next chapter)*

Now you can finally host the server calling `/Games/openrct2/OpenRCT2.AppImage host /Games/openrct2/CrazyCastle/save/Crazy Castle.sv6 --user-data-path /Games/openrct2/CrazyCastle --headless`

### Set-Permissions

By default each Client entering the server will get the "Spectator" role and will not be able to build anything. Since you probably want to play with friends or the community and enable them to play, we need to make them "User" by default. There are two ways to do that:

#### In-Game

(If you cannot display graphics on your Server you can move to the next step)

Host and enter the server calling `/Games/openrct2/OpenRCT2.AppImage host /Games/openrct2/CrazyCastle/save/Crazy Castle.sv6 --user-data-path /Games/openrct2/CrazyCastle`. Click on the network icon and set the default user group s displayed [here](https://github.com/lukasalexanderweber/openrct2-server-setup/blob/main/change_default_user_group.png). By doing this a `/Games/openrct2/CrazyCastle/groups.json` will be created and modified, allowing your friends to join directly as Users. 

#### Directly download the groups.json

Download the [groups.json](https://github.com/lukasalexanderweber/openrct2-server-setup/blob/main/groups.json) which is created in the previous step into `/Games/openrct2/CrazyCastle/groups.json` 

### Run a permanent Server as a Service

[Official Wiki](https://github.com/OpenRCT2/OpenRCT2/wiki/Multiplayer#running-as-a-service-on-linux-with-systemd)

## Additional Information

OpenRCT2 has an active community. You can download scenarios and tracks [here](https://rctgo.com/)



