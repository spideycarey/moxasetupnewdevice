# moxasetupnewdevice

Setup for Moxa UC-8200 from base image to restore configuration

1. SSH into device via ethernet using LAN 2 on device
   - Use Putty software
     - LAN 2 Default IP is `192.168.4.127`
     - Use Port `22`
   
   ![lan2](https://user-images.githubusercontent.com/109390971/182858043-242a11da-11f1-40d3-b667-8326291d9cc2.png)

2. Update edge computer name
   1. Type `sudo hostnamectl set-hostname KRxxxxxxx-EC01`
      - Host Name has the LSD, eg Pad 03-29-064 is KR0329064-EC01
   2. Type `sudo vi /etc/hosts`
      - To update file, press 'Insert' on keyboard to insert text rather than replace.
      - Edit first line to be "127.0.0.1 localhost"
      - Edit second line to be "127.0.0.1 KRxxxxxxx-EC01"  (But use the actual host name)
      - ![image](https://user-images.githubusercontent.com/109390971/211092041-e9df3e9e-de0c-4b49-8abc-38d081b15b9d.png)
      - To save press 'esc' then ':wq'

   3. To verify type `hostnamectl`.
   
      ![image](https://user-images.githubusercontent.com/109390971/184705976-ea4972e0-168a-4675-94cf-193c780683d2.png)
   4. The following commands are to clear/reset files for the edge device to use the new hostname
      - Type `cd /usr/local/bin/ignition`
      - Type `sudo ./ignition.sh stop`
      - Type `sudo rm webserver/metro-keystore`
      - Type `sudo rm data/.uuid`
      - Then reboot device `Sudo Reboot`

3. Configure Ignition Edge
   1. Open web browser and type http://192.168.4.127:8088
   2. Go to 'Config' on the left and login.
      * This username and password are not the same as the moxa device.  These seperate credentials can also be found in secret server
   3. Go to 'Licensing'.
   4. Click on 'Activate'.
   5. Enter Key and click submit.  Once accepted reboot the edge device and ensure everything is running as expected
   6. Click on ![image](https://user-images.githubusercontent.com/109390971/184707110-e554a741-c8c3-4958-ab9f-74c268e426a4.png).
   7. Chose file to restore.
      - If this is a restore, leave all boxes unchecked.
      - If this is restore is to create a new file, check "Override Gateway Name" and enter the new Gateway Name.
      ![image](https://user-images.githubusercontent.com/109390971/184719517-3fc4fb82-ce6a-4e16-947e-47dba5cb804b.png)
   8. After the gateway start again, go to ![image](https://user-images.githubusercontent.com/109390971/184720451-76b11573-01cb-4a73-a06d-6fd38f4c658c.png).
   9. Scroll down to ![image](https://user-images.githubusercontent.com/109390971/184720530-11f9ba16-a480-4ee5-b6ef-3716e1fca56a.png).
   10. Change project name to match LSD of site ![image](https://user-images.githubusercontent.com/109390971/184720624-b854fcf0-2f3a-4dd8-8884-036246aaf648.png)
   11. ![image](https://user-images.githubusercontent.com/109390971/184791340-582a3a45-7f12-4ccd-aa8c-ba24f5cbf66a.png)


4. Update LAN 1 IP Address to match the site IP list
   1. Go back to Putty and log into device as before
   2. Type `sudo vi /etc/network/interfaces`
      - To update file, press 'Insert' on keyboard to insert text rather than replace.
   3. Edit file to remove the eth0 DHCP line, remove hash's from the 4 lines after and update address, netmask and gateway.
   4. ![image](https://user-images.githubusercontent.com/109390971/184722809-bc90f63a-314e-4561-8333-5cca62653f20.png).
   5. It should look like above and once done press 'ESC' key and then ':wq' to save and exit file
   6. Type `sudo reboot` to reboot device
   7. Connect PC to LAN 1, update PC network to be in same subnet as device and test IP settings.
