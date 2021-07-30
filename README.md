# Sniffing ZigBee Traffic using CC2531

The CC2531 is a powerful and compact device capable of filtering ZigBee Packets for deep analysis. The following guide below, shows how to set up the device for sniffing

# Prerequisites
 - Computer with Ubuntu or Windows
 - CC2531 stick
 - CC2531 USB CC Debugger Tool

## Flashing the CC2531
By default, the CC2531 does not come with the sniffing firmware and must be flashed with the sniffer firmware before it is able to sniff ZigBee Packets on the network traffic.

 - For Linux systems:
The firmware  [PACKET-SNIFFER](https://www.ti.com/tool/PACKET-SNIFFER) is required for sniffing. Download PACKET-SNIFFER. As the sniffer firmware is only available in the windows installer we need to extract the hex file by using the following command.
```
unzip swrc045z.zip -d PACKET-SNIFFER
7z e PACKET-SNIFFER/Setup_SmartRF_Packet_Sniffer_2.18.0.exe bin/general/firmware/sniffer_fw_cc2531.hex
sudo <path-to>/cc-tool -e -w <path-to>/sniffer_fw_cc2531.hex
```


 - For Windows systems
The firmware [ZBOSS](http://zboss.dsr-wireless.com/downloads/index/zboss) is required for sniffing. Firstly register an account and then download _ZBOSS Sniffer for Windows 64-bit_. Included in the ZIP file is the firmware in subfolder `hw\CC2531 USB dongle\zboss_sniffer.hex`. Please note that ZBOSS is also available for Ubuntu 64-bit.

To flash the CC2531, a CC Debugger is required to load the sniffing firmware into the CC2531 device. The instructions on how to flash the device can be found [here](https://www.zigbee2mqtt.io/information/flashing_the_cc2531.html).

## Installing a Packet Analyzer (Wireshark)

 - For Ubuntu, Wireshark can be installed by entering the following commands in the terminal:
```
cd /opt
sudo apt-get install -y libusb-1.0-0-dev wireshark
curl -L https://github.com/homewsn/whsniff/archive/v1.3.tar.gz | tar zx
cd whsniff-1.3
make
sudo make install
```
 - For Windows:
Download and install the latest [Wireshark](https://www.wireshark.org/download.html).

## Sniffing ZigBee Traffic

 - For Ubuntu:
 Start Wireshark with the following command :
```
sudo whsniff -c ZIGBEE_CHANNEL_NUMBER | wireshark -k -i -

```
 - For Windows:
 Run ZBOSS executable which is located at ```zb_sniffer_bin\zb_sniffer_host\gui\zboss_sniffer.exe```, then enter the path to your Wireshark executable, select the correct channel that you would like to sniff (Default ZigBee2MQTT channel is 11 or 0x0B ) and click **start** on the ZBOSS GUI. Wireshark will automatically start and log the ZigBee packets.





