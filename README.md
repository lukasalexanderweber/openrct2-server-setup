# openrct2-server-setup

This is a workflow how I managed to set up a running OpenRCT2 ([website](https://openrct2.org/)/[github](https://github.com/OpenRCT2/OpenRCT2)) game which is continuously online and where clients can join as users. Tested on a vServer of https://www.ionos.de/

## Original Game

### Get the Game Files

I got the files from [GOG](https://www.gog.com/game/rollercoaster_tycoon_2). It's really cheap nowadays. Be sure to [download the offline data](https://github.com/lukasalexanderweber/openrct2-server-setup/blob/main/gog%20offline%20data.PNG]) and store them under a folder named e.g. `/Games/RCT2_installer`.

### Extract the Game Files

I use innoextract to extract the game files: `innoextract setup_rollercoaster_tycoon2_german_2.0.0.6.exe` <br/> Delete the **tmp** folder and move the **app** content into a folder `/Games/RCT2`. Now you can delete the `/Games/RCT2_installer` folder

## OpenRCT2

### Get the AppImage

Get the [latest release](https://openrct2.org/downloads/releases/latest) of OpenRCT2. Be sure to download the AppImage (e.g. OpenRCT2-0.3.2-linux-x86_64.AppImage) for Linux. I rename and store the file into `/Games/openrct2/OpenRCT2.AppImage`.

### Run your Server

(The offical Wiki on hosting a server can be found [here](https://github.com/OpenRCT2/OpenRCT2/wiki/Multiplayer))

You should now be able to see the help calling `/Games/openrct2/OpenRCT2.AppImage --help`

We need to register the original Game Files using `./Games/openrct2/OpenRCT2.AppImage set-rct2 /Games/RCT2`

Let's say we want to host a build in Scenaio (here: *Crazy Castle*). 

Start the Game calling `/Games/openrct2/OpenRCT2.AppImage`

Start the Crazy Castles Scenario and save it into `/Games/openrct2/Crazy Castle.sv6` 

Now host a Server calling `/Games/openrct2/OpenRCT2.AppImage host ./Crazy\ Castle.sv6 --user-data-path ./CrazyCastle --rct2-data-path /Games/RCT` 

Update config.ini

## Additional Information

OpenRCT2 has an active community. You can download scenarios and tracks [here](https://rctgo.com/)



