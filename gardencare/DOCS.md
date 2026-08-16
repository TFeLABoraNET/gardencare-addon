# GardenCare

Gartenpflege-Assistent für den eigenen Garten: Pflanzen erfassen, einen Pflegeplan festlegen,
Aufgaben abarbeiten, Fotos und Verlauf führen — alles lokal auf deinem Gerät.

> **Experimentelle Beta.** Zum Ausprobieren gedacht, nicht für den Dauerbetrieb. Daten, Bedienung
> und Schnittstellen können sich noch ändern. Es gibt noch **kein Backup/Restore**, und die
> Sicherheits- und Performance-Prüfung ist nicht abgeschlossen.

## Installation

1. Add-on installieren und **starten**. Der erste Start dauert länger: das Image wird geladen und
   die Datenbank angelegt.
2. **In Seitenleiste anzeigen** einschalten.
3. GardenCare über die Seitenleiste öffnen.

Es gibt keine Konfigurationsoptionen — siehe unten.

## Zugriff

GardenCare läuft über **Ingress**: du erreichst es über die Home-Assistant-Oberfläche und bist
damit schon angemeldet. Es wird kein Port nach außen geöffnet, und du brauchst kein zweites
Passwort.

## Daten

Alles liegt unter `/data`: die SQLite-Datenbank und die Fotodateien. Der Supervisor sichert dieses
Verzeichnis über Neustarts und Updates hinweg.

Bei jedem Start werden ausstehende Datenbank-Migrationen angewendet. Schlägt das fehl, **startet
GardenCare absichtlich nicht** — ein Server, der auf einer halb migrierten Datenbank weiterschreibt,
richtet Schaden an, den man erst Wochen später bemerkt. Im Protokoll steht dann, woran es lag.

## Home Assistant

Das Add-on liest die Home-Assistant-Core-API über den Supervisor (`homeassistant_api: true`). Dafür
ist **nichts einzustellen**: den nötigen Zugriff bekommt GardenCare zur Laufzeit, und ein Token
taucht weder in der Konfiguration noch im Protokoll auf.

Darüber laufen, sobald du sie in GardenCares Einstellungen zuordnest:

- Sensoren (z. B. Bodenfeuchte) für Pflegeregeln
- die Wetter-Entität für wetterabhängige Empfehlungen
- Benachrichtigungen, auch Telegram, über einen Home-Assistant-Dienst

Fällt Home Assistant aus, arbeitet GardenCare weiter: der Garten, der Pflegeplan, die Aufgaben und
die Fotos sind lokal.

## Berechtigungen

Bewusst **nicht** angefordert: `host_network`, `privileged`, `full_access`, Gerätezugriff und
zusätzliche Verzeichnis-Mappings. Ein Gartenprogramm braucht keine Hardware, und hinter Ingress kein
Host-Netzwerk.

## Cloud-Dienste (optional)

Pl@ntNet (Bestimmung per Foto) und Mistral (KI-Wissensentwürfe) sind optional und brauchen jeweils
einen eigenen API-Schlüssel. Beide richtest du in GardenCares **Einstellungen** ein, nicht hier.

Das ist Absicht: die Schlüssel gehören in genau einen Speicher, und ein zweiter in den Add-on-Optionen
wäre ein zweiter Ort, aus dem sie entweichen können. GardenCare zeigt einen gespeicherten Schlüssel
nie wieder an — nur, ob einer hinterlegt ist.

Ohne diese Dienste funktioniert der gesamte lokale Kern unverändert; die Pflanzenbestimmung ist dann
manuell.

## Zeitplanung

GardenCare prüft **stündlich**, welche Pflegeaufgaben anstehen, und einmal direkt beim Start. Nichts,
was GardenCare plant, ist feiner als tagesgenau, deshalb wäre häufigeres Prüfen nur Rechenzeit auf
einem Raspberry Pi.

Unabhängig davon: Wenn du eine Pflegeregel speicherst, werden die daraus fälligen Aufgaben **sofort**
erzeugt. Du musst nie auf den nächsten Durchlauf warten.

## Rückmeldungen

Was schiefgeht, wo etwas unverständlich ist, was fehlt:
<https://github.com/TFeLABoraNET/plantcalendar/issues>

Bitte keine API-Schlüssel oder Tokens mitschicken. Der vollständige Testablauf steht in
`docs/BETA_TESTING.md`.
