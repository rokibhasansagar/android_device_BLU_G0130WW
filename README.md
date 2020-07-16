# Unofficial TWRP Device Tree for BLU G9 - G0130WW

Original Tree made by @lopestom and built by @rokibhasansagar

## About Device

![BLU G9 G0130WW](https://fdn2.gsmarena.com/vv/pics/blu/blu-g9-1.jpg)

## Download links

- Latest Unoficial TWRP v3.4.0 at https://github.com/rokibhasansagar/android_device_BLU_G0130WW/releases/tag/twrp_v3.4.0

- Latest PitchBlack Recovery at https://github.com/rokibhasansagar/android_device_BLU_G0130WW/releases/tag/2.9.1-test

### Specifications

Component Type | Details
-------:|:-------------------------
CPU     | Octa-core 2.0 GHz Cortex-A53 Helio P22 (12 nm)
Platform | MediaTek MT6762
GPU     | PowerVR GE8320
Architecture | 64 bit
Memory  | 4 GB RAM
Shipped Android Version | 	Android 9.0 Pie
Storage | 64 GB
Battery | 4000 mAh
Height | 155.4 mm
Width | 71.8 mm
Thickness | 8.1 mm
Weight | 165 g
Display | 6.3" (99.1 cm2)
Screen resolution | 720 x 1520 pixels, HD+
Pixel density | 267 PPI
Video | 1920p, 1080p video, 30fps
Primary Camera | 13 MP + 2 MP(depth), f/2.0, 1/3", Five lenses Rear Camera, PDAF
Secondary Camera | 13 MP, f/2.0, 1/3"
Quick charging | Fast charging
Wifi | Yes, IEEE802.11 a/b/g/n, Supports 5G Wi-Fi Signal / Wi-Fi Direct / Wi-Fi Display
Bluetooth | v4.0, Bluetooth, A2DP
USB Type-C | Yes, 2.0, Type-C 1.0 reversible connector
NFC | No
Network support | Both SIM slots are compatible with 4G
GPRS | Available
EDGE | Available
SIM size | SIM1: Micro, SIM2: Nano
CARD slot |	microSD, up to 128 GB (microSDXC)
SD slot |	SIM1 + microSD or SIM2 + microSD
Sensors | Fingerprint (rear-mounted), Accelerometer, Gyroscope, Geomagnetic Sensor

Network | Bands
-------:|:-------------------------
2G | GSM 850 / 900 / 1800 / 1900 - SIM 1 & SIM 2
3G | HSDPA B1 (2100), B2 (1900), B4 (1700/2100 AWS A-F), B5 (850), B8 (900)
4G | LTE band 1 (2100), 2 (1900), 3 (1800), 4 (1700/2100 AWS 1), 5 (850), 7 (2600), 8 (900), 12 (700), 13 (700), 17 (700), 28 (700)
Speed | HSPA 42.2/11.5 Mbps, LTE-A (2CA) Cat6 300/50 Mbps

**This device tree can be used to build TWRP for BLU G9 - G0130WW**


## Build Instructions for Developers

Sync Minimal Manifest Sources with _twrp-9.0_ branch in a separate directory inside HOME
```bash
mkdir -p $HOME/android && cd $HOME/android/
repo init -q -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0 --depth 1
repo sync -c -q --force-sync --no-clone-bundle --no-tags -j$(nproc --all)
```
Do the following _Hack_ (right after repo sync ends) for bypassing the _OmniROM roomservice_ which now prevents lunching Unofficial Devices.
```bash
# Unshallow vendor_omni (Only for Unofficial Builds)
echo -e "\nFixing Unofficial TWRP Build lunch error\n"
repo forall vendor/omni -c "git fetch --unshallow omnirom android-9.0"
# Retain "roomservice: Do not overwrite existing repositories"
repo forall vendor/omni -c "git revert 718f4c2fd6890f5eaa2d4972b1c3f3f582b5da47 -Xtheirs --no-edit --no-commit"
# Retain "roomservice: Do not overwrite existing devices"
repo forall vendor/omni -c "git revert 380d19cea2857d5901d7e7163f65ccc66d7bbad7 -Xtheirs --no-edit --no-commit"
# Add those retains into local commit
repo forall vendor/omni -c "git commit -m 'Fix Build from forked/personal repos'"
```
Now git clone this repository
```bash
git clone https://github.com/rokibhasansagar/android_device_BLU_G0130WW -b android-9.0 device/BLU/G0130WW
```
Now, Start the build process
```bash
export ALLOW_MISSING_DEPENDENCIES=true
. build/envsetup.sh
lunch omni_G0130WW-eng
mka recoveryimage
```
