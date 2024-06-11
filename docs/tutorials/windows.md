# Windows Tutorial
*Thanks to u/bg7fbi on Reddit for originally posting this method*

## Prerequisites
> Store these files in an easily accessible location, such as your desktop.
> For this tutorial, we will be using `C:\carthing`

+ A PC running Windows
+ USB-C to USB-C or USB-C to USB-A cable
+ [SDK Platform Tools](https://developer.android.com/tools/releases/platform-tools) (scroll down and click "Download SDK Platform-Tools for Windows")
+ [Python](https://www.python.org/downloads/) (make sure to add to PATH)
+ [Git for Windows](https://github.com/git-for-windows/git/releases/)
+ [superbird-tool](https://github.com/bishopdynamics/superbird-tool) (click the green button that says "Code" and then "Download ZIP". Extract files to `C:\carthing\superbird-tool`)
+ [Jailbreak Firmware](https://mega.nz/folder/NxNXQCaT#-n1zkoXsJuw-5rQ-ZYzRJw/file/4klEDaAR) (Extract files to `C:\carthing\lastest_fw_with_adb`)
+ [Zadig](https://zadig.akeo.ie/)

## Flashing the Jailbreak Firmware

1. Connect your Car Thing to your computer while holding buttons 1 & 4.
      - If you open Device Manager, you should see a device called "GX-CHIP"
2. Launch Zadig and install/replace the USB driver to libusbK.
3. Open the folder with the Jailbreak Firmware and rename the following:
      - `settings.dump` to `settings.ext4`
      - `system_a.dump` to `system_a.ext2`
      - `system_b.dump` to `system_b.ext2`
      - `data.dump` to `data.ext4`
4. Open command prompt and run the following command:
      - `python -m pip install git+https://github.com/superna9999/pyamlboot`
        - If that command fails, try:
    `python -m pip install git+https://github.com/superna9999/pyamlboot.git`

5. Run the following commands:
```bash
# Get to the correct directory
cd C:\carthing\superbird-tool

# Check that your Car Thing is connected and is in USB MODE
python ./superbird_tool.py --find_device

# Enable Burn Mode so you're able to send commands
python ./superbird_tool.py --enable_burn_mode

# Check again to make sure your Car Thing is connected and is in USB BURN MODE
python ./superbird_tool.py --find_device

# Disable A/B, lock to A
python ./superbird_tool.py --disable_avb2 A

# Flash the Jailbreak Firmware
python ./superbird_tool.py --restore_device C:\carthing\latest_fw_with_adb
```
> Flashing the firmware will take some time. As long as the program is running, you're good.

> **IMPORTANT NOTE!**
> 
> It is expected that the data partition will fail. This is normal and you should just be able to unplug/plug in your Car Thing and it will boot.

You can now enable ADB on your Car Thing.

## Enabling ADB
To enable ADB on your Car Thing, you need to first plug in your Car Thing to your computer while holding button 4. Your Car Thing should be stuck on the boot screen.

1. In the same command prompt and run the following commands:
```bash
# Check connectivity and make sure it is in USB BURN MODE
python ./superbird_tool.py --find_device

# If your Car Thing isn't in USB BURN MODE, run:
python ./superbird_tool.py --enable_burn_mode

# Now boot to ADB mode
python ./superbird_tool.py --boot_adb_kernel A
```
Check to make sure your Car Thing is in ADB mode:
```bash
adb devices
```
You should see
> **List of devices attached**
>
> **123456 device**

You can now use ADB to interact with your Car Thing.