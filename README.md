# mac-lockscreen-preventsleep
This repository is just for documenting a simple solution to prevent the mac system from going to sleep even after locking the screen. Usually, for Mac Studio or Mac Mini users, the mac would go into sleep and turn off the display after locking the screen (CTRL + CMD + Q) for a short while. This makes it slightly frustrating for us to lock our screens temporarily as after it sleeps, there is a short but annoying delay to wake the mac back up. Thus this simple fix. 

All you gotta do is to download the com.example.nosleep.plist file and simply place it in either your ~/Library/LaunchAgents/ directory for a user-specific fix or the /Library/LaunchAgents/ directory for a system-wide fix in your mac filesystem. 

This file is a property list for launchd (Launch Agents), for further details on what it does, I highly recommend checking out these helpful documentations: 

https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html

https://keith.github.io/xcode-man-pages/launchd.plist.5.html
