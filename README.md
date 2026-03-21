```markdown
# TWRP for Oppo A32 / Oppo A53

This is a custom TWRP (Team Win Recovery Project) device tree for the Oppo A32 / Oppo A53 (codenamed *PDVM00* / *OP4E35* / *CPH2127* / *OP4EFDL1 *).

| Feature                 | Specification                                                     |
| :---------------------- | :-----------------------------------------------------------------|
| Chipset                 | Qualcomm SM4250 Snapdragon 460 (11 nm)                            |
| CPU                     | Octa-core (4x1.8 GHz Kryo 240 & 4x1.6 GHz Kryo 240)               |
| GPU                     | Adreno 610                                                        |
| Memory                  | 64GB 4GB RAM, 128GB 4GB RAM, 128GB 8GB RAM                        |
| Shipped Android Version | 11.0 (ColorOS 11)                                                 |
| Storage                 | UFS 2.1                                                           |
| SIM                     | Dual SIM (Nano-SIM, dual stand-by)                                |
| MicroSD                 | microSDXC (dedicated slot)                                        |
| Battery                 | 5000 mAh Li-Po (non-removable), 18W wired                         |
| Dimensions              | 163.9 x 75.1 x 8.4 mm                                             |
| Weight                  | 186 g                                                             |
| Display                 | 6.5 inches IPS LCD, 90Hz, 720 x 1600 pixels, 20:9 ratio (~270 ppi)|
| Rear Camera             | Triple: 13 MP (wide) + 2 MP (macro) + 2 MP (depth)                |
| Front Camera            | 8 MP, f/2.0                                                       |
| Fingerprint             | Rear-mounted                                                      |
| Sensors                 | Accelerometer, Proximity, Compass                                 |
| Sound                   | Stereo speakers with 3.5mm jack                                   |
| USB                     | USB Type-C 2.0, OTG                                               |
| WLAN                    | Wi-Fi 802.11 a/b/g/n/ac, dual-band, Wi-Fi Direct                  |
| Bluetooth               | 5.0, A2DP, LE, aptX HD                                            |
| NFC                     | No                                                                |
| Models                  | PDVM00, OP4E35 / CPH2127 , OP4EFDL1                               |

## Important Note About Screen Lock / Sleep

**Due to a limitation in the stock kernel, the normal screen blank / lock functionality does not work correctly in TWRP on this device.**  
If you attempt to let the screen turn off normally (e.g., by inactivity or pressing the power button), the device may become unresponsive or even crash.

As a **workaround**, this TWRP build keeps the screen **always on**, but sets the backlight brightness to **zero** when the device is considered “idle”.  
This effectively simulates a sleep state:

- The display remains powered (no blank/off command is sent to the kernel),
- The backlight is turned off (brightness = 0),
- Touch input is still processed (waking the device requires a touch on the screen, which will restore brightness).

This approach minimizes power consumption and prevents possible screen burn‑in while avoiding the kernel lockup issue.  
**Please do not press the power button to try to turn off the screen** – use the touchscreen to wake the device after it dims.

## Known Issues

- **Data decryption (FBE) partially implemented but not fully stable**: Due to compatibility issues with Qualcomm's FBE implementation and the stock kernel, TWRP may not be able to decrypt the `/data` partition on some devices or after certain updates.  If this happens, you can try:
  - Formatting data (this will erase all user data, so backup first).
  - Flashing a different kernel or using a version of TWRP built with alternative decryption methods.
  This issue is under investigation and may be fixed in future releases.

## Features

- Based on TWRP 3.7.x (Android 11/12 compatible)
- Bootable and stable TWRP environment
- Dynamic partition support
- MTP support
- ADB (sideload, shell)
- Touch fully working
- Backup / Restore
- Sideloadly flashing ZIP / IMG
## Device Specifications


## Compile

To build this recovery from source, follow these steps:

1. Set up a TWRP build environment (AOSP 11 or 12.1 manifest recommended).
2. Clone this device tree into `device/oppo/PDVM00`.
3. Run the following commands:

```bash
. build/envsetup.sh
lunch twrp_PDVM00-eng
mka recoveryimage
```

The output image will be located at `out/target/product/PDVM00/recovery.img`.

## Credits

- @rtyutechstudio & @wudilsr-Opensource
- Thanks to Teamwin
- 

## Disclaimer

- This software is provided as-is, without any warranty. Use at your own risk.
- Modifying your device may void its warranty and can cause irreversible damage.
- Always make a backup of your important data before flashing.
```
