# Home Assistant
home-assistant docker-compose



# Give your user permissions to access /dev/ttyUSB0 on every reboot
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
