# Android debugging and screen mirroring over Wifi


<img src="https://i.imgur.com/wO1TIO1.jpg" width=400 />


Since the new devices has USB-C plugs the connection is very instable. Short interruptions (triggered by looking to device) kills the debug session. This article describes an alternative.

## Start

First you have to connect you device with a cable. After enabling of developer mode (7x pressing …) and enabling of USB mode you type on you console on host:

```
adb connect tcpip 5555
```

The system will answer with a success message. If there are issues, then you can test with:

```
adb devices
```

Now a server is running on devicer. Perhaps you have to repeat this procedure after reboot of mobile device.

## Connecting

Now we have two cases: you are in an available Wifi infrastructure or not.

### Infrastructur

Both decvice must be in same net. The you open on device the `System configuration/Network manager/Wifi/MY_NET/Advanced` an get the IP number of device. Then on host:

```
adb connect IP_NUMBER:5555
adb devices

Rainers-MBP-3:Hoerdat fuerst$ adb devices
List of devices attached
192.168.43.130:5555	device
```

Et voilà!

### Own net (tethering)

After connecting you host with the tethered net you open the System `Configuration/Network/MY_TETHERED_NET/TCPIP` and get the IP

<img src="https://i.imgur.com/JxkReY9.png" width=400 />

```
adb connect 192.168.43.83:5555
```
Et voilà!

### Screen mirroring

First install ffmpeg

```
brew install ffmpeg
```
And:

```
adb shell screenrecord --bit-rate=16m --output-format=h264 --size 800x600 - | ffplay -framerate 60 -framedrop -bufsize 16M 
```
And after a couple of moments you see the mobile screen on your Mac.

<img src="https://i.imgur.com/A4Qct3D.jpg" width=400 />

Hint:
You can put the long line in a file places in path.

### Potential pitfal
The tethering method offen changes the IP of host.
