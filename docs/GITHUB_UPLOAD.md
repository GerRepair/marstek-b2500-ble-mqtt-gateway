# Projekt zu GitHub hochladen

## 1. Leeres Repository erstellen

Auf GitHub ein neues Repository anlegen, beispielsweise:

```text
marstek-b2500-ble-mqtt-gateway
```

Beim Erstellen **keine** zusätzliche README, `.gitignore` oder Lizenz erzeugen, da diese Dateien bereits enthalten sind.

## 2. Projekt lokal initialisieren

Den Projektordner in PowerShell oder einem Terminal öffnen:

```bash
git init
git add .
git commit -m "Initial release"
git branch -M main
```

## 3. Repository verbinden

`DEIN-NAME` ersetzen:

```bash
git remote add origin https://github.com/DEIN-NAME/marstek-b2500-ble-mqtt-gateway.git
git push -u origin main
```

## 4. Automatischen Build prüfen

Nach dem Push den Reiter **Actions** öffnen. Der Workflow baut automatisch:

- `esp32dev`
- `esp32-s3-devkitc-1`

Die erzeugten Binärdateien stehen anschließend als Workflow-Artefakte bereit.

## 5. Erste Release-Version erstellen

```bash
git tag v0.1.2
git push origin v0.1.2
```

Der Release-Workflow baut beide Firmwarevarianten, erstellt Prüfsummen und legt automatisch ein GitHub Release an.
