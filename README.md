# OpenWrt Guide For Tp Link Routers ::

#### What Is Openwrt ?

- OpenWrt (OPEN Wireless RouTer) is an open source project for embedded operating systems based on Linux, primarily used on embedded devices to route network traffic.

#### This Guide Will Work For All Supported [Tp Link Routers](https://openwrt.org/toh/views/toh_fwdownload?dataflt%5BBrand*%7E%5D=TP-Link)

- [Fix For Invalid File Type Issue](#installing-openwrt-using-tftpd-method-b-)

* [Revert Back To Stock Firmware if something happens to your router or if your Openwrt installation fails](#how-to-go-back-to-stock-firmware--)

* #### **NOTE: If you do this, you do so entirely at your own risk."**

- #### **I am going to use Tp Link C6 Gigabit Router (EU Version 2.0)**

- Note : It will work for Tp Link A6 as both are the same

* For the US model, a network switch is needed to be connected between the router and the TFTPD server to force a 100Mbps FullDuplex connection

#### **Things To Keep In Mind Before Installing Openwrt ::**

- Do not connect the modem and the router until instructed
- If you power down the device while it is installing or upgrading, then you will break the firmware

## **Downloading Openwrt ::**

- Check first to see if your router is supported, which you can do [here](https://openwrt.org/toh/views/toh_fwdownload) . You can find your hardware version by following these [steps](https://www.tp-link.com/us/support/faq/46/)

![Alt Text](/images/Image1.png)

- Now, once you find your router, download the corresponding firmware. I am going to download the stable version and copy it to the desktop. You can download the snapshot if you want

  **Note : Snapshot Firmware doesn't have a GUI, so you will have to install the Luci package manually. I will show you how to install the normal stable version as I encountered a lot of problems with the snapshot version. If you want the snapshot firmware, the procedure is the same; simply download the snapshot rather than the regular version**

* The difference between Stable Build and Snapshot can be found [here](https://openwrt.org/releases/snapshot)

- So, I have downloaded the file from **"Firmware Openwrt Upgrade URL Column"**

* Place this downloaded file on your desktop in a folder. Just name the folder openwrt. It is up to you

## Installing Openwrt (Method A) ::

- You cannot downgrade or install OpenWrt since the latest Tp-link-C6 Update, version 1.3.5 (Archer C6(EU)\_V2_200630), which was released on July 14th, 2020, because it displays an invalid file type.If you are facing this issue, then refer to Method B

* If your firmware version is below 1.3.5, then choose Method A. If you are still facing an invalid file type, then refer to Method B

- So, after downloading the openwrt snapshot firmware, follow the following steps:

  - Go to 192.168.0.1 (or tplinkwifi.net). Enter the password

  * Then navigate to **Advanced--> System Tools--> Firmware Upgrade--> Browse--> Desktop/openwrt-ath79-generic-tplink_archer-c6-v2-squashfs-factory.bin**

  - After this, click on "Upgrade" and done. Now, skip to **Setting Up Openwrt.**

  * **If You Get An Invalid File Type, Then Refer To Method B**

![Alt Text](/images/Image2.png)

![Alt Text](/images/Image3.png)

## Installing Openwrt Using Tftpd (Method B) ::

- If you are getting an invalid file type, then choose this method

![Alt Text](/images/Image6.png)

- This method can also be used if your router stops working, or if there is some problem while installing OpenWRT, or if you have bricked your firmware

* First download Tftpd from [here](https://tftpd32.jounin.net/tftpd32_download.html), choose tftpd64 installer

- Click on the downloaded file and install it. Then just click next and next. Everything is pretty straightforward

![Alt Text](/images/Image4.png)

![Alt Text](/images/Image5.png)

- After This : Right Click Your Network Icon --> Open Network And Internet Settings --> Click **Change Adapter Options** under "Change Your Network Settings. --->Double Click Ethernet --> Double Click Internet Protocol Version (TCP/IPv4) --> Then Change from **Obtain Ip Address Automatically** to **Use The Following Address**

* IP Address: Enter 192.168.0.66, then click Subnet Mask, which will change to **255.255.255.0** automatically, and then click OK. (You have to change this back to automatically later)

![Alt Text](/images/Image7.png)

- Now open Tftpd64 (Desktop). You can see the current directory. Change it to the directory where you have downloaded the firmware file. It would be better to just copy the firmware file to a folder on the desktop

* Now after this, click on the Log Viewer Tab

- **The Most Crucial Step : Power off the router**, and then when you power it on, press the reset button simultaneously (power and reset at the same time), release the power button, but don't release the reset button until you see the output as shown in the pic (for about 5-10 sec). You will see the log tab getting filled (right now it is looking for a particular file in the current directory)

* In my case, it was looking for this file **"ArcherC6v2_tp_recovery.bin"** , rename the openwrt firmware file with this file name, and **then power off the router again and power on again while simultaneously pressing the reset button** Make sure that the current directory is the one in which the openWRT firmware is located with the new file name . It will copy that file automatically and will install OpenWrt. Once this is done, Openwrt will be installed on your router

![Alt Text](/images/Image8.png)

- If you have bricked your router or you want to downgrade your router, then just do this and rename the firmware that you want to replace it with. This is how you can downgrade or fix a broken firmware for a TP-Link router

* Now change the IP address TCP/IPv4 from 192.168.0.66 to "automatically optain IP Address"

<br>

## Setting Up Openwrt (Using ssh) ::

- Open a terminal and then type:

  ```
  > ssh root@192.168.1.1
  ```

- After this, connect the router to the modem and plug the ethernet cable into the wan port

- Once this is done, enter the following commands:

  ```
  > ping google.com

  > opkg update

  > opkg install luci-ssl-nginx
  ```

- The following command is to download WPA3. (Optional, but strongly advised)

  ```
  > opkg install --force-depends --force-maintainer --force-overwrite wpad-openssl

  > reboot
  ```

- After all this is done, Open your browser and type **openwrt.lan** or **https://192.168.1.1/cgi-bin/luci/** , It will show "connection not secure". Add an exception and then the OpenWRT login page will come. By default, there is no password

- After this, just configure your Openwrt

![Alt Text](/images/Image9.png)

![Alt Text](/images/Image10.png)

![Alt Text](/images/Image11.png)

## Setting up Openwrt (Using Putty) ::

- The method is the same, with the same commands as above. I am not going to show you how to install putty

* Once you have Putty up and running, repeat the same commands as above
  <br>

## How To Go Back To Stock Firmware ::

- **Download the oldest version. Like in my case, [Archer A6(EU)\_V2_200110 , 2020-02-17](<https://static.tp-link.com/2020/202002/20200217/Archer%20A6(EU)_V2_200110.zip>). Sometimes the newer versions don't work for some reason, so always go with the oldest version and then update to the newest version**

- **NOTE : If the above file doesn't work, then download it from [here.](<https://static.tp-link.com/2018/201808/20180814/Archer%20C6(EU)_V2_180627.zip>) This is the oldest version available (1.0.1). If you click on the link, it will not work, so copy the link and paste it in the URL tab and press enter**

- Now download Tftpd from [here](https://tftpd32.jounin.net/tftpd32_download.html) and choose the TFTPD64 installer

* Click on the downloaded file and install it. Then just click next and next. Everything is pretty straightforward.

![Alt Text](/images/Image4.png)

![Alt Text](/images/Image5.png)

- After This : Right Click Your Network Icon --> Open Network And Internet Settings --> Under Change Your Network Settings Click On **Change Adapter Options** --> Double Click Ethernet --> Double Click Internet Protocol Version(TCP/IPv4) --> Then Change from Obtain Ip Address Automatically to **Use The Following Address**

* IP ADDRESS : Enter 192.168.0.66 , Click On Subnet Mask , It will automatically change to **255.255.255.0** , then click okay . (You have to chnage this back to automatically later)

![Alt Text](/images/Image7.png)

- Now open Tftpd64 (Desktop). You can see the current directory. Change it to the directory where you have downloaded the stock firmware (unzip the firmware file and copy the bin file to the working directory). Better yet, just copy the firmware file to a folder on the desktop.

* Now after this, click on the Log Viewer Tab.

- **The Most Crucial Step: Power Off The Router**, And then when you power it on, press the reset button simultaneously (power and reset at the same time, release the power button, but don't release the reset button until you see the output as shown in the pic) (for about 5-10 sec), you will see the log tab getting filled (right now it is looking for a particular file in the current directory).

* In my case, it's looking for this file **"ArcherC6v2_tp_recovery.bin"**, rename the stock firmware file with this file name and **then power off the router again and then power on again while simultaneously pressing the reset button.** Make sure that the current directory is the one in which the stock firmware is located with the new file name. It will copy that file automatically and will install the TP Link stock firmware again. Once this is done, wait for about 2-3 min.

- **NOTE : For some people, file transfer stops when trying to revert back to stock firmware . So, for those people, try using cat 5 or cat 5e cable (to force a 100Mbps full duplex connection). This does not happen with everyone, but if it does, then you can try this.**

* This is how you can install the stock firmware if any problem arises during Openwrt installation or if something else happens to your router during the upgradation of stock firmware. If you are still not able to go back to stock firmware, then pull a request.

![Alt Text](/images/Image8.png)
<br>

## FAQ ::

- 5Ghz Performance depends on a lot of factors . Please always use the stable Openwrt branch . Don't go for the snapshot version.

* In the wireless radio settings in Luci choose your country for signal strength accordingly.

- **Some people have complained about issues with 5Ghz performance, so if the other things don't work for you, then you can always go back to stock firmware**.

<br>

**Read more about WPA3 [here.](https://www.wi-fi.org/discover-wi-fi/security)**

# Contributing ::

Please check out the [contributing.md](Contributing.md) guide on how you can actively participate in the development of this guide.

# License ![GitHub](https://img.shields.io/badge/license-GPL--3.0%20License%20-blue)

This project is licensed under the GNU General Public License v3.0 - see the [License.md](https://github.com/radix007/OpenWrt-Tp-Link-C6/blob/master/LICENSE) file for more details.
