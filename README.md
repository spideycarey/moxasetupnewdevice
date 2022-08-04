# moxainstallnewfirmware

This is used for either creating a new bootable image, or installing the base Kakwa image onto a UC-8200.  The only difference is what image you load into the Micro USB

1. Load Firmware onto MicroUSB
   1. Plug Micro USB into PC
   2. Take the *.img firmware file and save it on the USB
      The name can be anything, but its best to keep it short as it will need to be typed later
   3. Eject the Micro SUSB from PC and plug it into the front of the UC-8200

2. Use a terminal named Tera Term for the next steps
   1. Open Tera Term
   2. Go to “Setup -> Serial Port” and change “Speed” to 115200 and change “Port” to your comm port.
      ![Terra](https://user-images.githubusercontent.com/109390971/182856647-318e0f68-f66d-49a5-b1d4-41617d40bb67.png)
   3. Plug serial cable into PC and into console port of device (Special cable needed, it comes with device)
   4. Reboot device and press delete key immediately.  That will open the boot menu.
      ![Boot Menu](https://user-images.githubusercontent.com/109390971/182856926-57a7c307-8a6e-4fc8-8a7b-4e2462c27899.png)
   5. Enter the full filename of firmware image

      ![v13](https://user-images.githubusercontent.com/109390971/182857128-4d81d0d9-243b-4c0d-82a9-5a685d7b1803.png)
   6. Wait for image to load.  Once the boot menu appears again, press 5 to Go to Linux
