# Third-party notices

Dieses Projekt verwendet zur Build-Zeit:

- NimBLE-Arduino – BLE-Client und Scanner
- PubSubClient – MQTT-Client
- ArduinoJson – JSON-Verarbeitung
- Arduino-ESP32 – WLAN, WebServer, Preferences und Laufzeit

Die minimal implementierte Marstek-B2500-Kommunikation orientiert sich an öffentlich dokumentierten Protokollmerkmalen des Projekts `tomquist/esphome-b2500`: BLE-Dienst FF00, Command-Charakteristik FF01, Status-Charakteristik FF02 sowie die Runtime- und Cell-Info-Kommandos. Es wurde kein Quellcode dieses Projekts in dieses Gateway kopiert.
