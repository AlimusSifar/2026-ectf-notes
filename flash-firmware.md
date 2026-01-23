# Flashing Firmware

> *Note: The target device (MSPM0 LITO L2228 / MSPM0 L2228 LaunchPad) must be in the update mode to flash the firmware. Follow the [Bootloader Setup](bootloader-setup.md) instructions to enter update mode.*

## Step 1: Erase Previous Firmware

Use the following command to erase any previous firmware on the device:

```bash
uvx ectf hw COM3 erase
```

## Step 2: Flash New Firmware

Use the following command to flash the new firmware onto the device:

```bash
uvx ectf hw COM3 flash .\build\hsm.bin -n hsm
```

## Step 3: Start the Device

After flashing, start the device with the following command:

```bash
uvx ectf hw COM3 start
```

## Step 4: Verify the Firmware

To verify that the firmware has been successfully flashed, use the following command:

```bash
uvx ectf tools COM3 list <HSM_PIN>
```

---

Next: [Available Flags](flags.md)
