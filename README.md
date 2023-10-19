[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

# Welcome to WVR

![WVR Pinout Diagram](https://github.com/marchingband/wvr_hardware/blob/main/images/wvr_pinout.png)

## Quick Links
- **Purchase a WVR**: [Tindie](https://www.tindie.com/products/ultrapalace/wvr)
- **WVR Forum**: [Google Groups](https://groups.google.com/g/wvr-audio)
- **WVR Hardware Resources**: [GitHub](https://github.com/marchingband/wvr_hardware)
- **WVR Binaries**: [GitHub](https://github.com/marchingband/wvr_binaries)
- **Web UI Code**: [GitHub](https://github.com/marchingband/wvr_ui)
- **USB Backpack Code**: [GitHub](https://github.com/marchingband/wvr_usb_backpack)
- **Thames: WVR in a Pedal**: [GitHub](https://github.com/marchingband/wvr_thames)

## Table of Contents
- [Getting Started](#getting-started)
- [Powering WVR](#powering-wvr)
- [Updating Firmware](#updating-firmware)
- [Playing Sounds](#playing-sounds)
  - [Sound Settings](#sound-settings)
    - [Understanding Priority](#understanding-priority)
    - [Understanding Exclusive Group](#understanding-exclusive-group)
    - [Understanding Playback Mode](#understanding-playback-mode)
    - [Understanding Response Curve](#understanding-response-curve)
    - [Understanding Retrigger Mode](#understanding-retrigger-mode)
    - [Understanding Note Off](#understanding-note-off)
- [MIDI Control](#midi-control)
- [Web MIDI](#web-midi)
- [Using Racks](#using-racks)
- [Bulk Uploading Files](#bulk-uploading-files)
- [Bulk Uploading Racks](#bulk-uploading-racks)
- [Save and Load Voice Configuration](#save-and-load-voice-configuration)
- [Pitch Interpolation](#pitch-interpolation)
- [Pitch Interpolating a Rack](#pitch-interpolating-a-rack)
- [Pitch Interpolating an ASR Loop](#pitch-interpolating-an-asr-loop)
- [Using FX](#using-fx)
- [Global Settings](#global-settings)
- [Firmware Manager](#firmware-manager)
- [Setting Up for Arduino IDE Programming](#setting-up-for-arduino-ide-programming)
- [Using Arduino CLI](#using-arduino-cli)
- [Using PlatformIO](#using-platformio)
- [Using FTDI](#using-ftdi)
- [Hardware Considerations](#hardware-considerations)

## Getting Started

1. Connect to the WiFi network **WVR** with the password **12345678**.
2. Open Google Chrome or another browser that [supports Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API).
3. Navigate to `http://192.168.5.18/` to open the WVR UI.

![WVR GUI](https://github.com/marchingband/wvr_hardware/blob/main/images/gui_sounds.png)

## Powering WVR

- **WVR Basic**: 
  - Plug in USB.
  - Alternatively, apply 5V and ground or 3.3V and ground to the power pins.
  
- **WVR Makers Board**: 
  - Plug in USB (this will not power the amp).
  - Use a center-negative 9V PSU (Boss style).
  - Alternatively, apply between 6V and 9V (and ground) to the VIN pins.

- **WVR Dev Board**: 
  - Plug in USB.
  - Use a center-negative 9V PSU (Boss style).
  - Alternatively, apply between 6V and 9V (and ground) to the VIN pins.

- **Thames**: 
  - Use a center-negative 9V PSU (Boss style).

- **USB Host Backpack**: 
  - The backpack is powered by the WVR; if the WVR is on, the backpack is also on.
  - When updating firmware on the backpack, plug into the USB micro port on the backpack **instead of** powering the WVR.

## Updating Firmware

1. Create a folder on your computer to store firmwares for your WVR.
2. Download the firmwares, saving them to this new folder.
3. Navigate to the [WVR Binaries GitHub Repository](https://github.com/marchingband/wvr_binaries) and find the folder for your board type.
4. Download the `.ino.bin` file for the newest binary (currently v3.0.0).
5. Apply power to your WVR.
6. Connect to the WiFi network **WVR** using the password **12345678**.
7. Open Google Chrome or another browser that [supports the Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API).
8. Navigate to `http://192.168.5.18/` to open the WVR UI.
9. Click on the **Firmware** menu item at the top.
10. Click **Select Binary** for **Slot 0** and upload the downloaded firmware.
11. (Optional) To give the binary a custom name, click its name on the left.
12. Click **Upload** for **Slot 0** and wait for the upload to complete.
13. Click **Boot** for **Slot 0** and wait for the boot to complete.
14. Reset the WVR, reconnect to the WiFi network, and reload the webpage.
  
For WVR units with a USB Host Backpack, follow [these instructions](https://github.com/marchingband/wvr_usb_backpack) to update the firmware.

Congratulations, you now have the most up-to-date firmware on your WVR!

![WVR GUI Firmware](https://github.com/marchingband/wvr_hardware/blob/main/images/gui_firmware.png)

## Playing Sounds

1. Open the WVR UI and click on a note, for example, E2.
2. Click **Select File** to open a window and choose a sound file from your computer.
3. Use **Audition** to preview the sound through your computer speakers.
4. Navigate to the **Pins** configuration page.
5. Click on a pin, like **D2**, to view its options.
   - Set the **Note** to **E2 (40)**.
   - Set the **Edge** to **Falling**.
   - Configure the **Debounce Time** based on your setup.
6. Some pins offer a touch/digital option. Configure this if necessary.
7. Click on **Action** to view or set what the pin can trigger.
8. Set **Velocity** to control the playback volume for events on this pin.
9. Click **Sync** to upload your configurations and wait for completion.
10. Connect headphones or line out to the WVR.
11. Trigger the sound by connecting the **GND** pin to **D2**.
12. Reset the WVR to apply changes after syncing.

![WVR GUI Pins](https://github.com/marchingband/wvr_hardware/blob/main/images/gui_pins.png)

## MIDI Control

WVR responds to the following MIDI events:
- Note On
- Note Off
- Program Change
- Various CC controls, like volume, panning, and expression.

1-byte SYSEX commands are also supported for global controls such as turning WiFi on or off.

## Web MIDI

1. Make sure your IAC Driver is online and configured in your DAW.
2. Configure Google Chrome to trust the WVR by adding it to the exceptions list.
3. In the WVR Web UI, refresh the Web MIDI settings to see the IAC Driver.
4. Your DAW should now stream MIDI data wirelessly to the WVR.

![WVR GUI Global](https://github.com/marchingband/wvr_hardware/blob/main/images/gui_global.png)

## Understanding Priority

WVR can play up to 18 stereo sounds simultaneously. If more sounds are triggered, WVR uses an algorithm to manage playback. You can control this behavior by setting sound **Priority**:
- Lower priority sounds can be halted to play equal or higher priority sounds.
- If all 18 slots are filled with high-priority sounds, a lower priority sound will not play.

## Understanding Exclusive Group

The **Exclusive Group** feature ensures that only one sound from a designated group plays at any given moment. This is useful for mutually exclusive sounds like open and closed hi-hats:
- Assign sounds to the same exclusive group number to make them mutually exclusive.
- Triggering a new sound in the group will immediately stop any currently playing sound in that group.

## Understanding Playback Mode

WVR offers different playback modes:
- **One-shot**: The sample plays once and stops.
- **Loop**: The sample loops until receiving a note-off signal.
- **ASR-loop**: The sample has more complex looping behavior, looping between specific points until a note-off signal is received.

Note: Loop start and end points are in *samples*. Be cautious with your calculations depending on your DAW and original sample format.

## Understanding Response Curve

MIDI notes come with a velocity value ranging from 0 to 127, which is translated to a playback volume. WVR allows you to set the **Response Curve** for this translation:
- **Linear**: A straight-line relationship between velocity and volume.
- **Square Root**: The default curve, considered more musical by some.
- **Logarithmic**: Another non-linear curve option.

Choose the curve that suits your musical needs.

## Understanding Retrigger Mode

A "retrigger" occurs when a sound is triggered again while already in playback. WVR offers various ways to handle this:
- **Note-off**: Stops the sound.
- **Restart**: Restarts the sound from the beginning.
- **Ignore**: Ignores the second trigger.
- **Retrigger**: Starts new playback without stopping the first.

## Understanding Note Off

A "note-off" event is triggered when a key is lifted on a piano or when a pin on WVR goes from LOW to HIGH. You have two options:
- **Ignore**: Ignores the note-off event.
- **Halt**: Quickly fades out the sound and stops it.

## Using Racks

Racks enable multi-sample functionality. Instead of modulating volume based on velocity, the engine plays different samples that reflect lighter or heavier touches. To create a rack:
1. Click **Create Rack** and name it.
2. Specify the **Number of Layers** (changing this later will erase data).
3. Set "break points" for each sample layer to define velocity ranges.

Note: Effects applied in Rack mode affect all layers.

## Bulk Uploading Files

To bulk upload files, use **Shift-Click**, **Command-Click**, or **Ctrl+A** to select notes or racks. Click **Select Files**, and you can choose multiple files, which will be sorted alphanumerically and placed in your selected notes.

## Bulk Uploading Racks

To bulk upload racks, **Shift-Click** on **Select Files** with a region of notes selected. A file dialog will allow you to pick a directory. The directory must contain sub-folders, each representing a rack. The sub-folder names become the rack names. Each sub-folder must contain all files for its rack. Files and folders are sorted alphanumerically. Exceptions:
- A folder with a single file becomes a single sample.
- A folder with only `empty.txt` will leave the note empty.

## Save and Load Voice Configuration

- **Shift-Click** on a voice button (1-16) to download its config as a `.json` file.
- **Shift-Alt-Click** on a voice button to upload a `.json` file, setting that voice's config.

## Pitch Interpolation

To interpolate pitch across a range of notes:
1. Select the notes.
2. **Shift-Alt-Click** on one note to set it as the **Pitch Interpolation Target**.
3. Click **Select File** and choose one file.
4. The target maintains its pitch; other notes are pitched in relation.

## Pitch Interpolating a Rack

Follow the above pitch interpolation steps but select multiple files to create a rack. The rack will be applied to all selected notes and pitch-shifted like regular pitch interpolation.

## Pitch Interpolating an ASR Loop

### Overview

When using pitch interpolation with an ASR Loop sample, it's necessary to interpolate the `Start` and `End` values. This is because the file size and the samples scale according to the pitch.

### How To

- Use **shift-click** and **shift-alt-click** to select a range and an interpolation target.
- Enter the `Start` and `End` values for the target sample. Interpolated values for the rest of the range will be automatically calculated.

---

## Using FX

### Overview

WVR uses the browser's built-in audio engine for sample preparation and adds various FX like Distortion, Reverb, Pitch Shift, Panning, and Volume.

### Considerations

- FX are hard-coded into the sample.
- To change FX, reselect the original sound file, modify FX settings, and hit SYNC again.
- Use the **audition** button to preview FX.

---

## Global Settings

### Overview

Access global settings by clicking the blue **WVR** button at the top center of the UI.

### Options

- **Global Volume**: Control the overall output volume.
- **Recovery Mode**: Experiment with firmwares safely.
- **Log Verbosity**: Control logging details.
- **WiFi Settings**: Manage WiFi network, password, and signal strength.
- **eMMC Management**: Options for backup, restore, and reset.

---

## Firmware Manager

### Overview

WVR can store up to 10 different firmwares.

### How To

- Use **select binary** to choose a firmware file.
- Rename your firmware for easy identification.
- Click **upload** and refresh the browser.
- Click **boot** and wait for the firmware to boot.

### Important Note

Firmware compatibility is crucial. Follow the versioning guidelines to avoid losing data.

## Setting Up for Arduino IDE Programming

### Warning

:warning: **Do not upload your own custom code to WVR without a working USB-FTDI module setup.** If your code has bugs, WiFi won't launch and your WVR will be bricked until you get a USB-FTDI module.

### Steps for Arduino IDE Setup

1. **Install Arduino IDE**: Download the latest version.
2. **ESP32 Installation**: Follow [these instructions](https://github.com/espressif/arduino-esp32).
3. **Board Version**: Select version `2.0.8` in the Arduino Boards manager.
4. **WVR Arduino Library**: Download from [GitHub](https://github.com/marchingband/wvr/releases/tag/v3.8.3) and unzip into `Arduino/libraries/WVR/`.
5. **Install Libraries**: Use the Arduino library manager to install **ADAFRUIT NEOPIXEL**.
6. **Additional Libraries**: Download [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer) and [AsyncTCP](https://github.com/me-no-dev/AsyncTCP) and unzip into the `libraries` folder.
7. **ESP Exception Decoder**: Recommended for decoding stack traces from the serial monitor.
8. **Restart Arduino IDE**: Make sure all changes are applied.

### Running Your First Program

1. Go to `File` -> `Examples`, and under **WVR**, open **wvr_basic**.
2. Save this as a new sketch.
3. Compile the binary.
4. Join the **WVR** WiFi network and upload your firmware.

---

## Using Arduino CLI

### How To

1. **Install the Arduino CLI**: Follow the official documentation.
2. **Compile Your Sketch**: Use the `arduino-cli compile` command with your sketch name.
3. **Join WVR WiFi**: Connect to the network for flashing.

### Flashing Firmware

- Use `curl` to flash your compiled binary to WVR.
  
  ```bash
  curl --data-binary "@/path/to/your_binary.ino.bin" http://192.168.5.18/update --header "content-type:text/plain"
  ```
  
### Additional Options

- Check `wvr.sh` in the WVR Arduino library for more ideas and commands.

## Using PlatformIO

### Configuration

Set up your `platformio.ini` file with the following configuration:

```ini
[env:esp-wrover-kit]
platform = espressif32@6.2.0
framework = arduino
board = esp-wrover-kit
lib_deps =
    https://github.com/marchingband/wvr.git
    https://github.com/me-no-dev/ESPAsyncWebServer.git
    https://github.com/me-no-dev/AsyncTCP.git
    adafruit/Adafruit NeoPixel@^1.11.0
build_flags = -DBOARD_HAS_PSRAM -mfix-esp32-psram-cache-issue
monitor_speed = 115200
# upload_port = /dev/cu.usbserial-A50285BI
```

### Creating Main.cpp

1. Create a file named `main.cpp`.
2. Copy the content from one of the example files into `main.cpp`.
3. Add `#include <Arduino.h>` at the top of `main.cpp`.

This sets you up for working with PlatformIO and the specified board and libraries.

## Using FTDI

### Required Hardware

You'll need a USB-to-FTDI module like this one: [Adafruit's USB-to-FTDI Module](https://www.adafruit.com/product/3309).

### Connection Instructions

1. Connect **D0** to **RX** on the FTDI module.
2. Connect **D1** to **TX** on the FTDI module.
3. Connect **GND** to **GND** on the FTDI module.
4. Open the example sketch `examples/wvr_ftdi`. In this sketch, you'll find `wvr->useFTDI = true`.

### Booting into FTDI Mode

1. Ground **D6** and the small copper pad labeled "boot" next to the eMMC on the WVR.
2. Press the reset button on the WVR.
3. Release **D6** and the "boot" pad.

You should now see `waiting for download` if you have a serial monitor attached to the WVR. Use the **UPLOAD** button in the Arduino IDE to flash your code. After flashing, restart the WVR.

### Monitoring

Open the Arduino Serial Console to view logs from the WVR boot process. Alternatively, you can use `./wvr.sh ftdi` for flashing and any Serial monitor app to get logs from the WVR.

## Hardware Considerations

### Important Pins

* **Pin D6**: Acts as a strapping pin for the ESP32, corresponding to **GPIO_0**. Cannot be disabled and if held LOW during boot, will enter bootloader mode.
* **Pins D6 and D13**: Connected to **ADC peripheral 2**, which is shared with the WiFi radio. ADC readings may be inconsistent when WiFi is active.
* **Pins D7, D8, D9, and D10**: These are input-only pins. No internal pullups are available. Use external pullups when necessary.

Note: Calling `digitalWrite()` on input-only pins will have no effect.
