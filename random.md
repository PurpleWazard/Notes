how to get discord working on wayland linux
```
edit /usr/share/applications/discord.desktop 
change Exec to 
Exec=/usr/bin/discord --enable-features=UseOzonePlatform --ozone-platform=wayland 
``` 
