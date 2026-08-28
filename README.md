## Keymap

Below representation was generated with [`keymap-drawer`](https://github.com/caksoylar/keymap-drawer) – check out the automatically generated layouts using the [automated Github workflow](https://github.com/caksoylar/keymap-drawer/tree/main#setting-up-an-automated-drawing-workflow) for each keyboard in the [`keymap-drawer` folder](keymap-drawer/), which is always up to date with the config.

![Keymap Representation](./keymap-drawer/toledo.svg?raw=true "Keymap Representation")

## Layout

This keyboard runs as a **dongle** setup: a third XIAO BLE acts as the central and
both halves connect to it as peripherals. See [`build.yaml`](build.yaml) for the
three firmware targets.

To go back to a dongle-less keyboard (left half as central), remove the
`cmake-args` lines from `build.yaml`, rebuild, and redo the reset procedure below.

## Keymap edit

#### Option 1. Keymap Editor

1. Open [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/).
2. Connect it to your Github account and give an access to your repository to Keymap Editor's app.
3. Make changes to your keymap and press `Save` - it will trigger software build. Wait for it to complete.
4. Grab the `firmware.zip` archive.

#### Option 2. Manual

1. Make changes to the [toledo.keymap](config/toledo.keymap) file using your favorite text editor.
2. Commit changes to your repository.
3. Go to `Actions` tab in your Github repository, locate the latest build and wait for it to complete.
4. Grab the `firmware.zip` archive

### How to flash the keyboard?

1. Obtain `firmware.zip`
2. Unzip `firmware.zip` - you should have these files:
   - `toledo_dongle-xiao_ble_nrf52840_zmk-zmk.uf2`
   - `toledo_left-xiao_ble_nrf52840_zmk-zmk.uf2`
   - `toledo_right-xiao_ble_nrf52840_zmk-zmk.uf2`
   - `settings_reset-xiao_ble_nrf52840_zmk-zmk.uf2`
3. Turn off the power for the selected part (move slider to position `OFF`)
4. Connect the selected part to the PC via USB-C cable
5. Press `RESET` button **twice** to enter DFU mode - you should see new USB device in your file manager
6. Copy the corresponding firmware to the root directory of the new USB device
7. Disconnect the selected part from the PC
8. Repeat steps 3-7 for the other parts

### How to pair the halves to the dongle?

Bonding information is **not** cleared by flashing normal firmware, so any old
pairing from a previous setup has to be wiped first.

1. Flash `settings_reset` to **all three** devices (dongle, left, right), following the steps above
2. Flash the real firmware to each device: `toledo_dongle` to the dongle, `toledo_left` to the left half, `toledo_right` to the right half
3. Plug the dongle into the host via USB
4. Turn on the power for both halves (move slider to position `ON`)
5. They will find the dongle and pair automatically

Note that the keyboard does not work without the dongle - the halves are
peripherals and cannot connect to a host on their own.

### Problems

#### I'm getting File Transfer Error after copying firmware to the keyboard

It's OK. Proof: https://zmk.dev/docs/troubleshooting#file-transfer-error
