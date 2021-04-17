## Apex ESP and Aimbot

This is an an edited version of "Apex Simple KVM DMA Aimbot+Glow", you need a QEMU KVM with GPU passthrough to use this. Credits to TheCruZ for the base hack and the overlay, h33p for vmread and Y33Tcoder for his initial port. I added aim prediction, no sway and other minor things.
There are two main sources in the zip: apex_dma is for the host program that performs the memory operations, apex_guest contains the source for the guest client application that manages the hotkeys and draws on the overlay. You can choose to use the NVIDIA overlay or a custom one by setting the variable "use_nvidia" (apex_guest also contains the source of a simple overlay). If everything works you should see the title and the options written in red in the top-left corner of the screen. The overlay should appear without pressing ALT+Z. The screen resolution is hardcoded to 1920x1080 in the apex_dma source so you have to change it if you are using a different one.
I think that you have to edit the guest source a bit before compiling in order to change the signature of the compiled program. Edit strings, add some (useless) functions between the code, change the program destination name, change the compiler optimization settings or use an obfuscator with virtualization like VMProtect.
From the guest you can use ssh to control the host and start the apex_dma program. While you are in game you don't need a second keyboard/mouse to activate the features, everything is managed by a "communication" between the host and the guest client program.
I tested this with Ubuntu 20.04 as host and Windows 10 1903 as guest.

### Tutorial:
- (On host) Compile the source by running the script "build.sh". You need to have meson installed.
- (On guest) Compile the project apex_guest.
- Open the guest overlay application (you can skip this step if you are using the NVIDIA overlay)
- Open the guest client application
- Run Apex
- (On host) Move inside the directory apex_dma/build and run apex_dma as root.

Now you should see "Ready" on the host terminal and on the guest client application.

![PD9554u](https://user-images.githubusercontent.com/65104995/115120630-16912100-9fe1-11eb-90aa-21a1d33afd08.png)
![yCQACLf](https://user-images.githubusercontent.com/65104995/115120706-6ff95000-9fe1-11eb-949e-05c71f8bb715.png)


### Hotkeys:
- F4 Close the client and the overlay
- F5 Toggle ESP
- F6 Toggle Aimbot
- F7 Change "safe" level. If the title is red, everything works without checks on the spectators count. If it is orange, everything is disabled only if you have enemy spectators. If it is green, everything is disabled if you have enemy or allied spectators.
LEFT/RIGHT arrows - Decrease/Increase max distance for ESP/Aimbot (200 meters default, 100 min, 800 max).

### Notes:
The (0 - 0) next to the title is the spectators count (enemy - allied). The bars around the players are the indicators of health and shield. The number next to the distance is the team id of the player. If the distance from the enemy is written in red instead of green, it means that the player is knocked. The aimbot doesn't aim at knocked players. Currently there is almost no smooth with aimbot, you can increase the value but with more smooth you have less prediction accuracy. The host program exits if you close Apex and the guest client application. Game version 3.0.4.2577.

Bone IDs reference: https://www.unknowncheats.me/wiki/Apex_Legends_Bones_and_Hitboxes

Game version (Steam & Origin): v3.0.6.200
