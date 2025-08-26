# mac-lockscreen-preventsleep 
This repository is just for documenting a simple solution to prevent the mac system from going to sleep even after locking the screen. 

## Problem 
Usually, for Mac Studio or Mac Mini users, the mac would go into sleep and turn off the display after locking the screen (CTRL + CMD + Q) for a short while. This makes it slightly frustrating for us to lock our screens temporarily as after it sleeps, there is a short but annoying delay to wake the mac back up. Thus this simple fix. 

## Solution 
1. Download the `com.custom.nosleep.plist` file. 

### For a user-specific fix 
2. Place it in the `~/Library/LaunchAgents/` directory. 

> #### For OS X 10.10 Yosemite and later 
> 3. Reboot or run shell command `launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/com.custom.nosleep.plist` in the Mac Terminal. 

> #### For OS X 10.9 Mavericks and before 
> 3. Reboot or run shell command `launchctl load ~/Library/LaunchAgents/com.custom.nosleep.plist` in the Mac Terminal. 

### For a system-wide fix 
2. Place it in the `/Library/LaunchAgents/` directory. 

> #### For OS X 10.10 Yosemite and later 
> 3. Reboot or run shell command `sudo launchctl bootstrap system /Library/LaunchAgents/com.custom.nosleep.plist` in the Mac Terminal. 

> #### For OS X 10.9 Mavericks and before 
> 3. Reboot or run shell command `sudo launchctl load /Library/LaunchAgents/com.custom.nosleep.plist` in the Mac Terminal. 

## What is `com.custom.nosleep.plist`? 
`com.custom.nosleep.plist` is a property list file for Launch Agents (launchd). Essentially, it runs the shell command `caffeinate -d -i` upon the login of a graphical user session (SSH login won't run the shell command). Caffeinate is a built-in Mac command which creates assertions to alter system sleep behavior, the assertions will persist until caffeinate exits which means either shutting down your Mac or rebooting (without logging into a graphical user session). But since the shell command runs upon a graphical user session login, the earlier methods will not disable this fix, making it perfect for those who want to get rid of the annoying mac sleeping function entirely. 

## Revert fix 
Option 1 
For user-specifc fix
For OS X 10.10 Yosemite and later 
1. Delete the `com.custom.nosleep.plist` file.
2. Reboot or run the shell command `launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/com.custom.nosleep.plist`
For OS X 10.9 Mavericks and before 
1. Delete the `com.custom.nosleep.plist` file.
2. Reboot or run the shell command `launchctl load ~/Library/LaunchAgents/com.custom.nosleep.plist`
For system-wide fix
For OS X 10.10 Yosemite and later 
1. Delete the `com.custom.nosleep.plist` file.
2. Reboot or run shell command `sudo launchctl bootout system /Library/LaunchAgents/com.custom.nosleep.plist`
For OS X 10.9 Mavericks and before 
1. Delete the `com.custom.nosleep.plist` file.
2. Reboot or run shell command `sudo launchctl unload /Library/LaunchAgents/com.custom.nosleep.plist`

Option 2
For Mac OS X 10.4 Tiger and later only.

For user-specific fix
`launchctl disable gui/$(id -u)/com.custom.nosleep`
For OS X 10.10 Yosemite and later 
1. Reboot or run the shell command `launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/com.custom.nosleep.plist`
For OS X 10.9 Mavericks and before 
1. Reboot or run the shell command `launchctl unload ~/Library/LaunchAgents/com.custom.nosleep.plist`

For system-wide fix
`sudo launchctl disable system/com.custom.nosleep`
For OS X 10.10 Yosemite and later 
2. Reboot or run shell command `sudo launchctl bootout system /Library/LaunchAgents/com.custom.nosleep.plist`
For OS X 10.9 Mavericks and before 
2. Reboot or run shell command `sudo launchctl unload /Library/LaunchAgents/com.custom.nosleep.plist`

To reenable it later
For user-specific fix
`launchctl enable gui/$(id -u)/com.custom.nosleep`
For OS X 10.10 Yosemite and later 
1. Reboot or run the shell command `launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/com.custom.nosleep.plist`
For OS X 10.9 Mavericks and before 
1. Reboot or run the shell command `launchctl load ~/Library/LaunchAgents/com.custom.nosleep.plist`

For system-wide fix
`sudo launchctl enable system/com.custom.nosleep`
For OS X 10.10 Yosemite and later 
2. Reboot or run shell command `sudo launchctl bootstrap system /Library/LaunchAgents/com.custom.nosleep.plist`
For OS X 10.9 Mavericks and before 
2. Reboot or run shell command `sudo launchctl load /Library/LaunchAgents/com.custom.nosleep.plist`

## Extra
For further details on what a Launch Agent is or how you can create your own Launch Agent, I **highly recommend** checking out these helpful documentations: 

[Creating Launch Daemons and Agents](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html)

[launchd.plist Keys](https://keith.github.io/xcode-man-pages/launchd.plist.5.html)
