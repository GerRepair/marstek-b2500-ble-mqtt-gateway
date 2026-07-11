# Bauen und Flashen

## Voraussetzungen

- Visual Studio Code mit PlatformIO-Erweiterung oder PlatformIO Core
- Datenfähiges USB-Kabel
- Klassischer ESP32 beziehungsweise ESP32-S3

## Klassischer ESP32

```bash
pio run -e esp32dev -t clean
pio run -e esp32dev
pio run -e esp32dev -t upload
pio device monitor -b 115200
```

## ESP32-S3

```bash
pio run -e esp32-s3-devkitc-1 -t clean
pio run -e esp32-s3-devkitc-1
pio run -e esp32-s3-devkitc-1 -t upload
pio device monitor -b 115200
```

## Falscher Chip ausgewählt

Bei dieser Meldung:

```text
This chip is ESP32, not ESP32-S3. Wrong --chip argument?
```

wurde ein klassischer ESP32 mit der S3-Umgebung angesprochen. Verwende:

```bash
pio run -e esp32dev -t upload
```

## Upload bleibt bei „Connecting“ stehen

1. Upload starten.
2. Die BOOT-Taste gedrückt halten.
3. Kurz RESET/EN drücken oder das Board neu verbinden.
4. BOOT loslassen, sobald der Schreibvorgang beginnt.

Je nach DevKit funktioniert der automatische Bootloader-Modus bereits ohne Tastendruck.
