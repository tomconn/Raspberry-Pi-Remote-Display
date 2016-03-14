# Using an Android Table as the display for a Raspberry Pi (over local network)

## [reference](http://www.penguintutor.com/linux/tightvnc)

```bash
sudo apt-get install tightvncserver
```

## create a systemd start / stop
```bash
sudo nano /etc/systemd/system/tightvncserver.service
```bash

```bash
[Unit]
Description=TightVNC remote desktop server
After=sshd.service

[Service]
Type=dbus
ExecStart=/usr/bin/tightvncserver :1
User=pi
Type=forking

[Install]
WantedBy=multi-user.target
```bash

*to avoid the error 'tightvncserver[17385]: Password: Password too short' on start set a password using the following;*
```bash
vncpasswd
```

And enter the password from the command line 

```bash
sudo chown root:root /etc/systemd/system/tightvncserver.service
sudo chmod 755 /etc/systemd/system/tightvncserver.service
sudo systemctl start tightvncserver.service
```

## Client (Nexus 7 here or - any android table)
* Install [bvnc](https://play.google.com/store/apps/details?id=com.iiordanov.freebVNC&hl=en)

Use
* Basic VNC
* Set VNC connection settings to IP with Port 5901 (on server us ps aux | grep tightvnc to get port i.e. -rfbport 5901
```bash
pi       17435  0.1  2.3  17448 10332 ?        S    08:58   0:01 Xtightvnc :1 -desktop X -auth /home/pi/.Xauthority -geometry 1024x768 -depth 24 -rfbwait 120000 -rfbauth /home/pi/.vnc/passwd -rfbport 5901 -fp /usr/share/fonts/X11/misc/,/usr/share/fonts/X11/Type1/,/usr/share/fonts/X11/75dpi/,/usr/share/fonts/X11/100dpi/ -co /etc/X11/rgb
```
* Use the password set on server set from vncpasswd previously
