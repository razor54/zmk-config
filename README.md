# Corne ZMK Configuration

This repository contains my ZMK firmware configuration for the Corne keyboard (also known as Crkbd), a popular split ergonomic mechanical keyboard with 42 keys.

## Keyboard Layout

Below is a visual representation of my keyboard layout including all layers:

![Corne Keyboard Layout](./corne_keymap.svg)

## Features

- **Default Layer (0)**: QWERTY layout with home row mods (GACS) - tap rightmost thumb key to toggle Gallium layer
- **Gallium Layer (1)**: Alternative ergonomic layout - tap rightmost thumb key to return to Default layer
- **Colemak Layer (2)**: Colemak layout with home row mods - accessible via Lower layer (hold left thumb, press to2)
- **Colemak-DH Layer (3)**: Colemak Mod-DH layout with home row mods - accessible via Lower layer (hold left thumb, press to3)
- **Lower Layer (4)** (hold left thumb key): Numbers, bluetooth controls, arrow keys, and base layer switching
  - Bottom row includes quick access to switch between base layers: Default (to0), Gallium (to1), 5-Col (to8), Colemak (to2), and Colemak-DH (to3)
- **Raise Layer (5)** (hold right thumb key): Symbols and special characters
- **Symbol Layers (6-7)**: Additional symbol layers for advanced punctuation
- **5-Column QWERTY (8)**: 5-column QWERTY layout for 5-column keyboard simulation
- **5-Column Lower/Raise (9-10)**: Number and symbol layers for 5-column layout
- **Combos**: Escape using Q+W, and Caps Word using both inner thumb keys

**Layer Priority**: Utility layers (Lower, Raise, Symbol) have higher layer numbers (4-10) than base layers (0-3), ensuring they can override keys on the base layers when activated.

## Home Row Mods

The home row keys function as modifiers when held:

- A: Left Meta (GUI)
- S: Left Alt
- D: Left Shift
- F: Left Control
- J: Right Control
- K: Right Shift
- L: Right Alt
- ;: Right Meta (GUI)

## Bluetooth Support

The Lower layer provides Bluetooth controls:

- BT CLR: Clear Bluetooth connections
- BT 0-4: Switch between paired devices

### Dongle Configuration

This repository includes a dongle build configuration that allows using a central controller to connect to both keyboard halves. The dongle configuration includes:

- **Bluetooth Name**: Set to "Nice_Dongle" in the configuration
- **Display Timeout**: Display will turn off after 1 minute of inactivity (configurable in `boards/shields/corne/corne_dongle_pro_micro.conf`)
- **Deep Sleep**: Disabled to ensure the dongle always wakes up on key press from the keyboard halves (increases power consumption on battery, no impact when USB-powered)

**Important**: If your dongle shows the wrong Bluetooth name (e.g., "eyeslash_sofle" from factory settings), you need to flash the `settings_reset` firmware first to clear the stored settings, then flash the dongle firmware again. The settings_reset firmware is automatically built by GitHub Actions.

## Building and Flashing

To build and flash this firmware:

1. Fork this repository
2. Make your changes to the configuration files
3. GitHub Actions will build the firmware automatically
4. Download the firmware files from the Actions tab
5. Flash your keyboard using the appropriate method for your controller

## Customizing

To customize this layout for your own use, modify the following files:

- `config/corne.keymap` - Edit the keymap
- `config/corne.conf` - Adjust keyboard settings

For more information on ZMK configuration, visit the [ZMK Documentation](https://zmk.dev/docs).

## Generating the Layout Image

To visualize your keymap, you can use the [keymap-drawer](https://github.com/caksoylar/keymap-drawer) tool.

### 1. Install keymap-drawer

You need Python 3.7+ and pip installed. Then run:

```bash
pip install keymap-drawer
```

### 2. Generate the YAML keymap

```bash
keymap parse -c 10 -z ./config/corne.keymap > corne_keymap.yaml
```

### 3. Draw the SVG layout

```bash
keymap draw corne_keymap.yaml > corne_keymap.svg
```

The resulting `corne_keymap.svg` will be a visual representation of your keyboard layout.
