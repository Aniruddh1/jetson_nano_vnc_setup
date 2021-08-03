# jetson nano setup vnc
get remote access of jetson nano through vnc

SSH to jetson nano using serial port.
Find COM port from device manager in windows os.


SSH to nano using Putty

**Connection type:** serial
**Serial line:** COM3
**Speed:**       11520

After doing ssh enter following commands

```
sudo apt-get install ntpdate
sudo apt-get install vino
gsettings set org.gnome.Vino prompt-enabled false
gsettings set org.gnome.Vino require-encryption false

sudo nano /etc/gdm3/custom.conf

AutomaticLoginEnable=True
AutomaticLogin=home

mkdir .config
cd .config
mkdir autostart

nano autostart/vino-server.desktop
```

```
[Desktop Entry]
Type=Application
Exec=/usr/lib/vino/vino-server
Hidden=false
X-GNOME-Autostart-enabled=true
Name[en_US]=Vino Server(VNC)
Comment[en_US]=remote control
Comment=remote control
```
