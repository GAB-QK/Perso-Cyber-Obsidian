---
id: wifiPhisher
created_date: 18/10/2022
updated_date: 18/10/2022
type: note
---

#  wifiPhisher
- **🏷️Tags** :  #10-2022 #wifi #tools #credentials 

## 📝 Notes
- [Wifiphisher](https://wifiphisher.org/) is a rogue Access Point framework for conducting red team engagements or Wi-Fi security testing. Using Wifiphisher, penetration testers can easily achieve a man-in-the-middle position against wireless clients by performing targeted Wi-Fi association attacks. Wifiphisher can be further used to mount victim-customized web phishing attacks against the connected clients in order to capture credentials (e.g. from third party login pages or WPA/WPA2 Pre-Shared Keys) or infect the victim stations with malwares.

| short form              | Long form                                 | Explenation                                                                                            |
| ----------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| -eI EXTENSIONSINTERFACE | --extensionsinterface EXTENSIONSINTERFACE | Manually choose an interface that supports monitor mode for running the extensions. Example: -eI wlan1 |
| -aI APINTERFACE         | --apinterface APINTERFACE                 | Manually choose an interface that supports AP mode for spawning an AP. Example: -aI wlan0              |

#### exemple of launching command : 
- you need first to change the mode of the wifi card 
##### wifi card monitor mode  : 
``` bash
sudo ifconfig wlan0 down
sudo iwconfig wlan0 mode monitor
sudo ifconfig wlan0 up
```
##### Launch wifiphisher
``` bash
sudo wifiphisher -aI wlan0 -eI wlan1 
```

## Questions/Thoughts


## 🔗 Links
- [GitHub](https://github.com/wifiphisher/wifiphisher.git)
![[Pasted image 20221018094705.png]]