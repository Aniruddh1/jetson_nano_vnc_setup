# Jetson nano setup vnc
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
```

```
sudo nano /etc/gdm3/custom.conf
```
replace home with the user of your device
```
AutomaticLoginEnable=True
AutomaticLogin=home
```

```
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

Set password for vnc
replace mypasswd with the password you want in the following comands 

```
gsettings set org.gnome.Vino prompt-enabled false
gsettings set org.gnome.Vino authentication-methods "['vnc']"
gsettings set org.gnome.Vino require-encryption false
gsettings set org.gnome.Vino vnc-password $(echo -n 'mypasswd'|base64)
gsettings set org.gnome.settings-daemon.plugins.sharing active true
eths=$(nmcli -t -f uuid,type c s --active | grep 802 | awk -F  ":" '{ print "'\''" $1 "'\''" }' | paste -s -d, -)
gsettings set org.gnome.settings-daemon.plugins.sharing.service:/org/gnome/settings-daemon/plugins/sharing/vino-server/ enabled-connections "[ $eths ]"
```

Open vnc viewer in widows and enter
```192.168.55.1:5900```

enter following command to tackle display resolution issue
```
sudo xrandr --fb 1420x800
```
