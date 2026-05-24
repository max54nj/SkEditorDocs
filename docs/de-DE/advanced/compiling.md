---
prev:
   text: 'Erweiterungen - Eine Erweiterung erstellen'
   link: '/de-DE/addons/creating-an-addon'
next: 
   text: 'Fortgeschritten - Mitwirken'
   link: '/de-DE/advanced/contributing'

---

# Kompilieren

Möglicherweise möchtest du SkEditor selbst kompilieren, um beispielsweise neue Funktionen aus einem `dev`-Branch zu testen.
Das ist in .NET ganz einfach und kann in wenigen Schritten erledigt werden.

## Voraussetzungen

- [.NET 8.0 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
- [Git](https://git-scm.com/downloads)

::: warning
Stelle sicher, dass du die neuste Version des SDK installiert hast. Der apt-Paketmanager auf Linux installiert oft eine ältere Version, die während der Kompilierung zu Problemen führen könnte. Verwende das Installationsskript, um die neueste Version zu installieren.
:::

## Repository klonen

Du kannst das Repository mit dem folgenden Befehl klonen:

```bash
git clone -b dev/dev https://github.com/SkEditorTeam/SkEditor.git
```

Dies klont den `dev/dev`-Branch des Repositorys. Wenn du einen anderen Branch klonen möchtest, kannst du `dev/dev` durch den gewünschten Branch-Namen ersetzen oder die `-b`-Option ganz weglassen, um den `main`-Branch zu klonen.

## Navigieren zum Projektverzeichnis

Das Repository enthält zwei Projekte: `SkEditor` und `Installer`, daher musst du zum `SkEditor`-Projektverzeichnis navigieren, um es zu kompilieren. Du kannst dies mit dem folgenden Befehl tun (vorausgesetzt, du befindest dich im Stammverzeichnis des geklonten Repositorys):

```bash
cd SkEditor
```

## Projekt kompilieren

Jetzt kannst du die App mit einem einzigen Befehl ausführen:

```bash
dotnet run
```

Und veröffentliche es mit:

```bash
dotnet publish
```

Dies wird das Projekt erstellen und veröffentlichen, wobei die Ausgabe irgendwo im `bin/Release/net8.0`-Ordner platziert wird (die Befehlsausgabe zeigt dir den genauen Pfad an).

Aber das ist nur die einfachste Möglichkeit, das Projekt zu veröffentlichen. Es gibt viele Optionen, die du verwenden kannst, um den Build-Prozess anzupassen, die du in der [offiziellen Dokumentation](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-publish) finden kannst.

Wenn du einen sauberen und effizienten Build möchtest, kannst du den folgenden Befehl verwenden:

```bash
dotnet publish -c Release -r win-x64 --no-self-contained -p:PublishSingleFile=true -p:PublishReadyToRun=true
```

Dieser Befehl wird die folgenden Dinge tun:

- Sicherstellen, dass der Build in der `Release`-Konfiguration erfolgt
- Den `win-x64`-Runtime anvisieren (du kannst dies bei Bedarf zu `linux-x64`, `osx-x64` usw. ändern)
- Die .NET-Laufzeit NICHT in die Ausgabe einbeziehen (der Benutzer muss also .NET 8.0 installiert haben)
- Das Projekt als eine einzelne Datei veröffentlichen (nun ja, eine einzelne ausführbare Datei - es wird immer noch einige DLL-Dateien im Ausgabeverzeichnis geben, die für die Ausführung der App erforderlich sind)
- R2R-Kompilierung aktivieren, die die Startzeit der Anwendung verbessert

Du kannst diese Optionen an deine Bedürfnisse anpassen, aber das ist ein guter Ausgangspunkt für die meisten Anwendungsfälle.
