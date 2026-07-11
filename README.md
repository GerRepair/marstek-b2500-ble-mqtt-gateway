# Marstek B2500 BLE–MQTT Gateway


<img width="1173" height="760" alt="tempsnip" src="https://github.com/user-attachments/assets/1da8f7e3-13dd-4e86-92d8-ae9f43b432f7" />



ESP32-Firmware mit Weboberfläche zum Suchen und Hinzufügen mehrerer Marstek-B2500-Speicher. Das Gateway liest per Bluetooth ausschließlich den Akkustand (SOC) aus und veröffentlicht ihn über MQTT. Optional werden die Sensoren automatisch über Home Assistant MQTT Discovery angelegt.

> **Hinweis:** Community-Projekt, nicht von Marstek entwickelt oder unterstützt. Das BLE-Protokoll ist nicht offiziell dokumentiert und kann sich zwischen Modellen oder Firmwareständen unterscheiden. Die ESP32-Firmware ist experimentell und sollte zunächst mit einem Speicher getestet werden.

![Weboberfläche](docs/images/webinterface-preview.png)

## Funktionen

- Responsive Weboberfläche direkt auf dem ESP32
- WLAN-Suche mit auswählbaren SSIDs
- DHCP oder manuelle IPv4-Konfiguration
- Notfall-Access-Point erst nach drei fehlgeschlagenen WLAN-Versuchen
- Automatisches Abschalten des Access Points nach erfolgreicher WLAN-Verbindung
- BLE-Suche nach Speichern in Reichweite
- Automatische Kennzeichnung und Übernahme möglicher B2500-Geräte
- Bis zu acht gespeicherte Geräte
- Sequenzielle BLE-Abfrage für bessere Stabilität
- Retained MQTT-Akkustand pro Speicher
- Optionale Home Assistant MQTT Discovery
- Anzeigename ändern, Gerät löschen und sofortige Abfrage


## Datenfluss

```text
Marstek B2500 ── BLE ──► ESP32 ── WLAN/MQTT ──► Home Assistant / MQTT-Client
```

## Unterstützte Boards

| Board | PlatformIO-Umgebung | Hinweis |
|---|---|---|
| ESP32-WROOM-32, ESP32 DevKit V1, ESP32 Dev Module | `esp32dev` | Standard und empfohlen für das vorhandene Board |
| ESP32-S3 DevKitC-1 | `esp32-s3-devkitc-1` | Alternative Umgebung enthalten |

## Schnellstart

### 1. Bauen und flashen

1. Visual Studio Code öffnen und "PlatformIO" auf der Linken Seite unter Erweiterung hinzufügen
<img width="1235" height="730" alt="image" src="https://github.com/user-attachments/assets/7b48b8fd-6bc8-4c86-a92f-e9bb6b3d1edd" />

2. Projekt-Ordner öffnen  File->Open Folder -> marstek-b2500-web-gateway öffnen

3 Build und Upload 

<img width="651" height="685" alt="image" src="https://github.com/user-attachments/assets/234a3461-11ac-4190-b791-1b13875b8fbc" />

Nach dem Upload startet der ESP32 den AP zum einrichten.



Terminal

```bash
pio run -e esp32dev -t upload
pio device monitor -b 115200
```

Bei einem echten ESP32-S3:

```bash
pio run -e esp32-s3-devkitc-1 -t upload
```

Ausführliche Hinweise: [Bauen und Flashen](docs/BUILD_AND_FLASH.md)

### 2. Ersteinrichtung

Ohne gültige WLAN-Konfiguration wird der Einrichtungs-AP gestartet:

```text
SSID:     Marstek-Gateway-XXXX
Passwort: marstek123
Adresse:  http://192.168.4.1
```

1. Mit dem Access Point verbinden.
2. `http://192.168.4.1` öffnen.
3. Unter **Einstellungen** auf **WLAN suchen** klicken.
4. SSID übernehmen, WLAN-Passwort und MQTT-Daten eintragen.
5. Speichern und den Neustart abwarten.
6. Im normalen WLAN die neue DHCP-IP oder `http://marstek-gateway.local` öffnen.
7. Unter **Speicher suchen** die gewünschten Geräte hinzufügen.

Sind WLAN-Daten gespeichert, versucht das Gateway die Verbindung dreimal. Erst danach wird der Notfall-AP aktiviert. Sobald die WLAN-Verbindung erfolgreich ist, wird der AP vollständig abgeschaltet.

## DHCP und feste IP-Adresse

Standardmäßig bezieht der ESP32 seine Adresse per DHCP. Für eine feste Adresse:

1. Zunächst erfolgreich per DHCP verbinden.
2. In den Einstellungen **Aktuelle Werte übernehmen** wählen.
3. DHCP deaktivieren.
4. Gewünschte IP, Gateway, Subnetzmaske und DNS prüfen.
5. Speichern.

Die Adresse muss im Router reserviert sein oder außerhalb dessen DHCP-Vergabebereichs liegen, damit kein IP-Konflikt entsteht.

## MQTT

Akkustand:

```text
marstek/<MAC-OHNE-DOPPELPUNKTE>/soc
```

Beispiel:

```text
Topic:   marstek/aabbcc112233/soc
Payload: 73
```

Verfügbarkeit:

```text
marstek/aabbcc112233/availability
```

Weitere Details: [MQTT-Schnittstelle](docs/MQTT.md)

## GitHub-Projekt verwenden

Das Repository enthält:

- Build-Workflow für jeden Push und Pull Request
- Release-Workflow für Tags wie `v0.1.2`
- Issue-Vorlagen
- Pull-Request-Vorlage
- Sicherheits- und Beitragsrichtlinien

Anleitung: [Zu GitHub hochladen](docs/GITHUB_UPLOAD.md)

## Projektstruktur

```text
.github/
  workflows/
  ISSUE_TEMPLATE/
docs/
  images/
src/
  main.cpp
  web_ui.h
platformio.ini
README.md
LICENSE
CHANGELOG.md
SECURITY.md
CONTRIBUTING.md
```

## Technische Eckdaten

- BLE-Service: `FF00`
- Command-Charakteristik: `FF01`
- Status-Charakteristik: `FF02`
- Maximal acht gespeicherte Geräte
- Eine BLE-Verbindung gleichzeitig
- Standard-Abfrageintervall: 60 Sekunden
- Firmware-Version: `0.1.2`

## Sicherheit

Das Webinterface besitzt derzeit keine Anmeldung. Das Gateway darf nicht direkt aus dem Internet erreichbar sein. Ändere außerdem vor einem dauerhaften Einsatz das Standardpasswort `marstek123` in `src/main.cpp`. Weitere Hinweise stehen in [SECURITY.md](SECURITY.md).

## Fehlerbehebung

Siehe [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md).

## Lizenz

MIT – siehe [LICENSE](LICENSE).
