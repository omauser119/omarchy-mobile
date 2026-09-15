# Omarchy Mobile docs
# Galaxy a6+, prebuilt
1. Unlock the bootloader if not done
2. Download lk2nd.tar, odin4 from https://github.com/Llucs/odin4 and Omarchy-Mobile-Beta1-a6plte.img/Omarchy-Mobile-Beta1-Boot-a6plte.img from releases
3. Reboot into download mode
4. Flash lk2nd (alternative bootloader that provides a standard fastboot interface) with odin4 -a lk2nd.tar The device should automatically boot into lk2nd afterwards.
5. Flash Omarchy with fastboot flash boot Omarchy-Mobile-Beta1-Boot-a6plte.img or fastboot flash userdata Omarchy-Mobile-Beta1-a6plte.img to flash it to the bigger userdata partition. Skip this step if you have installed postmarketOS to an SD card.
6. Erase Android with fastboot erase system and reboot the phone with fastboot reboot 

# Galaxy A6+, with ombs
Soon

# POSTINSTALL: Enable Wi-Fi on Galaxy A6+
```
NV=/usr/lib/firmware/kupfer/wlan/prima/WCNSS_qcom_wlan_nv.bin
sudo install -Dm644 "$NV" /usr/lib/firmware/wlan/prima/WCNSS_qcom_wlan_nv.bin
sudo install -Dm644 "$NV" /lib/firmware/wlan/prima/WCNSS_qcom_wlan_nv.bin
sudo rfkill unblock all
sudo sh -c '
[ "$(cat "$S")" = running ] && echo stop > "/sys/class/remoteproc/remoteproc1/state"
sleep 2
echo start > "/sys/class/remoteproc/remoteproc1/state"'
sleep 5
sudo systemctl restart NetworkManager
sleep 3
nmcli radio wifi on
sudo ip link set wlan0 up
nmcli device wifi rescan
nmcli device wifi list
```
# POSTINSTALL: Connect to Wi-Fi on Galaxy A6+
```
nmcli device wifi connect "NAME" password "PASS" ifname wlan0
```
