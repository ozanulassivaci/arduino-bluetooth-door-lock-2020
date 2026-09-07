# Arduino Bluetooth Door Lock

A 3D-printed, Arduino-controlled door lock that opens with a keypad
PIN or remotely from an Android app over Bluetooth.

## Features

- 4x4 keypad PIN entry with LCD feedback and a wrong-password lockout
- Servo-driven bolt mechanism
- Optional Bluetooth (HC-05/HC-06) variant controlled from a companion
  Android app
- Buzzer feedback for accepted/rejected codes
- Manual override switches for opening/closing from inside
- 3D-printed enclosure and a separate 3D-printed sliding door bolt,
  with a custom-modified rail/receiver

## Tech stack

- Arduino Uno
- 4x4 matrix keypad
- SG90 9g servo motor
- I2C LCD (16x2 or 20x4 depending on the variant)
- HC-05/HC-06 Bluetooth module (Bluetooth variant only)
- Android app (Bluetooth variant only)
- PLA 3D-printed parts

## Installation and usage

1. Wire the components as shown in [`hardware/wiring_diagram.png`](hardware/wiring_diagram.png).
2. Open one of the sketches in the Arduino IDE:
   - [`src/keypad_lock/keypad_lock.ino`](src/keypad_lock/keypad_lock.ino) — keypad only
   - [`src/keypad_bluetooth_lock/keypad_bluetooth_lock.ino`](src/keypad_bluetooth_lock/keypad_bluetooth_lock.ino) — keypad + Bluetooth
3. Install the required libraries via Library Manager: `LiquidCrystal_I2C`, `Keypad`, `Servo`.
4. Update `mot_min`/`mot_max` to match your servo's locked/unlocked angles, and change the hardcoded PIN (search for `Str[6]` in the `if` condition) before real use — the default in this repo is a demo value.
5. Upload to the Arduino Uno.
6. (Bluetooth variant) Install [`android-app/door-lock-remote.apk`](android-app/door-lock-remote.apk) on an Android phone and pair it with the HC-05/HC-06 module.
7. Print the enclosure and bolt parts from [`models/`](models/) — see print settings in each model's `reference/thingiverse_README.txt`.

## Project structure

```
src/                     Arduino sketches
  keypad_lock/           keypad-only variant
  keypad_bluetooth_lock/ keypad + Bluetooth variant
android-app/             companion Android app (compiled build only)
hardware/                wiring diagram and a photo of the assembled prototype
models/
  keypad-case/           3D-printed enclosure (based on ELECTRONOOBS's design)
  sliding-bolt/
    original/            stock sliding bolt STLs (Sagittario's design)
    custom/              rail/receiver STLs modified for this build
```

## Credits

This project builds on two Thingiverse designs and a YouTube tutorial;
the sections below credit each source and note what was changed.

- **Enclosure and base Arduino code**: [KeyPad Door lock Arduino servo](https://www.thingiverse.com/thing:2422074)
  by [ELECTRONOOBS](https://www.youtube.com/electronoobs), licensed
  [CC BY 3.0](models/keypad-case/reference/LICENSE_CC-BY-3.0.txt). The
  enclosure STLs in `models/keypad-case/` are used as designed. The
  Arduino sketches in `src/` are adapted from ELECTRONOOBS's tutorial
  code, with changes to the LCD type/size, pin configuration, and (in
  the Bluetooth variant) added Bluetooth serial control.
- **Sliding door bolt**: [Sliding Door bolt Print fully assembled](https://www.thingiverse.com/thing:1596180)
  by Sagittario, licensed
  [CC BY-SA](models/sliding-bolt/original/reference/LICENSE_CC-BY-SA.txt).
  The stock files are in `models/sliding-bolt/original/`. The rail and
  receiver were redesigned for this build; those modified files are in
  `models/sliding-bolt/custom/` and, per the share-alike license, are
  also distributed under CC BY-SA.
- **Android app**: based on ELECTRONOOBS's companion Bluetooth control
  app, modified for this build. Only the compiled APK is included —
  the original source project could not be located.

## License

The project documentation, Arduino sketch adaptations, and this
repository's organization are licensed under the [MIT License](LICENSE).
The third-party assets listed under Credits remain under their
original licenses (CC BY 3.0 / CC BY-SA), which take precedence over
the MIT license for those specific files.

## Note

This project was a simple self-study exercise I built in high school
(2020) to develop my computer/programming skills through courses I was
taking at the time. It was reorganized and cleaned up in 2026 for
public release.

> 📝 TODO: add the course/resource that inspired this project
