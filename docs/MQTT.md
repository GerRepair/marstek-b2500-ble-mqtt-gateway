# MQTT-Schnittstelle

Das Gateway veröffentlicht pro hinzugefügtem Speicher einen retained Akkustand.

## Akkustand

```text
marstek/<mac-ohne-doppelpunkte>/soc
```

Beispiel:

```text
marstek/aabbcc112233/soc
```

Payload:

```text
73
```

Der Wert ist eine ganze Zahl von `0` bis `100`.

## Verfügbarkeit

```text
marstek/<mac-ohne-doppelpunkte>/availability
```

Typische Payloads:

```text
online
offline
```

## Home Assistant Discovery

Bei aktivierter Discovery veröffentlicht das Gateway eine Sensorkonfiguration unter dem Home-Assistant-Discovery-Präfix. Dadurch erscheint jeder Speicher als eigenes Gerät mit einem Batteriesensor.

## Test mit Mosquitto

```bash
mosquitto_sub -h 192.168.1.10 -u mqtt-user -P 'PASSWORT' -v -t 'marstek/#'
```

Nutze für das Gateway nach Möglichkeit einen eigenen MQTT-Benutzer mit Lese-/Schreibrechten nur auf den benötigten `marstek/#`- und Discovery-Topics.
