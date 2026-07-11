# Mitwirken

Beiträge sind willkommen. Das Projekt ist experimentell und kommuniziert mit einem nicht offiziell dokumentierten BLE-Protokoll. Änderungen am Protokoll sollten deshalb besonders nachvollziehbar und möglichst mit anonymisierten Logs belegt sein.

## Lokale Einrichtung

```bash
python -m pip install platformio
pio run -e esp32dev
```

Für einen ESP32-S3:

```bash
pio run -e esp32-s3-devkitc-1
```

## Pull Requests

1. Einen eigenen Branch erstellen.
2. Kleine, klar abgegrenzte Änderungen vornehmen.
3. Beide PlatformIO-Umgebungen bauen, sofern die Änderung nicht ausdrücklich boardspezifisch ist.
4. Keine Zugangsdaten, vollständigen MAC-Adressen aus fremden Installationen oder private Netzwerkdaten einchecken.
5. Sichtbare Änderungen in `CHANGELOG.md` ergänzen.

## Stil

- C++: zwei Leerzeichen Einrückung.
- Keine dynamisch unnötig großen JSON-Dokumente oder lange blockierende Wartezeiten ergänzen.
- BLE-Abfragen bleiben sequenziell, solange die Speicher- und Stabilitätsauswirkungen paralleler Verbindungen nicht getestet sind.
- Fehler im Webinterface sollen als verständliche Meldung erscheinen und zusätzlich seriell protokolliert werden.
