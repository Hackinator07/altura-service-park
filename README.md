# Altura Service Park

Web-based firmware flasher for the Altura Rally Computer. Runs entirely in the browser — no software installation required.

**Live:** https://Hackinator07.github.io/altura-service-park

---

## Requirements

- Google Chrome or Microsoft Edge (desktop only)
- Web Serial API support (enabled by default in Chrome/Edge)
- Altura hardware connected via USB

---

## Supported Targets

| Target | Folder | Description |
|--------|--------|-------------|
| CYD | `firmware/cyd/` | Open source build · Cheap Yellow Display · NEO-6M |
| Base | `firmware/base/` | Standard rally computer firmware |
| Base + IMU | `firmware/base-imu/` | Base with inertial measurement |
| NEO-M8 | `firmware/neo-m8/` | Precision GPS build |
| NEO-M8 + IMU | `firmware/neo-m8-imu/` | NEO-M8 with IMU |
| Reckoner | `firmware/reckoner/` | Dead-reckoning navigation build |

---

## Updating Firmware

1. Replace the `.bin` files in the appropriate `firmware/<target>/` folder
2. Update `firmware.json` in that folder with the new version string
3. Commit and push — GitHub Actions deploys automatically

### firmware.json format

```json
{
  "version": "v1.0.75-NeoGPS",
  "files": [
    { "offset": "0x1000",  "file": "bootloader.bin" },
    { "offset": "0x8000",  "file": "partitions.bin" },
    { "offset": "0xE000",  "file": "boot_app0.bin" },
    { "offset": "0x10000", "file": "app.bin" }
  ]
}
```

### Finding your .bin files

After a PlatformIO build, the files are in `.pio/build/esp32dev/`:

| PlatformIO output | Rename to |
|-------------------|-----------|
| `bootloader.bin` | `bootloader.bin` |
| `partitions.bin` | `partitions.bin` |
| `firmware.bin` | `app.bin` |

`boot_app0.bin` is at:
`~/.platformio/packages/framework-arduinoespressif32/tools/partitions/boot_app0.bin`

---

## Local Development

No build step required. Open `index.html` directly in Chrome, or serve with any static file server:

```bash
npx serve .
```

---

## License

Altura Rally Computer © Jason Hack & Eli Goethel. All rights reserved.
