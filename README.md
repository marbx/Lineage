## Searchh issues for Sony XA2
https://gitlab.com/LineageOS/issues/android/-/issues?label_name%5B%5D=device%3Apioneer&scope=all&state=closed


## Install Lineage on Sony XA2


## Install Lineage 16.0 on Sony XA2
Install adb on Linux.

### Temporarily boot XA2 into TWRP
[Official docs](https://wiki.lineageos.org/devices/pioneer/install)

1) Get the latest TWRP image (twrp-*pioneer.img) from  https://twrp.me/

2) Boot XA2 into fastboot mode (blue LED)
- Turn off the XA2
- Press and hold Volume ***Up***
- Wait a few seconds, connect the USB cable and watch the LED turn blue
- Release Volume ***Up***
- You may execute `fastboot devices` to verify

3) Fastboot into TWRP
- Execute `fastboot boot twrp-3.3.1-4-pioneer.img` 
- XA2 leaves fastboot mode, turns off blue LED and starts TWRP.

Note:
- Don't flash TWRP, this would destroy Lineage! (Do NOT excute `fastboot FLASH boot twrp-ERROR.img`)
  
### Sideload Firmware
1) Inquire firmware version from post https://forum.xda-developers.com/showpost.php?p=78973496&postcount=2

As of 2019-08: UK 50.1.A.12.123  

As of 2019-12: 50.2 or 50.1 and [pioneer_modem_bt_dsp_50.2.A.0.400.zip](https://androidfilehost.com/?fid=1899786940962602524) 

2) Temporarily boot into TWRP!

3) Execute

        adb shell twrp sideload
        adb sideload pioneer_modem_bt_dsp_50.2.A.0.400.zip

### Sideload Lineage
Get Lineage build from https://download.lineageos.org/pioneer

1) Temporarily boot into TWRP!

2) Execute

        adb shell twrp sideload
        adb sideload lineage-16.0-20200106-nightly-pioneer-signed.zip

### Leave TWRP
- Press Reboot, then press System
- Uncheck "Prompt to install TWRP" 
- If you see "Swipe to install TWRP App": chose "Do not Install"
- If TWRP warns "No OS has been installed": ignore

### Sony
- Flash Tool Emma https://developer.sony.com/develop/open-devices/get-started/flash-tool/

### Glossary

- Bootloader mode = download mode = fastboot mode
- Baseband = ?

### PROBLEM "Boot loop" into 'your device is corrupt'

    Your device is corrupt
    It can't be trusted and will not boot
    Your device will be powered off in 5 seconds

#### SOLUTION switching slots twice

    fastboot getvar current-slot
    current-slot: _a

    fastboot set_active b
    fastboot set_active a


