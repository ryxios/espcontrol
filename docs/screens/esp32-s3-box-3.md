---
title: Espressif ESP32-S3-BOX-3
description:
  EspControl on the Espressif ESP32-S3-BOX-3 — a compact 2.4-inch 320x240 touchscreen with 4 cards, powered by ESP32-S3.
---

# Espressif ESP32-S3-BOX-3

The **Espressif ESP32-S3-BOX-3** is a compact ESP32-S3 development kit with a 2.4-inch 320×240 touchscreen, native USB-C serial/JTAG, onboard audio hardware, and expansion connectors. EspControl uses the display, GT911 touch controller, backlight, and physical buttons defined by Espressif's BSP.

::: warning Experimental support
This profile is based on Espressif's `esp-box-3` BSP at commit `8d403e718188a25811e869fdafe613b36dd09007`. Audio, SD card, IMU, and PMOD expansion are intentionally not enabled in EspControl yet because the project does not currently expose stable abstractions for those features.
:::

## Specifications

| | |
|---|---|
| **Display** | 2.4-inch 320×240 LCD |
| **Touch** | Capacitive GT911 touch controller |
| **Processor** | ESP32-S3, dual-core Xtensa LX7 up to 240 MHz |
| **Memory** | 16 MB QSPI flash, 16 MB Octal PSRAM |
| **Wireless** | 2.4 GHz Wi-Fi 802.11 b/g/n, Bluetooth LE |
| **USB** | Native USB-C serial/JTAG/programming |
| **Audio hardware** | ES8311 speaker codec and ES7210 microphone ADC present, not enabled by EspControl |
| **Home screen** | 4 card slots |

## Card Layout

<!--@include: ../generated/screens/esp32-s3-box-3-grid.md-->

## Install

Connect the ESP32-S3-BOX-3 to your computer with a USB-C data cable, then click the button below.

<!--@include: ../generated/screens/esp32-s3-box-3-install.md-->

## Manual ESPHome Package

```yaml
substitutions:
  name: "esp32-s3-box-3"
  friendly_name: "ESP32-S3-BOX-3"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

packages:
  espcontrol:
    url: https://github.com/ryxios/espcontrol/
    file: devices/esp32-s3-box-3/packages.yaml
    refresh: 1s
```

## Hardware Integration Notes

- LCD SPI, touch I²C, backlight, and button pins are copied from the Espressif BSP, not from generic ESP32-S3 examples.
- The GT911 red circular home touch button is exposed as a binary sensor.
- The physical Config and Mute buttons are exposed as binary sensors and wake the screen.
- TT21100 touch variants are not enabled because the BSP detects GT911/TT21100 dynamically in C, while this ESPHome YAML profile must choose one static touch platform.
- Audio, SD card, IMU, and PMOD expansion remain TODO until EspControl has explicit product behavior for them.
