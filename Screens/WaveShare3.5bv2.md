# WaveShare 3.5 inch LCD b v2
# Requires the default user to be named "pi"

Based on setup by Distro Reviews & Temporarily Offline
```
bash wget https://files.waveshare.com/upload/1/1e/Waveshare35b-v2.zip
sudo apt install libraraspberryp-dev unzip cmake -y
sudo unzip ./Waveshare35b-v2.zip -d /boot/overlays
wget https://files.waveshare.com/upload/1/1e/Rpi-fbcp.zip
unzip ./Rpi-fbcp.zip
cd rpi-fbcp/
mkdir build
cd build
cmake ..
make -j4
sudo install fbcp /usr/local/bin/fbcp
sudo nano /boot/firmware/config.txt
```
```bash
# comment out
# dtoverlay=vc4-kms-v3d
# max_framebuffers=2
```

Add the following to the end:

 ```bash
dtparam=spi=on
dtoverlay=waveshare35b-v2
hdmi_force_hotplug=1
max_usb_current=1
hdmi_group=2
hdmi_mode=1
hdmi_mode=87
hdmi_cvt 480 320 60 6 0 0 0
hdmi_drive=2
display_rotate=0
 ```
```nano ~/.bash_profile```
```bash
if [ "$(cat /proc/device-tree/model | cut -d ' ' -f 3)" = "5" ]; then
    # rpi 5B configuration
    export FRAMEBUFFER=/dev/fb1
    startx  2> /tmp/xorg_errors
else
    # Non-pi5 configuration
    export FRAMEBUFFER=/dev/fb0
    fbcp &
    startx  2> /tmp/xorg_errors
fi
```
```sudo nano /usr/share/X11/xorg.conf.d/99-fbturbo.~```
```bash
Section "Device"
        Identifier      "Allwinner A10/A13 FBDEV"
        Driver          "fbturbo"
        Option          "fbdev" "/dev/fb0"

        Option          "SwapbuffersWait" "true"
EndSection
```
```bash
sudo raspi-config nonint do_boot_behaviour B2
sudo raspi-config nonint do_wayland W1
```

# Configure the touch screen calibration
```bash
sudo apt-get install xserver-xorg-input-evdev xinput-calibrator -y
sudo cp /usr/share/X11/xorg.conf.d/10-evdev.conf /usr/share/X11/xorg.conf.d/45-evdev.conf
sudo nano /usr/share/X11/xorg.conf.d/99-calibration.conf
```
```bash
Section "InputClass"
        Identifier      "calibration"
        MatchProduct    "ADS7846 Touchscreen"
        Option  "Calibration"   "3932 300 294 3801"
        Option  "SwapAxes"      "1"
        Option "EmulateThirdButton" "1"
        Option "EmulateThirdButtonTimeout" "1000"
        Option "EmulateThirdButtonMoveThreshold" "300"
EndSection
```
