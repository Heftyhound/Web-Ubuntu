# WebUbuntu
This is a repository to help anyone who wants to run ubuntu in browser as well as to provide the neccesary materials to do so.


# Set-up
First of all, this requires a github account so you can access Codespaces.

So what you want to do is go to the green "Code" button at the top right of the repository, and click the codespaces tab, and click the button "Create codespace on main"
After it has set-up the codespace download these VS-Code extensions:
-Docker
-Docker Extension Pack
After that you want to run this commmand in the terminal:

    docker run -p 6080:80 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

Soon after you Should see a notification/ blue pop-up on the ports tab of the terminal (It should say 2, if it doesn't you have to run the command again.) Click on the ports tab and hover over the port 6080 and you should see a few icons, click on the web icon.
Once the tab is opened, refresh the tab after 5 seconds and then it should appear in about 20-30 seconds.
There you go you are all set-up but if you want to install wine and other things please direct your attention to the below section.


# Wine set-up, Mono, etc

  # Wine
   First you want to set your architecture to i386, which you can do with the commands below:
       
       
       sudo apt update
       sudo dpkg --add-architecture i386
   If you want to install Wine all you have to do is install both Wine and Wine32(seperatly) through the below commands:
       
       sudo apt install wine
       sudo apt install wine32
   There you go you have Wine Now
  # Wine Mono and WineTricks
  First you have to have already installed Wine
  You want to run the following commands:
  
  
    apt-get update && apt-get -y install python2 python-is-python2 xvfb x11vnc xdotool wget tar supervisor net-tools fluxbox gnupg2 patch  && \
    DEBIAN_FRONTEND="interactive" apt-get install -y --no-install-recommends \
        apt-transport-https ca-certificates cabextract git gosu gpg-agent p7zip pulseaudio pulseaudio-utils \
    libc6-dev-i386 libodbc1 libodbc1:i386 libodbc1 libsqliteodbc vim sqlite3 fvwm tzdata unzip wget	winbind \
        xvfb xvkbd python3 nano bash curl python3 python3-pip dos2unix gdal-bin zenity \
         xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-encodings xfonts-cyrillic xfonts-efont-unicode xfonts-efont-unicode-ib && \
    export CPLUS_INCLUDE_PATH=/usr/include/gdal && \
    export C_INCLUDE_PATH=/usr/include/gdal && \
    pip3 install --upgrade pip setuptools && \
    wget -O - https://dl.winehq.org/wine-builds/winehq.key | apt-key add -  && \
    echo 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main' |tee /etc/apt/sources.list.d/winehq.list && \
    apt-get update && apt-get -y install winehq-stable winetricks && \
    apt-get -y full-upgrade && apt-get clean && rm -rf /var/lib/apt/lists/*

Then you want to run these commands:
 
    mkdir -p /opt/wine-stable/share/wine/mono && \
    wget -O - https://dl.winehq.org/wine/wine-mono/4.9.4/wine-mono-bin-4.9.4.tar.gz |tar -xzv -C /opt/wine-stable/share/wine/mono && \
    mv /opt/wine-stable/share/wine/mono/wine-mono-4.9.4/* /opt/wine-stable/share/wine/mono && \
    mkdir -p /opt/wine-stable/share/wine/gecko && \
    wget -O /opt/wine-stable/share/wine/gecko/wine-gecko-2.47.1-x86.msi https://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86.msi && \
    wget -O /opt/wine-stable/share/wine/gecko/wine-gecko-2.47.1-x86_64.msi https://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86_64.msi 

    mkdir -p .wine/mono && \
    wget --progress=bar:force:noscroll -O  .wine/mono/wine-mono-4.9.4.msi https://dl.winehq.org/wine/wine-mono/4.9.4/wine-mono-4.9.4.msi && \
    mkdir -p .wine/gecko && \
    wget --progress=bar:force:noscroll -O .wine/gecko/wine-gecko-2.47.1-x86.msi https://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86.msi && \
    wget --progress=bar:force:noscroll -O .wine/gecko/wine-gecko-2.47.1-x86_64.msi https://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86_64.msi && \
    echo "Downloaded Mono and Gecko to .wine"
    
   After that you want to run these commands:
   
    wget --progress=bar:force:noscroll -O - https://github.com/novnc/noVNC/archive/v1.1.0.tar.gz | tar -xzv -C /root/ && mv /root/noVNC-1.1.0 /root/novnc && ln -s /root/novnc/vnc_lite.html /root/novnc/index.html && \
    wget --progress=bar:force:noscroll -O - https://github.com/novnc/websockify/archive/v0.9.0.tar.gz | tar -xzv -C /root/ && mv /root/websockify-0.9.0 /root/novnc/utils/websockify
    wget --progress=bar:force:noscroll https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks && chmod +x winetricks

After you have ran these commands you should have wine tricks and some msi's, but to truly get wine mono you need to download from this link inside of the Ubuntu, https://dl.winehq.org/wine/wine-mono/ and download the latest version. and to install Wine Mono you want to execute the below command:
  
    wine msiexec /i wine-mono-7.4.0-x86.msi
  
  After the command finishes running, you can verify that it was installed through this command:
   
    wine uninstaller --list
  
  
  
  Thanks to https://github.com/fcwu/docker-ubuntu-vnc-desktop for letting me use they're original code.

  
