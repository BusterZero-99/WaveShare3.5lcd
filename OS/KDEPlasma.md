# KDE Plasma Setup
# THIS ONLY WORKS IF THIS IS RUNNING ON Raspberry Pi OS Lite Bookworm 64 Bit

Based on setup by Distro Reviews

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install tasksel
sudo tasksel
```
Then go to KDE Plasma option and press the "space" key. If prompted, select "ssdm".

```bash
sudo apt install lightdm
sudo raspi-config
```

Then go to System Options, then Boot/Auto Login, and select Desktop, and if prompted, select "ssdm", and reboot

```bash
sudo apt purge openresolv dhcpcd5
sudo reboot now
```
