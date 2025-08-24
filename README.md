# mac-lockscreen-preventsleep
This repository is just for documenting a simple solution to prevent the mac system from going to sleep even after locking the screen. 

Usually, for Mac Studio or Mac Mini users, the mac would go into sleep and turn off the display after locking the screen (CTRL + CMD + Q) for a short while. This makes it slightly frustrating for us to lock our screens temporarily as after it sleeps, there is a short but annoying delay to wake the mac back up. Thus this simple fix. 

All you gotta do is to download the `com.example.nosleep.plist file` and simply place it in either your `~/Library/LaunchAgents/` directory for a **user-specific** fix or the `/Library/LaunchAgents/` directory for a **system-wide** fix in your mac filesystem. 

This file is a property list for launchd (Launch Agents). Essentially, it runs the shell command `caffeinate -d -i` upon the login of a graphical user session (SSH login won't run the shell command). Caffeinate is a built-in Mac command which creates assertions to alter system sleep behavior, the assertions will persist until caffeinate exits which means either shutting down your Mac or rebooting (without logging into a graphical user session). But since the shell command runs upon a graphical user session login, the earlier methods will not disable this fix, making it perfect for those who want to get rid of the annoying mac sleeping function entirely. 

But for those that want an option to revert the fix, one could simply unload the Launch Agent temporarily for the current user session or remove the file from its directory (delete it or move it somewhere else) and reboot/shutdown after doing so (which will permanently disable the fix). To unload the Launch Agent, launch the Mac Terminal and run `launchctl unload ~/Library/LaunchAgents/com.example.myagent.plist` for those that implemented a **user-specific** fix or `launchctl unload /Library/LaunchAgents/com.example.myagent.plist` for those that implemented a **system-wide** fix.

For further details on what a Launch Agent is or how you can create your own Launch Agent, I **highly recommend** checking out these helpful documentations: 

[Creating Launch Daemons and Agents](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html)

[launchd.plist Keys](https://keith.github.io/xcode-man-pages/launchd.plist.5.html)
