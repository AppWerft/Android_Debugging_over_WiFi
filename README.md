# Android debugging and screen mirroring over Wifi

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

