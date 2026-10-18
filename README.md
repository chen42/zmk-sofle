# Eyelash Sofle (personal ZMK config)

My ZMK firmware for the Eyelash Sofle wireless split keyboard (nice!nano v2 in each half).
Forked from [a741725193/zmk-sofle](https://github.com/a741725193/zmk-sofle); the keymap is
ported from the Vial layout of my other split keyboard.

## Keymap

Each half has 6 columns and 5 thumb keys; the left half also has a rotary encoder, and the
middle has a 5-way joystick. Keymap source: [`config/eyelash_sofle.keymap`](config/eyelash_sofle.keymap).

### Layer 0 (base)

```
Esc    1  2  3  4  5     [↑]      6  7  8  9  0  Bksp
Tab    Q  W  E  R  T     [↓]      Y  U  I  O  P  '
LShift A  S  D  F  G     [←]      H  J  K  L  ;  Enter
LCtrl  Z  X  C  V  B     [→]      N  M  ,  .  /  RShift
(enc:Mute) ScrLk ` LAlt Space L1  [Enter]  L1 Space RAlt L2 MidClick
```

- Encoder turns adjust volume; pressing it mutes.
- Scroll Lock triggers voxtype (voice typing).

### Layer 1 (hold L1): symbols and navigation

| Key   | Output | Key   | Output |
|-------|--------|-------|--------|
| Esc   | `~`    | H J K L | ← ↓ ↑ → |
| E     | `=`    | N M , . | Home PgDn PgUp End |
| R / T | `[` `]` | Y / U | `{` `}` |
| D     | `-`    | I     | `\|`   |
| C     | `_`    | P     | `+`    |
| B     | `#`    | /     | `\`    |
| Encoder press | RGB toggle | Bksp | Delete |

The joystick moves the mouse pointer on this layer, and pressing it left-clicks.

### Layer 2 (hold L2): numpad and system

- Right half numpad (needs Num Lock on): `7 8 9` on U I O, `4 5 6` on J K L,
  `0 1 2 3` on N M , ., `-` on Y, `+` on P, `,` on ;, `.` on /.
- Left half:

| Key | Action |
|-----|--------|
| 1–5 | Select Bluetooth profile 0–4 |
| Q   | Clear current profile's pairing |
| W   | Clear all pairings |
| A / S | Output to USB / Bluetooth |
| Z   | Reset |
| C   | Enter bootloader (flash mode) |

### Combo

- Hold **Q + S + Z** for 2 seconds: soft off (deep sleep). Press the reset button to wake.

## Building

Pushing to `main` builds the firmware with GitHub Actions. Download the **firmware**
artifact from the run in the Actions tab. It contains:

- `eyelash_sofle_left nice_view-nice_nano_v2-zmk.uf2` (left half, with ZMK Studio)
- `eyelash_sofle_right nice_view-nice_nano_v2-zmk.uf2` (right half)
- `settings_reset-nice_nano_v2-zmk.uf2`

## Flashing

Flash one half at a time with only that half connected over USB (turn the other off):

1. Double-tap the reset button quickly; a `NICENANO` drive appears.
2. Copy that half's `.uf2` file onto it. The half reboots when done.

After flashing both halves, press reset on both at the same time so they re-pair.

### Settings reset

If the keyboard behaves strangely (wrong keymap, stuck modifiers, halves not pairing),
flash `settings_reset` to each half first, then that half's normal firmware. This wipes
Bluetooth pairings and any ZMK Studio changes, so remove the keyboard from your computers'
Bluetooth lists and pair again afterwards.

## ZMK Studio

Studio works over USB on the left half. Changes made in Studio are stored on the keyboard
only and are lost on a settings reset; Studio has no export. Copy any change you want to
keep into `config/eyelash_sofle.keymap`.

On Linux, add your user to the `uucp` group (Arch) so Studio can open the serial port.
On Wayland with NVIDIA, set `WEBKIT_DISABLE_DMABUF_RENDERER=1` if Studio fails with
"Error 71 (Protocol error)".

## Hardware notes from the original maker

- Contact for 3D model files or hardware problems: [380465425@qq.com](mailto:380465425@qq.com)
- `sofle-3D-MODEL.zip` contains the case model.
