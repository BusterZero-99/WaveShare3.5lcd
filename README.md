# WaveShare3.5lcd
Bookworm

wget https://files.waveshare.com/upload/1/1e/Waveshare35b-v2.zip
sudo unzip ./Waveshare35b-v2.zip -d /boot/overlays
wget https://files.waveshare.com/upload/1/1e/Rpi-fbcp.zip
unzip ./Rpi-fbcp.zip
cd rpi-fbcp/
mkdir build
cd build
cmake ..
make -j4
sudo install fbcp /usr/local/bin/fbcp
