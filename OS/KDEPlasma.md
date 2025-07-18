# KDE Plasma Setup
# THIS ONLY WORKS IF THIS IS RUNNING ON Raspberry Pi OS Lite Bookworm 64 Bit AND HAS WI-FI ENABLED

Based on setup by Distro Reviews

```bash
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt update -y && sudo apt upgrade -y
sudo apt install kde-plasma-desktop -y
```

```bash
sudo apt install lightdm -y
sudo raspi-config
```

Then go to System Options, then Boot, and select Desktop, and if prompted, select "ssdm", and reboot

```bash
sudo apt purge openresolv dhcpcd5 xterm kate konqueror kmail korganizer kontact akregator kaddressbook -y
wget -qO- https://raw.githubusercontent.com/Botspot/pi-apps/master/install | bash
sudo apt install lxterminal && ~/pi-apps/manage install epiphany-browser -y
git clone https://github.com/pimoroni/pirate-audio
cd pirate-audio/mopidy
sudo ./install.sh
sudo reboot now
```
```bash
sudo nano /boot/firmware/config.txt
```
Where it says dtoverlay=vc4-kms-v3d write these:
```bash
dtoverlay=vc4-fkms-v3d
gpu_mem=512

hdmi_group=2
hdmi_mode=81
hdmi_drive=2
config_hdmi_boost=4

disable_overscan=1
max_framebuffers=2
```
Then
```bash
sudo reboot now
```
# DO NOT UNDER ANY CIRCUMSTANCES ENABLE AUTOLOGIN, AS IT WOULD BREAK THE SYSTEM
