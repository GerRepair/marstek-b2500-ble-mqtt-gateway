# Fehlerbehebung

## Notfall-AP erscheint nicht

Das Gateway startet den Access Point nur ohne gespeicherte WLAN-Daten oder nach drei erfolglosen Verbindungsversuchen. Ein vollständiger Versuch kann einige Sekunden dauern.

Standardwerte:

```text
SSID: Marstek-Gateway-XXXX
Passwort: marstek123
Adresse: http://192.168.4.1
```

## Weboberfläche ist nach Speicherung nicht erreichbar

- Im Router nach der neu vergebenen DHCP-Adresse suchen.
- `http://marstek-gateway.local` probieren.
- Bei statischer IP Gateway, Netzmaske und Adressbereich prüfen.
- Nach drei fehlgeschlagenen WLAN-Versuchen wieder mit dem Notfall-AP verbinden.

## B2500 wird gefunden, aber SOC bleibt unbekannt

- Marstek-App vollständig schließen; sie kann die BLE-Verbindung blockieren.
- ESP32 näher am Speicher platzieren.
- Nur einen Speicher hinzufügen und ein Abfrageintervall von mindestens 300 Sekunden verwenden.
- Seriellen Monitor mit 115200 Baud öffnen.
- Prüfen, ob das konkrete Modell beziehungsweise die Firmware das erwartete BLE-Protokoll verwendet.

## MQTT bleibt getrennt

- Broker-IP, Port, Benutzer und Passwort prüfen.
- Topic-Rechte des MQTT-Benutzers prüfen.
- Sicherstellen, dass ESP32 und Broker einander im Netzwerk erreichen können.
- Mit `mosquitto_sub` oder den MQTT-Entwicklerwerkzeugen von Home Assistant testen.

## WLAN-Suche zeigt keine Netzwerke

- Einige Sekunden warten und erneut suchen.
- Prüfen, ob das WLAN im 2,4-GHz-Band sendet; klassische ESP32 unterstützen kein 5-GHz-WLAN.
