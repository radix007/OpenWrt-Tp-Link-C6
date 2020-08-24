# OpenWrt Guide For Tp Link Routers :

#### What Is Openwrt ?

- OpenWrt (OPEN Wireless RouTer) is an open source project for embedded operating systems based on Linux, primarily used on embedded devices to route network traffic. 



#### This Guide Will Work For All Supported [Tp Link Routers](https://openwrt.org/toh/views/toh_fwdownload?dataflt%5BBrand*%7E%5D=TP-Link)

* Fix For Invalid File Type Issue .

#### I am not responsible for any damage to your router , if you do this then it is at your own risk . 


##### I am going to use Tp Link C6 Gigabit Router (EU Version 2.0) .
- Note : Will Work For Tp Link A6 as both are the same . 
- For US Model ,  A network switch is need to be connected between the router and TFTP server, force 100Mbps FullDuplex connection .


#### Things To Keep In Mind Before Installing Openwrt :
- Do not connect the modem and the router until instructed . 
- If you power down the device while it is installing or upgrading then you will break the firmware .



### Downloading  Openwrt  : 

- First check whether your router is supported , you can check [here](https://openwrt.org/toh/views/toh_fwdownload) . You can find your hardware version by following these [steps](https://www.tp-link.com/us/support/faq/46/) 
  
![Alt Text](/images/Image1.png)

- Now once you find your router , Download the corresponding Firmware . I am going to download the stable version and copy it to the desktop .You can download the snapshot if you want.  



  **Note : Snapshot Firmware  Doesn't have GUI , so you will have to install Luci package manually , I will show you how to install the normal stable version as I encountered a lot of problems with the snapshot version , if you want the snapshot then the process is the same just download the snapshot instead of normal version** 

* You Can Find The Diff btw stable build and snapshot [here](https://openwrt.org/releases/snapshot) and choose accordingly.

- So , I have downloaded The File From **"Firmware Openwrt Upgrade URL Column ".**

* Place This Downloaded File on your desktop in a folder , just name the folder openwrt , its up to you.
  


### Installing Openwrt (Method A) : 

- Since The Latest Tp-link-C6 Update , the version 1.3.5(Archer C6(EU)_V2_200630) released on 14th July 2020 , you cannot downgrade nor install openwrt , it shows **Invalid File Type** . If You are facing this issue then refer to Method B . 

* If Your Firmware version is below 1.3.5 then choose Method A . If Still facing invalid file type then refer to Method B .



- So After Downloading openwrt snapshot firmware , Follow the following steps : 

  - Go To 192.168.0.1 (Or tplinkwifi.net) . Enter The password . 
  * Then Go To  :   Advanced --> System Tools --> Firmware Upgrade --> Browse --> Desktop/openwrt-ath79-generic-tplink_archer-c6-v2-squashfs-factory.bin 

   - After This Click On Upgrade And Done . Now Skip To **Setting Up Openwrt.** 
   * **If You Get Invalid File Type Then Refer To Method B**


![Alt Text](/images/Image2.png) 

![Alt Text](/images/Image3.png) 


### Installing Openwrt Using Tftpd (Method B) :

- If You are getting Invalid File type then choose this method . 

![Alt Text](/images/Image6.png) 

 
* This Method can also be used if your router stops working or their is some problem while installing openwrt or you have bricked your firmware .

-  First Download Tftpd from [here](https://tftpd32.jounin.net/tftpd32_download.html) , Choose tftpd64 installer . 

* Click on the downloaded file  and install it , just click next and next , everything is pretty straightforward . 

![Alt Text](/images/Image4.png) 




![Alt Text](/images/Image5.png) 

- After This : Right Click Your Network Icon --> Open Network And Internet Settings --> Under Change Your Network Settings Click On **Change Adapter Options** --> Double Click  Ethernet --> Double Click Internet Protocol Version(TCP/IPv4) --> Then Change from Obtain Ip Address Automatically to **Use The Following Address** 

* IP ADDRESS :  Enter 192.168.0.66 , Click On Subnet Mask ,  It will automatically change to **255.255.255.0**  , then click okay . (You have to chnage this back to automatically later)

![Alt Text](/images/Image7.png) 



- Now open  Tftpd64 (Desktop) , You can see the current directory change it to the directory where you have downloaded the firmware file , better would be to just copy the firmware file to a folder on the  desktop . 

* Now After This Click on the Log Viewer Tab . 

- **The Most Crucial Step : Power off The Router**, And Then when you power it on  , press the reset button simultaneously (power and reset at the same time , release the power button , but dont release the reset button until you see the output as shown in the pic) (for about 5-10 sec) , you will see the log tab getting filled (right now its looking for a particular file in the current directory ) . 
* In My Case It Is looking for this file **"ArcherC6v2_tp_recovery.bin"** , rename the openwrt firmware file with this file name and **then power off the router again and then power on again while simultaneously pressing the reset button**  Make Sure that the Current Directory is the one in which the openwrt firmware  is located with the new file name . It Will Copy That File automatically and will install openwrt . Once This is Done Openwrt will be installed on your router . 

![Alt Text](/images/Image8.png) 



- If you have bricked your router  or you want to downgrade your router then  , just do this and rename the firmware that you want to replace it with . This is how you can downgrade or fix a broken firmware Tp Link Router . 

* Now change back the IP Address TCP/IPv4 from 192.168.0.66 to "automatically optain Ip Address " . 



#### Setting Up Openwrt (Using ssh ) :

- Open a Terminal and then type -  
  > ssh root@192.168.1.1

- After this connect the router to the modem  , plug the ethernet cable into the wan port . 

- Once This is done enter the following commands :
  > ping google.com


  > opkg update


  > opkg install luci-ssl-nginx

- The Following Command is to Download WPA3 .(Optional But Highly Recommended) 


  > opkg install --force-depends --force-maintainer --force-overwrite wpad-openssl

  > reboot  


- After All this Is Done . Open your browser and type **openwrt.lan** or **https://192.168.1.1/cgi-bin/luci/** , It will show Connection not secure add an exception and then openwrt login page will come , by defualt no password . 

- After This Just Configure Your Openwrt . 

![Alt Text](/images/Image9.png) 

![Alt Text](/images/Image10.png)


![Alt Text](/images/Image11.png)

#### Setting up Openwrt (Using Putty) :

 - The Method is the same , same commands as above . I am not going to show how to install putty .

*  Once You Have Putty Up And Running , repeat the same commands as above .


**Read More About WPA3 [Here.](https://www.wi-fi.org/discover-wi-fi/security)**



#### Thank you Guys , Hope This Helps You . Any Recommendations are Welcomed 

