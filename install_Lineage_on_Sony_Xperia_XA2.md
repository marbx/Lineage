
# Install Lineage on Sony XA2
You need Linux, adb and TWRP.

## Temporarily boot XA2 into TWRP
[Official docs](https://wiki.lineageos.org/devices/pioneer/install)

1) Get the latest TWRP image (twrp-*pioneer.img) from  https://twrp.me/

2) Boot XA2 into fastboot mode (blue LED)
- Turn off your XA2 
- Press and hold the Volume ***Up*** key for a few seconds
- Connect the USB cable and watch the LED turn blue
- Release the Volume ***Up*** key
- You may execute `fastboot devices` to verify

3) Fastboot into TWRP:
- Execute `fastboot boot twrp-3.3.1-4-pioneer.img` 

Notes: 
- Fastbooting TWRP ends fastboot mode, only adb commands still work
- Don't flash TWRP, this would destroy Lineage! (Do NOT excute `fastboot FLASH boot twrp-ERROR.img`)
  
## Sideload Firmware
1) Inquire firmware version from post https://forum.xda-developers.com/showpost.php?p=78973496&postcount=2

As of 2019-08: UK 50.1.A.12.123  

As of 2019-12: 50.2 or 50.1 and [pioneer_modem_bt_dsp_50.2.A.0.400.zip](https://androidfilehost.com/?fid=1899786940962602524) 

2) Temporarily boot into TWRP!

3) Execute

        adb shell twrp sideload
        adb sideload pioneer_modem_bt_dsp_50.2.A.0.400.zip

## Sideload Lineage
Get Lineage build from https://download.lineageos.org/pioneer
Continue on https://wiki.lineageos.org/devices/pioneer/install 

1) Temporarily boot into TWRP

2) Execute

        adb shell twrp sideload
        adb sideload lineage-16.0-20200106-nightly-pioneer-signed.zip

## Reboot from TWRP into Lineage
- Press Reboot, then press System
- Uncheck "Prompt to install TWRP" 
- If you see "Swipe to install TWRP App": chose "Do not Install"
- If TWRP issues warning "No OS has been installed": ignore

## Glossary

Bootloader mode = download mode = fastboot mode

## PROBLEM "Boot loop" into 'your device is corrupt'

    Your device is corrupt
    It can't be trusted and will not boot
    Your device will be powered off in 5 seconds

### SOLUTION switching slots twice

    fastboot getvar current-slot
    current-slot: _a

    fastboot set_active b
    fastboot set_active a

