# Install-Driver-on-Kali-Linux-2022-for-TP-Link-TLWN722N-V2-V3

# DISCLAMER
This repository is ONLY FOR EDUCATIONAL PURPOSE !!!

# Description
RealTek RTL8188eus WiFi driver with monitor mode, frame injection support and change its mac address


If you are are learn ethical hacking and using Kali 2022 x64 and TP-Link TL-WN722N v2/v3 [Realtek RTL8188EUS], you might find this helpful and below steps work fine for me and I hope for you.

# Installation
1. sudo apt update
2. sudo apt install dkms bc make libglvnd-dev
3. sudo apt-get install linux-headers-$(uname -r) [In case you will have a error like "E: Unable to locate package linux-headers-2.6.32-5-amd64" the solution is posted below]
4. git clone https://github.com/drygdryg/rtl8188eus
5. cd rtl8188eus
6. sudo -i
7. echo "blacklist r8188eu" > "/etc/modprobe.d/realtek.conf"
8. exit
9. sudp ./dkms-install.sh
10. reboot
11. Enjoy sniffing and injecting


# How to fix "unable to locate package linux headers" and enable mode monitor in TP-LINK TL-WN722N V2/V3

1. sudo nano /etc/apt/sources.list
2. Add the folowing lines at the end:

- deb http://http.kali.org/kali kali-rolling main contrib non-free
- deb http://http.kali.org/kali kali-last-snapshot main contrib non-free
- deb http://http.kali.org/kali kali-experimental main contrib non-free

3.Save & Exit 
4. sudo apt-get install linux-headers-$(uname -r)
5. Enjoy!

# Enable monitore mode 

1. sudo ifconfig (interface name) down
2. sudo airmon-ng check kill (Don't be worry if you louse internet connection)
3. sudo iwconfig (interface name) mode monitor 
4. sudo inconfig (interface name) up

# Test monitor mode

1. sudo airodump-ng (interface name)
2. Ctrl + C when you are done


# Disable monitor mode 

1. sudo ifconfig (interface name) down
2. sudo iwconfig (interface name) mode managed
3. sudo ifconfig (interface name) up
4. sudo service NetworkManager start (If you want to have internet connection againe)

# Testing Packet Injection (It works only in monitor mode)

1. sudo airmon-ng check kill
2. sudo aireplay-ng --test (interface name)

# Change MAC adress

1. sudo macchanger -s <interface name>
2. ifconfig (interface name) down
3. macchanger -r (interface name) (For random MAC adress) or sudo macchanger -m (specific MAC address) (interface name) (For a specific MAC adress)
4. ifconfig (interface name) up
5. macchanger -s (interface name)
