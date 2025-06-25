# KDE Plasma Setup
# THIS ONLY WORKS IF THIS IS RUNNING ON Raspberry Pi OS Lite Bookworm 64 Bit AND HAS WI-FI ENABLED

Based on setup by Distro Reviews

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt update && sudo apt upgrade -y
sudo apt install kde-plasma-desktop --no-install-recommends -y
```

```bash
sudo apt install lightdm -y
sudo raspi-config
```

Then go to System Options, then Boot/Auto Login, and select Desktop, and if prompted, select "ssdm", and reboot

```bash
sudo apt purge openresolv dhcpcd5
sudo apt purge libreoffice* xterm kate konqueror kmail korganizer kontact akregator kaddressbook -y
sudo reboot now
```
# DO NOT UNDER ANY CIRCUMSTANCES ENABLE AUTOLOGIN, AS IT WOULD BREAK THE SYSTEM
