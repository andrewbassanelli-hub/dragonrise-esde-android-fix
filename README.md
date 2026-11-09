# DragonRise 0079:0006 — ES-DE Android controller workaround

**Tested and documented by Andrew Bassanelli** · 8 November 2026 · [Português](LEIA-ME-PTBR.md)

> **Scope:** This is a tested workaround on **one Android arcade-cabinet setup**, not a universal fix for all DragonRise 0079:0006 controllers. It is **not** an official ES-DE or SDL patch.

## Tested environment

| Component | Tested setup |
| --- | --- |
| Device | Samsung Galaxy Tab S4 |
| OS | Android (exact OS build not documented in this report) |
| Frontend | ES-DE 3.5.0-65 (r52) |
| SDL version reported by ES-DE | 2.32.10 |
| Controller | DragonRise Inc. / PC TWIN SHOCK Gamepad |
| USB VID:PID | `0079:0006` |
| Connection/use | USB arcade joystick + six physical arcade buttons |

## Problem observed

- An Android gamepad testing app and RetroArch registered inputs from the controller.
- ES-DE initially did **not** recognize the device as a controller.
- The ES-DE startup log showed `Added keyboard with default configuration`, without a corresponding controller-addition entry.

## Working configuration

Download [`es_controller_mappings.cfg`](es_controller_mappings.cfg), or create a plain-text file containing exactly this line:

```text
default,DragonRise Arcade Android Buttons Test,a:b20,b:b21,x:b22,y:b23,back:b24,start:b25,dpup:b11,dpdown:b12,dpleft:b13,dpright:b14,leftx:a0,lefty:a1,platform:Android,
```

**Important:** This uses SDL's `default` mapping key rather than a device-specific controller GUID. It is a **broad fallback** and could affect other currently-unmapped controllers. Do not apply it blindly to unrelated setups.

## Installation

1. Fully close ES-DE.
2. Locate your ES-DE **user data folder** on Android (the folder named `ES-DE`; its storage location may vary).
3. Open or create its `controllers` subfolder.
4. Back up any existing `es_controller_mappings.cfg`.
5. Copy the supplied file to `ES-DE/controllers/es_controller_mappings.cfg`, relative to the ES-DE user data folder. Keep the exact filename.
6. Restart ES-DE and test the joystick and all six buttons in the frontend.
7. If behavior is wrong or other input devices are affected, close ES-DE, remove the test file, and restore any backed-up file.

No root or background remapping app was required in the tested setup. This changes **ES-DE frontend input**, **not** emulator/core button mappings.

## Observed result

After installing the file and restarting ES-DE, the arcade joystick and six physical arcade buttons worked in the ES-DE interface on the Samsung Galaxy Tab S4 setup described above.

## Limitations

- **Single-device confirmation only.** Different DragonRise boards can share USB ID `0079:0006` while using different wiring or input indices.
- Android button indices `b20`–`b25` are specific to the tested setup.
- Other Android releases, ES-DE versions, SDL releases, devices, or encoder boards are **untested**.
- Working in the ES-DE interface does not establish that games and emulators work without separate mapping.
- The `default` mapping can affect other previously-unmapped controllers.

## Technical context

- [ES-DE official installation documentation](https://gitlab.com/es-de/emulationstation-de/-/blob/master/INSTALL.md)
- [ES-DE FAQ](https://gitlab.com/es-de/emulationstation-de/-/blob/master/FAQ.md)
- [SDL community discussion of DragonRise 0079:0006 layouts](https://discourse.libsdl.org/t/duplicated-conflicting-guids-for-the-dragonrise-pc-twin-shock-controllers/24112)

These are background references, not independent validation of this exact Android workaround.

## Feedback

If you test the workaround, please share your exact device, Android version, ES-DE and SDL versions, USB VID:PID, buttons/axes, and result. Negative tests are also valuable.

## Optional support

If this workaround helped you, consider [supporting my independent testing through Wise](https://wise.com/pay/me/andrewb8447). Donations are completely voluntary; this guide and mapping are free to use.

**Credit:** Andrew Bassanelli — tester and author of this documented workaround. This is an independent community report, unaffiliated with ES-DE or SDL.
