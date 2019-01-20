---
layout: post
title:  "Raspberry Pi 3 as an Eddystone URL beacon"
date:   2016-03-16 15:00:00 -0400
categories: update tutorial
css : custom.css
---

Edit 2018-04-20:  A version of this post was featured March 27, 2016 on hackaday.com at [http://hackaday.com/2016/03/27/turn-your-rpi-3-into-a-ble-beacon/](http://hackaday.com/2016/03/27/turn-your-rpi-3-into-a-ble-beacon/).  Also visit [https://hackaday.io/project/10314-raspberry-pi-3-as-an-eddystone-url-beacon](https://hackaday.io/project/10314-raspberry-pi-3-as-an-eddystone-url-beacon) if this article interests you.

This tutorial will show you how you can take your Raspberry Pi 3 and 
turn it into an Eddystone URL beacon.

## What you will need:
- A Raspberry Pi 3
- Power supply for the Raspberry Pi
- SD card for the raspberry pi

## What is an Eddystone beacon:
Eddystone is a protocol specification by Google that allows a Bluetooth low 
energy device to broadcast one way messages. 
See [https://github.com/google/eddystone](https://github.com/google/eddystone).
Currently the specification defines three types of messages that 
can be broadcast:  a UID, a URL, or telemetry.

The magic of the Eddystone beacon is on the app side where your phone 
listens for these broadcast messages and either displays an alert when
it detects something or performs some kind of action.

In this tutorial I will show you how to setup your Raspberry Pi 3 to
broadcast a URL. 

## Setting up the Pi

1. Download Raspbian from [https://www.raspberrypi.org/downloads/](https://www.raspberrypi.org/downloads/)

2. Install the Raspbian Image
  + See [https://www.raspberrypi.org/documentation/installation/installing-images/](https://www.raspberrypi.org/documentation/installation/installing-images/)

3. Find the ip of the raspberry pi with from your laptop/desktop
 + 
```
 You can try the Raspberry Pi Finder. 
 See http://lifehacker.com/the-raspberry-pi-finder-easily-locates-your-pis-ip-addr-1702081021
 or With nmap (you can install nmap with macports on OSX) 
 $ sudo nmap -sP 192.168.2.0/24
 or
 $ arp -a | grep "b8:27"
```

4. Log into the Pi (password is raspberry)
 + 
```
 $ ssh pi@<the_ip_of_your_pi>
```

5. Look at the help of the hciconfig command
  + 
```
 $hciconfig -h
```

6. Enable the Bluetooth device
  + 
```
 pi@raspberrypi:~ $ sudo hciconfig hci0 up
```

7. Set the Bluetooth device to "advertise and not-connectable" 
  + 
```
 pi@raspberrypi:~ $ sudo hciconfig hci0 leadv 3
```

8. Enter the Beacon Advertising Data
  + 
```
 pi@raspberrypi:~ $ sudo hcitool -i hci0 cmd 0x08 0x0008 17 02 01 06 03 03 aa fe 0f 16 aa fe 10 00 02 77 65 62 67 61 7a 65 72 08 00 00 00 00 00 00 00 00
```

&nbsp;

Here is a breakdown of the payload

| Option | Description                                                                                 |
| ------ | ------------------------------------------------------------------------------------------- |
| 0x08   | #OGF = Operation Group Field = Bluetooth Command Group = 0x08                               |
| 0x0008 | #OCF = Operation Command Field = HCI_LE_Set_Advertising_Data = 0x0008                       |
| 17     | Length.  The hexadecimal 17 converts to 23 decimal which is the number of bytes that follow |
| 02     | Length                                                                                      |
| 01     | Flags data type value                                                                       |
| 06     | Flags data                                                                                  |
| 03     | Length                                                                                      |
| 03     | Complete list of 16-bit Service UUIDs data type value                                       |
| aa     | 16-bit Eddystone UUID                                                                       |
| fe     | 16-bit Eddystone UUID                                                                       |
| 0f     | Length. The hexadecimal 0f converts to 15 decimal which is the number of bytes that follow  |
| 16     | Service Data data type value                                                                |
| aa     | 16-bit Eddystone UUID                                                                       |
| fe     | 16-bit Eddystone UUID                                                                       |
| 10     | Frame Type = URL                                                                            |
| 00     | TX Power (this should be calibrated)                                                        |
| 02     | URL Scheme (http:// = 0x02)                                                                 |
| 77     | 'w' in hexadecimal                                                                          |
| 65     | 'e' in hexadecimal                                                                          |
| 62     | 'b' in hexadecimal                                                                          |
| 67     | 'g' in hexadecimal                                                                          |
| 61     | 'a' in hexadecimal                                                                          |
| 7a     | 'z' in hexadecimal                                                                          |
| 65     | 'e' in hexadecimal                                                                          |
| 72     | 'r' in hexadecimal                                                                          |
| 08     | .org (.org = 0x08)                                                                          |
| 00     |                                                                                             |
| 00     |                                                                                             |
| 00     |                                                                                             |
| 00     |                                                                                             |
| 00     |                                                                                             |
| 00     |                                                                                             |
| 00     |                                                                                             |
| 00     |                                                                                             |

&nbsp;

The command above broadcasts my blog's URL [http://webgazer.org](http://webgazer.org).  
If you want to advertize a different URL enter the URL of the link that 
you want to advertize in the box below.
&nbsp;

<iframe src="https://yencarnacion.github.io/eddystone-url-calculator" style="overflow:hidden;height:100%;width:100%" height="100%" width="100%"> </iframe>

&nbsp;

To detect the Raspberry Pi beacon with an iPhone follow the steps in the 
video below which outlines how to enable Chrome's Physical Web extension 
on iOS [https://www.youtube.com/watch?v=gxPcPXSE_O0](https://www.youtube.com/watch?v=gxPcPXSE_O0)

On Android, your phone should detect the URL if you have Android 4.3.2 or higher
with bluetooth turned on, location turned on, and Chrome location runtime
permission turned on.  See [https://support.google.com/chrome/answer/6239299?hl=en](https://support.google.com/chrome/answer/6239299?hl=en). However, I had
to install the Physical Web App from [https://play.google.com/store/apps/details?id=physical_web.org.physicalweb&hl=en](https://play.google.com/store/apps/details?id=physical_web.org.physicalweb&hl=en) to make it work.
