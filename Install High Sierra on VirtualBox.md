# Install macOS Hight Sierra on VirtualBox

Host: Windows 10 1803 x64

Follows below guideline
https://techsviewer.com/install-macos-high-sierra-virtualbox-windows/

To make it even faster, I created a batch script to finish all the jobs with just one-click.  
1. Save below script as "InstallMacOS.bat";  
2. Find the image at https://techsviewer.com/install-macos-high-sierra-virtualbox-windows/ and download it;  
3. Put the batch script and vm image at same directory;  
4. Run the script as Adminitrator;  
5. Open your VirtualBox to find a new VM named "macOS 10.12 Sierra"  
6. Enjoy!  
Visit TechsViewer for further information.

```
set VM="macOS High Sierra"
set PATH="C:\Program Files\Oracle\VirtualBox\"
VBoxManage createvm --name %VM% --ostype "MacOS1013_64" --register

VBoxManage storagectl %VM% --name "SATA Controller" --add sata --controller IntelAHCI
VBoxManage storageattach %VM% --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium "%~dp0macOS High Sierra.vmdk"

VBoxManage modifyvm %VM% --memory 4096 --vram 128 --cpus 2
VBoxManage modifyvm %VM% --firmware efi --pae on --chipset ich9 --rtcuseutc on 
VBoxManage modifyvm %VM% --accelerate3d on

REM it is important to set up mouse and keyboard to usb from default ps/2 to assure they work in guest system
VBoxManage modifyvm %VM% --mouse usbtablet --keyboard usb

VBoxManage modifyvm %VM% --boot1 disk --boot2 none --boot3 none --boot4 none

VBoxManage modifyvm %VM% --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff
VBoxManage setextradata %VM% "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"
VBoxManage setextradata %VM% "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
VBoxManage setextradata %VM% "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"
VBoxManage setextradata %VM% "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
VBoxManage setextradata %VM% "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1

pause
```

# After installation 
~~It seems a good idea to disable TRIM after system boot. The new OS stuck at "HID legacy shim 2" for very long time when I rebooted it for the first time. Below command works so far as I collected. ~~
```
sudo trimforce disable
```
~~The computer will automatically reboot after the command succeeds. ~~


Not sure about it.... Maybe just be patient and wait for 15+ minutes if encouter boot stucking. 

Download and double click to install if failed to install update 10.13.4 in app store.  


