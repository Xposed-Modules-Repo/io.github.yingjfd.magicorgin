# MagicOriG

Let a third-party SPP earbud (**NickHCK YuanDao OriG in**) behave like a first-party Honor
earbud on MagicOS — adjust ANC and see per-ear battery right in the **device center**, and
switch ANC from a Quick Settings tile.

> ⚠️ This project is generated and maintained by AI under human direction, including all
> reverse engineering and hook code. Use at your own risk.

## Features

| Feature | Description |
| --- | --- |
| **Device-center ANC** | Pull down the control center → drag **Device Center** to the main bar → tap the bud ball → **ANC / Pass-through / Off** buttons. Every tap goes down the verified SPP link (~50 ms) |
| **Per-ear battery** | The device-center card shows independent **L / R** battery bars |
| **Quick Settings tile** | Add the MagicOriG tile to cycle the three ANC gears |
| **Notification battery** | The audio-switch notification shows `原道 OriG in / 左耳 x% 右耳 x%` |
| **Auto-clear** | The notification is cancelled when the earbud disconnects |

## Requirements

- Honor MagicOS 10.0+ (Android 16+)
- KernelSU / Magisk + LSPosed (Zygisk, API 101+)
- NickHCK YuanDao OriG in earbud

## Usage

1. Install the APK, enable the module in LSPosed and select the scopes listed below.
2. Soft-reboot (`su -c 'setprop ctl.restart zygote'`) or reboot the device.
3. Connect the earbud.

## Scopes

| Package | Purpose |
| --- | --- |
| `com.android.bluetooth` | SPP dispatch and status queries |
| `com.android.systemui` | Notification text rewrite, Quick Settings tile |
| `com.hihonor.audioaccessorymanager` | Honor earbud service compatibility |
| `com.hihonor.imedia.sws` | Battery on the audio-switch notification |
| `com.hihonor.controlcenter` | **Device center**: ball list, service card, ANC buttons, per-ear battery. ⚠️ This scope must be checked **once in the LSPosed manager UI** (editing the config file alone does not work) |

## ANC gears

| Button | Protocol | SPP frame |
| --- | --- | --- |
| ANC | Experimental ANC (default gear) | `4E 05 00 00 01 02 10 00` |
| Pass-through | ANC_TRANSPARENT | `4E 05 00 00 01 02 01 00` |
| Off | ANC_OFF | `4E 05 00 00 01 02 00 00` |

## Notes

- This module is MagicOS-specific (Honor). On other ROMs the hooks silently miss and
  nothing breaks.
- The Bluetooth settings page is left untouched (stock behavior): the module only adds
  the device-center entry, the Quick Settings tile and the notification battery.

## Source

Full source, build instructions and the ANC-chain write-up:
https://github.com/yingjfd/MagicOriG
