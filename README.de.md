# Plugins

[English](README.md) | **Deutsch**

Ein Plugin-Manager (Dateisystem-Plugin) für den [Total Commander](https://www.ghisler.com), 32 und 64 Bit.
Er zeigt alle Plugins des Total Commanders als Dateien in einem Panel und lässt dich sie installieren, entfernen, aktivieren, deaktivieren und umsortieren, ohne die *Konfiguration* zu öffnen. Nativ, ohne Laufzeitumgebung, außer dem Plugin muss nichts installiert werden.

![Plugins zeigt die Eigenschaften eines Lister-Plugins: Datei, Version, Architektur, Position und die Endungen, für die es registriert ist](docs/screenshot.png)

## Aufbau

*Plugins* öffnest du über die Netzwerkumgebung bzw. die Liste der Dateisystem-Plugins.

- Zwei Ansichten (Einstellung *Ansicht*): **Gruppiert** (Standard) mit einem Ordner pro Plugin-Typ – Lister, Packer, Inhalt, Dateisystem – oder **Liste** mit allen Plugins in einer Liste. In der Liste beginnen die Namen mit dem Typ (`WLX 00 Synta`, `WCX 7-Zip`, `WDX …`, `WFX …`); sie lässt sich nach Name (nach Typ, dann nach Nummer) oder nach der Spalte *Typ* sortieren, und das Umsortieren funktioniert wie in den Ordnern.
- Jedes Plugin ist eine Datei. Lister-, Inhalts- und Dateisystem-Plugins tragen ihre Reihenfolge als Zahl (`00`, `01`, … wie in der `wincmd.ini`); deaktivierte Plugins sind mit „(aus)“ markiert und stehen am Ende.
- Das Panel öffnet sich in einer Spaltenansicht mit Name, Status, „Registriert für“ (Endungen eines Packers, Detect String der übrigen) und Version. Weitere Spalten für eigene Ansichten (*Benutzerdefinierte Spalten*, Plugin „Plugins“): Position, Typ, Architektur, Pfad, Beschreibung.

## Aktionen

- **Installieren:** eine Plugin-Datei (`.wlx`, `.wcx`, `.wdx`, `.wfx`, auch die 64-Bit-Varianten) oder ein ZIP/7z mit `pluginst.inf` ins Panel kopieren (F5/F6, Drag & Drop), in die Wurzel oder in einen der Ordner – der Typ wird aus der Datei gelesen. Plugins fragt vorher nach und lehnt Plugins ab, die nur in der anderen Bit-Breite als der Total Commander vorliegen. Die Dateien landen im Plugin-Ordner des Total Commanders und das Plugin wird registriert (Lister: der Detect String wird aus dem Plugin gelesen, Packer: Endungen aus `pluginst.inf` oder werden erfragt). Eine Plugin-Datei, die der Total Commander geladen hat, lässt sich nicht überschreiben; die alte Datei wird daher in *Name*`.old` umbenannt und die neue daneben geschrieben. Die `.old`-Datei wird beim nächsten Laden von Plugins gelöscht.
- **Deinstallieren:** Entf, oder die Schaltfläche *Deinstallieren* in den Eigenschaften (Enter). Das Plugin wird abgemeldet und sein Ordner in den Papierkorb verschoben.
- **Aktivieren / Deaktivieren:** Alt+Enter. Ein deaktiviertes Plugin bleibt in `[InactivePlugins]` und kehrt an seinen Platz zurück, wenn du es wieder aktivierst.
- **Reihenfolge ändern:** in den Eigenschaften (Enter) die Pfeil-Buttons neben der Position benutzen (oder die Tasten Hoch und Runter), die neue Position eintippen, oder den Eintrag umbenennen (Umschalt+F6) und die Zahl am Anfang ändern, zum Beispiel `05 Synta` in `01 Synta`. Lister-, Inhalts- und Dateisystem-Plugins haben eine Reihenfolge (bei Dateisystem-Plugins die der Einträge in der wincmd.ini; der Total Commander 11.5 zeigt sie in der Netzwerkumgebung trotzdem nach Namen sortiert); Packer nicht. Optional (Einstellung „Hoch / Runter mit Tastenkombination verschiebt Lister-, Inhalts- und Dateisystem-Plugins“, standardmäßig aus): Strg+Alt+Hoch / Strg+Alt+Runter verschiebt den Eintrag unter dem Cursor direkt im Panel um eine Stelle, der Cursor folgt; das gilt in den Ordnern Lister, Inhalt und Dateisystem und in der Listenansicht. Der Name unter dem Cursor wird aus der Dateiliste gelesen, die Zwischenablage und die Kommandozeile bleiben also unberührt und die Taste funktioniert auch bei ausgeblendeter Kommandozeile. Alt+Hoch / Alt+Runter ist im Total Commander die „Verzeichnishistorie“, die Tastenkombination kannst du deshalb selbst wählen: in den Einstellungen Strg, Alt und Umschalt beliebig ankreuzen (mindestens Strg oder Alt) oder `ReorderKeys` in der `fsplugin.ini` setzen, zum Beispiel `ReorderKeys=Ctrl+Shift+Alt`.
- **Eigenschaften** (Enter): bei Lister- und Inhalts-Plugins werden die Endungen des Detect Strings als Kontrollkästchen angezeigt, zusammen mit denen, die das Plugin selbst vorschlägt; an- oder abhaken, *Alle* / *Keine* benutzen. Andere Teile des Detect Strings (`FORCE`, `SIZE<…`, Gruppen) bleiben unverändert in einem Feld darunter. Bei Packern sind die Kontrollkästchen die Endungen, für die der Packer registriert ist; eine Endung, die ein anderer Packer benutzt, wechselt zu diesem.
- Derselbe Dialog hat einen Schalter *Pfad mit %COMMANDER_PATH% speichern*: der Plugin-Pfad wird als `%COMMANDER_PATH%\plugins\…` (portabel) oder als absoluter Pfad gespeichert.
- **Info** in der Wurzel zeigt den Über-Dialog, **Einstellungen** öffnet die Einstellungen: Darstellung (Auto / Hell / Dunkel), Sprache (Auto / Deutsch / English), Ansicht (Gruppiert / Liste), ob Info und Einstellungen mit Enter oder nur mit Alt+Enter öffnen, ob neue Plugins mit `%COMMANDER_PATH%` gespeichert werden, ob nur die zur Bitbreite des Total Commanders passenden Dateien kopiert werden (32 oder 64 Bit), eine Schaltfläche *Aufräumen*, die ungenutzte 32-/64-Bit-Dateien registrierter Plugins in den Papierkorb verschiebt, und die Benachrichtigungen – vor dem Installieren fragen, Bestätigung nach erfolgreicher Installation, vor dem Löschen fragen, Bestätigung nach dem Löschen – und das Umsortieren per Tastatur (Schalter plus die Tasten Strg, Alt und Umschalt, mindestens Strg oder Alt).

Änderungen werden in `wincmd.ini` geschrieben (und in die Datei, auf die sie die Plugin-Abschnitte umleitet); eine Kopie der vorherigen Datei bleibt als `*.plugins-bak` erhalten. Der Total Commander übernimmt sie nach einem Neustart.

Helles und dunkles Design im Windows-11-Stil, Oberfläche auf Deutsch und Englisch (folgt der Windows-Sprache).

## Download und Installation

1. **`Plugins.zip`** vom [neuesten Release](https://github.com/naderi/tc-plugins/releases/latest) herunterladen.
2. Das ZIP im Total Commander öffnen (Enter auf der Datei) und die Frage nach der Installation des Plugins bestätigen.

Voraussetzung: Total Commander 32 oder 64 Bit unter Windows 10 oder 11. Die Einstellungen stehen in `fsplugin.ini` neben `wincmd.ini`, Abschnitt `[Plugins]` (`Theme`, `Language`, `View`, `OpenInfoKey`, `StorePathWithVariable`, `OnlyOwnBitness`, `AskBeforeInstall`, `MessageAfterInstall`, `AskBeforeUninstall`, `MessageAfterUninstall`, `ReorderHotkey`, `ReorderKeys`).

## Lizenz

Freeware – frei nutzbar, aber **nicht zum Verkauf**. Siehe [LICENSE](LICENSE).

## Unterstützung

Wenn Plugins dir Zeit spart, kannst du die Entwicklung auf Ko‑fi unterstützen. ☕

<a href='https://ko-fi.com/N7N123QIX0' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi2.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

---

© 2026 [Ali Naderi](https://github.com/naderi) · [digitalent.dev](https://digitalent.dev/de/)
