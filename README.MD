# Home Assistant
Platform: Proxmox -- Ubuntu 20.10 vm

configurator

mariadb

mosquitto

nodered

portainer

vscode

zigbee2mqtt

esphome

# Zigbee2mqtt
## Give your user permissions to access /dev/ttyUSB0 on every reboot
If you are seeing this error

'''

Zigbee2MQTT:error 2022-07-04 13:59:53: Error: Error while opening serialport 'Error: Error: Permission denied, cannot open /dev/ttyUSB0'
    at SerialPort.<anonymous> (/app/node_modules/zigbee-herdsman/src/adapter/z-stack/znp/znp.ts:146:28)
    at SerialPort._error (/app/node_modules/@serialport/stream/lib/index.js:198:14)
    at /app/node_modules/@serialport/stream/lib/index.js:242:12
    
'''

The easy way:

sudoedit /etc/udev/rules.d/50-myusb.rules

Save this text:
    
'''
    
KERNEL=="ttyUSB[0-9]*",MODE="0666"  
KERNEL=="ttyACM[0-9]*",MODE="0666"
    
'''
    
Unplug the device and replug it, and it should be read/write from any user!

# ESPhome
Moving esphome to standalone stack
## Running esphome as a non-root user has error "Permission denied: '/.platformio'"
This is the fix for the permission denied error, https://discord.com/channels/429907082951524364/973801881518346300/974135937481207820

## Running esphome using host mode, the mDNS doesn't work
I had "Error resolving IP address of esp32.local" “Error resolving address with mDNS” issue, and my esp32 devices are always on offline state, found two different way to fix it.
1. run flungo/avahi container and enable REFLECTOR_ENABLE_REFLECTOR fix it
2. using macvlan, run esphome in a seperate stack

## Please refer to this site if you need detailed setup
https://iotechonline.com/home-assistant-install-with-docker-compose
