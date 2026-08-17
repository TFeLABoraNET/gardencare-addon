# GardenCare — Home Assistant Add-on (Beta)

Gartenpflege-Assistent: Pflanzen, Pflegeplan, Aufgaben, Fotos und Kalender — lokal auf dem eigenen
Gerät.

> **Experimentelle Beta.** Zum Ausprobieren gedacht, nicht für den Dauerbetrieb. Daten, Bedienung
> und Schnittstellen können sich noch ändern. Es gibt noch **kein Backup/Restore**, und die
> Sicherheits- und Performance-Prüfung ist nicht abgeschlossen. Lege hier nichts ab, was du nicht
> verlieren möchtest.

## Installation

1. In Home Assistant: **Einstellungen → Add-ons → Add-on Store → ⋮ → Repositories**
2. Diese URL hinzufügen:

   ```text
   https://github.com/TFeLABoraNET/gardencare-addon
   ```

3. **GardenCare** erscheint im Store. Installieren und **starten**. Der erste Start dauert länger:
   das Image wird geladen und die Datenbank angelegt.
4. **In Seitenleiste anzeigen** einschalten.

## Was hier drin ist

Nur die Add-on-Beschreibung. Das Image kommt aus der GitHub Container Registry:

```text
ghcr.io/tfelaboranet/gardencare:0.1.0-beta.15
```

Unterstützt werden `aarch64` (Raspberry Pi 4) und `amd64`.

## Konfiguration

Es gibt **keine Optionen**, und das ist Absicht. Den Zugriff auf die Home-Assistant-API bekommt
GardenCare zur Laufzeit vom Supervisor; Pl@ntNet, Mistral und Telegram richtest du in GardenCares
eigenen **Einstellungen** ein. Ein zweiter Ort für Geheimnisse wäre ein zweiter Ort, aus dem sie
entweichen können.

## Daten

Alles liegt unter `/data` — die Datenbank und die Fotos. Der Supervisor sichert das über Neustarts
und Updates hinweg.

## Rückmeldungen

<https://github.com/TFeLABoraNET/plantcalendar/issues>

Bitte keine API-Schlüssel oder Tokens mitschicken.

---

*Dieses Repository wird aus `deploy/home-assistant/` im GardenCare-Quellrepository erzeugt
(`scripts/build-addon-repo.sh`). Bitte hier nichts von Hand ändern — die Änderung wäre beim
nächsten Release wieder weg.*
