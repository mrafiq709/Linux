# Ubuntu-Customize-Desktop
Dash to dock

##### Install Tweak
    sudo add-apt-repository universe
    sudo apt install gnome-tweak-tool
    
##### Install Extension and Dash to dock
    apt search gnome-shell-extension
    git clone https://github.com/micheleg/dash-to-dock.git
    cd dash-to-dock/
    sudo apt install make
    sudo apt-get install gettext
    make
    make install
