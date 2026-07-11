# Sicherheit

## Unterstützte Version

Sicherheitskorrekturen werden zunächst für den aktuellen Stand des `main`-Branches vorgesehen.

## Sicherheitsrelevante Hinweise

- Das Webinterface besitzt derzeit keine Benutzeranmeldung. Es darf nur in einem vertrauenswürdigen lokalen Netzwerk betrieben und nicht aus dem Internet freigegeben werden.
- Der Einrichtungs-Access-Point nutzt im Auslieferungszustand das dokumentierte Passwort `marstek123`. Für eine öffentliche oder dauerhaft zugängliche Installation sollte es vor dem Flashen in `src/main.cpp` geändert werden.
- WLAN- und MQTT-Zugangsdaten werden im nichtflüchtigen Speicher des ESP32 abgelegt. Sie sind nicht als Schutz gegen physischen Zugriff auf das Gerät gedacht.
- MQTT sollte nach Möglichkeit mit einem eigenen Benutzer und nur den benötigten Topic-Rechten betrieben werden.
- Logs und Screenshots können MAC-Adressen, SSIDs und IP-Adressen enthalten. Vor Veröffentlichung anonymisieren.

## Schwachstellen melden

Bitte sicherheitsrelevante Details nicht sofort in einem öffentlichen Issue veröffentlichen. Nutze nach dem Hochladen des Projekts die Funktion **Security → Advisories → New draft security advisory** im GitHub-Repository.
