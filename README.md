# hekate - Nyx

![Bild von Hekate](https://user-images.githubusercontent.com/3665130/60391760-bc1e8c00-9afe-11e9-8b7a-b065873081b2.png)

Benutzerdefinierter grafischer Nintendo Switch-Bootloader, Firmware-Patcher, Werkzeuge und vieles mehr.

- [Funktionen](#features)
- [Bootloader-Ordner und -Dateien](#bootloader-folders-and-files)
- [Bootloader-Konfiguration](#bootloader-configuration)
  * [Globale hekate-Konfigurationsschlüssel/Werte](#hekate-global-configuration-keysvalues-when-entry-is-config)
  * [Schlüssel/Werte-Kombinationen für Boot-Einträge](#boot-entry-keyvalue-combinations)
  * [Schlüssel/Werte-Kombinationen für Boot-Einträge für Exosphère](#boot-entry-keyvalue-combinations-for-exosphère)
  * [Payload-Speicher](#payload-storage)
  * [Nyx Konfigurationsschlüssel/Werte](#nyx-configuration-keysvalues-nyxini)

## Funktionen

- **Vollständig konfigurierbar und grafisch** mit Touchscreen- und Joycon-Eingabeunterstützung
- **Launcher-Stil, Hintergrund- und Farbthemen**
- **HOS (Switch OS) Bootloader** -- Für CFW Sys/Emu, OFW Sys und Stock Sys
- **Android & Linux Bootloader**
- **Payload-Launcher**
- **eMMC/emuMMC Backup/Wiederherstellungswerkzeuge**
- **SD-Karten-Partition-Manager** -- Bereitet SD-Karte für beliebige Kombination von HOS (Sys/emuMMC), Android und Linux vor und formatiert sie
- **emuMMC-Erstellung & -Manager** -- Kann auch vorhandene emuMMC migrieren und reparieren
- **Switch Android & Linux-Flasher**
- **USB-Massenspeicher (UMS) für SD/eMMC/emuMMC** -- Wandelt Switch in einen SD-Kartenleser um
- **USB-Gamepad** -- Wandelt Switch mit Joycon in ein USB-HID-Gamepad um
- **Hardware- und Peripheriegeräteinformationen** (SoC, Sicherungen, RAM, Display, Touch, eMMC, SD, Batterie, Netzteil, Ladegerät)
- **Viele weitere Werkzeuge** wie Archive Bit Fixer, Touch-Kalibrierung, SD/eMMC-Benchmark, AutoRCM-Aktivierung und mehr


## Bootloader-Ordner und -Dateien

| Ordner/Datei           | Beschreibung                                                             |
| ---------------------- | ------------------------------------------------------------------------ |
| bootloader             | Hauptordner.                                                             |
|  \|__ bootlogo.bmp     | Wird verwendet, wenn kein `logopath`-Schlüssel gefunden wird. Vom Benutzer bereitgestellt. Kann übersprungen werden. |
|  \|__ hekate_ipl.ini   | Haupt-Bootloader-Konfiguration und Boot-Einträge im `Launch`-Menü.       |
|  \|__ nyx.ini          | Nyx GUI-Konfiguration                                                    |
|  \|__ patches.ini      | Externe Patches hinzufügen. Kann übersprungen werden. Eine Vorlage findet sich [hier](./res/patches_template.ini) |
|  \|__ update.bin       | Wird bei Boot geladen, wenn neuer. Normalerweise für Modchips. Automatisch aktualisiert und beim ersten Boot erstellt. |
| bootloader/ini/        | Für individuelle INIs. `Weitere Konfigurationen`-Menü. Autoboot wird unterstützt. |
| bootloader/res/        | Nyx-Benutzerressourcen. Symbole und mehr.                                |
|  \|__ background.bmp   | Nyx - Benutzerdefiniertes Hintergrundbild. Vom Benutzer bereitgestellt. |
|  \|__ icon_switch.bmp  | Nyx - Standard-Symbol für CFWs.                                         |
|  \|__ icon_payload.bmp | Nyx - Standard-Symbol für Payloads.                                      |
| bootloader/sys/        | hekate- und Nyx-Systemmodulordner.                                       |
|  \|__ emummc.kipm      | emuMMC KIP1-Modul. !Wichtig!                                             |
|  \|__ libsys_lp0.bso   | LP0 (Schlafmodus) Modul. Wichtig!                                       |
|  \|__ libsys_minerva.bso | Minerva Training Cell. Wird für DRAM-Frequenztraining verwendet. !Wichtig! |
|  \|__ nyx.bin          | Nyx - hekates GUI. !Wichtig!                                             |
|  \|__ res.pak          | Nyx-Ressourcenpaket. !Wichtig!                                           |
|  \|__ thk.bin          | Atmosphäre Tsec Hovi Keygen. !Wichtig!                                   |
| bootloader/screenshots/ | Ordner, in dem Nyx-Screenshots gespeichert werden.                       |
| bootloader/payloads/   | Für das `Payloads`-Menü. Alle CFW-Bootloader, Tools, Linux-Payloads werden unterstützt. Autoboot nur durch Einbindung in eine INI unterstützt. |
| bootloader/libtools/   | Reserviert                                                               |



## Bootloader-Konfiguration

Der Bootloader kann über 'bootloader/hekate_ipl.ini' konfiguriert werden (sofern er auf der SD-Karte vorhanden ist). Jeder INI-Abschnitt repräsentiert einen Boot-Eintrag, außer dem speziellen Abschnitt 'config', der die globale Konfiguration steuert.


Es gibt vier mögliche Arten von Einträgen. "**[ ]**": Boot-Eintrag, "**{ }**": Beschriftung, "**#**": Kommentar, "*neue Zeile*": .ini kosmetische Neue Zeile.


**Eine Vorlage findest du [Hier](./res/hekate_ipl_template.ini)**

### Globale Konfigurationsschlüssel/Werte von hekate (wenn Eintrag *[config]*):

| Konfigurationsoption | Beschreibung                                                 |
| --------------------- | ------------------------------------------------------------ |
| autoboot=0            | 0: Deaktivieren, #: Nummer des Boot-Eintrags zum automatischen Booten. |
| autoboot_list=0       | 0: Lesen des `autoboot`-Boot-Eintrags aus hekate_ipl.ini, 1: Lesen aus dem INI-Ordner (INI-Dateien sind ASCII-geordnet). |
| bootwait=3            | 0: Deaktivieren (Deaktiviert auch das Bootlogo. Wenn **VOL-** seit dem Einspritzen gedrückt wird, gelangt man zum Menü.), #: Wartezeit für **VOL-**, um ins Menü zu gelangen. Max: 20s. |
| noticker=0            | 0: Animierter Strich wird während des benutzerdefinierten Bootlogos gezeichnet und zeigt die verbleibende Zeit bis zum Überspringen des Menüs an. 1: Deaktivieren. |
| autohosoff=1          | 0: Deaktivieren, 1: Wenn aus dem HOS über einen RTC-Alarm aufgewacht wird, wird das Logo angezeigt und dann vollständig ausgeschaltet, 2: Kein Logo, sofortiges Ausschalten. |
| autonogc=1            | 0: Deaktivieren, 1: Wendet automatisch den nogc-Patch an, wenn unverbrannte Sicherungen gefunden werden und ein >= 4.0.0 HOS gebootet wird. |
| bootprotect=0         | 0: Deaktivieren, 1: Schützt den Bootloader-Ordner vor Beschädigungen, indem das Lesen oder Bearbeiten im HOS verhindert wird. |
| updater2p=0           | 0: Deaktivieren, 1: Erzwingt Updates (falls erforderlich), um die reboot2payload-Binärdatei auf hekate zu setzen. |
| backlight=100         | Bildschirm-Hintergrundbeleuchtungsstufe. 0-255.              |

### Kombinationen von Schlüssel/Werten für Boot-Einträge:

| Konfigurationsoption      | Beschreibung                                                |
| -------------------------- | ---------------------------------------------------------- |
| warmboot={DATEI-Pfad}     | Ersetzt die Warmboot-Binärdatei                            |
| secmon={DATEI-Pfad}       | Ersetzt die Sicherheitsüberwachungs-Binärdatei             |
| kernel={DATEI-Pfad}       | Ersetzt die Kernel-Binärdatei                              |
| kip1={DATEI-Pfad}         | Ersetzt/Fügt den Initialisierungsprozess des Kernels hinzu. Es können mehrere festgelegt werden. |
| kip1={ORDNER-Pfad}/*      | Lädt jede .kip/.kip1 innerhalb eines Ordners. Kompatibel mit einzelnen kip1-Schlüsseln. |
| fss0={DATEI-Pfad}         | Nimmt eine Atmosphäre `package3`-Binärdatei (ehemals fusee-secondary.bin) und `extrahiert` alle benötigten Teile daraus. Kips, Exosphere, Warmboot und Mesophere, wenn aktiviert. |
| fss0experimental=1        | Aktiviert das Laden von experimentellem Inhalt aus einem FSS0-Speicher |
| exofatal={DATEI-Pfad}     | Ersetzt die Exosphere-Fatal-Binärdatei für Mariko          |
| -------------------------- | ---------------------------------------------------------- |
| kip1patch=Patchname        | Aktiviert einen kip1-Patch. Mehrere Zeilen und/oder in einer Zeile mit `,` als Trennzeichen angeben. Wenn der tatsächliche Patch nicht gefunden wird, wird eine Warnung angezeigt |
| emupath={ORDNER-Pfad}     | Zwingt emuMMC, den ausgewählten zu verwenden. (=emuMMC/RAW1, =emuMMC/SD00, etc). emuMMC muss von hekate erstellt werden, da es die raw_based/file_based-Dateien verwendet. |
| emummcforce=1              | Erzwingt die Verwendung von emuMMC. Wenn emummc.ini deaktiviert oder nicht gefunden ist, tritt ein Fehler auf. |
| emummc_force_disable=1     | Deaktiviert emuMMC, wenn es aktiviert ist.                 |
| stock=1                    | Deaktiviert nicht benötigte Kernel-Patching und CFW-Kips beim Ausführen von Stock oder Semi-Stock. `Wenn emuMMC aktiviert ist, ist emummc_force_disable=1` erforderlich. emuMMC wird auf Stock nicht unterstützt. Wenn zusätzliche KIPs benötigt werden, die nicht von OFW stammen, können Sie sie mit dem `kip1`-Schlüssel definieren. Es sollte kein Kip verwendet werden, der auf Atmosphäre-Patching beruht, da es hängen bleiben wird. Wenn `NOGC` benötigt wird, verwenden Sie `kip1patch=nogc`. |
| fullsvcperm=1              | Deaktiviert SVC-Überprüfung (volle Dienstberechtigung). Funktioniert nicht mit Mesosphäre als Kernel. |
| debugmode=1                | Aktiviert den Debug-Modus. Veraltet bei Verwendung von Exosphere als Secmon. |
| atmosphere=1               | Aktiviert das Atmosphère-Patching. Nicht erforderlich, wenn `fss0` verwendet wird. |
| -------------------------- | ---------------------------------------------------------- |
| payload={DATEI-Pfad}       | Payload-Start. Tools, Android/Linux, CFW-Bootloader usw. Jeder obige Schlüssel wird bei Verwendung damit nicht berücksichtigt. |
| -------------------------- | ---------------------------------------------------------- |
| l4t=1                      | Start von L4T Linux/Android nativ.                        |
| boot_prefixes={ORDNER-Pfad} | L4T-Bootstack-Verzeichnis.                             |
| ram_oc=0                   | L4T-RAM-Übertaktung. Siehe README_CONFIG.txt für weitere Informationen. |
| ram_oc_vdd2=1100           | L4T-RAM-VDD2-Spannung. Setzen Sie die VDD2 (T210B01) oder VDD2/VDDQ (T210) Spannung. 1050-1175. |
| ram_oc_vddq=600            | L4T-RAM-VDDQ-Spannung. Setzen Sie die VDDQ (T210B01). 550-650.         |
| uart_port=0                | Aktiviert das Protokollieren auf dem seriellen Port für L4T uboot/kernel. |
| Zusätzliche Schlüssel      | Jedes Distro unterstützt weitere Schlüssel. Lesen Sie README_CONFIG.txt für weitere Informationen.  |
| -------------------------- | ---------------------------------------------------------- |
| bootwait=3                 | Überschreibt das globale Boot-Warten aus `[config]`.     |
| id=IDNAME                  | Identifiziert den Boot-Eintrag für das erzwungene Booten über ID. Max. 7 Zeichen. |
| logopath={DATEI-Pfad}      | Wenn vorhanden, wird das angegebene Bitmap geladen. Andernfalls wird `bootloader/bootlogo.bmp` verwendet, wenn vorhanden. |
| icon={DATEI-Pfad}          | Erzwingt Nyx, das hier definierte Symbol zu verwenden. Wenn dies nicht gefunden wird, wird nach einer BMP mit dem Namen des Boot-Eintrags gesucht ([Test 2] -> `bootloader/res/Test 2.bmp`). Andernfalls werden Standardwerte verwendet. |

**Hinweis1**: Wenn du das Platzhalterzeichen (`/*`) mit `kip1` verwendest, kannst du trotzdem das normale `kip1` danach verwenden, um zusätzliche einzelne Kips zu laden.

**Hinweis2**: Bei Verwendung von FSS0 analysiert es Exosphere, Warmboot und alle Kern-Kips. Du kannst die ersten beiden durch die Verwendung von `secmon`/`warmboot` nach der Definition von `fss0` überschreiben. Du kannst `kip1` definieren, um einen zusätzlichen Kip oder mehrere über die Verwendung des Platzhalters (`/*`) zu laden.

**Warnung**: Sei vorsichtig, wenn du *fss0-Kernkips* definierst, wenn du `fss0` verwendest oder der Ordner (bei Verwendung von `/*`) sie enthält. Dies ist der Fall, wenn die Kips nicht miteinander kompatibel sind. Wenn sie kompatibel sind, kannst du `fss0`-Kips ohne Probleme überschreiben (nützlich zum Testen mit Zwischen-Kip-Änderungen). In solchen Fällen muss die `kip1`-Zeile unter der `fss0`-Zeile stehen.

### Boot-Eintrags-Schlüssel/Wert-Kombinationen für Exosphère:

| Konfigurationsoption  | Beschreibung                                                |
| ---------------------- | ---------------------------------------------------------- |
| nouserexceptions=1     | Deaktiviert Ausnahmehandler im Benutzermodus, wenn sie mit Exosphère gekoppelt sind. |
| userpmu=1              | Aktiviert den Benutzerzugriff auf PMU, wenn sie mit Exosphère gekoppelt sind.     |
| cal0blank=1            | Überschreibt die Exosphère-Konfiguration `blank_prodinfo_{sys/emu}mmc`. Wenn dieser Schlüssel nicht vorhanden ist, wird `exosphere.ini` verwendet. |
| cal0writesys=1         | Überschreibt die Exosphère-Konfiguration `allow_writing_to_cal_sysmmc`. Wenn dieser Schlüssel nicht vorhanden ist, wird `exosphere.ini` verwendet. |
| usb3force=1            | Überschreibt die Systemeinstellungen mit `mitm`-Konfiguration `usb30_force_enabled`. Wenn dieser Schlüssel nicht vorhanden ist, wird `system_settings.ini` verwendet. |

**Hinweis**: `cal0blank`, `cal0writesys` und `usb3force` überschreiben wie angegeben die `exosphere.ini` oder `system_settings.ini`. 0: Deaktivieren, 1: Aktivieren, Schlüssel fehlt: Originalwert verwenden.

**Hinweis2**: `blank_prodinfo_{sys/emu}mmc`, `allow_writing_to_cal_sysmmc` und `usb30_force_enabled` in `exosphere.ini` bzw. `system_settings.ini` sind die einzigen Atmosphäre-Konfigurationsschlüssel, die die hekate-Bootkonfiguration extern beeinflussen können, **wenn** die entsprechenden Schlüssel in der hekate-Konfiguration fehlen.

### Payload-Speicherung:

hekate verfügt über einen Startspeicher im Binärformat, der ihm hilft, die Konfiguration außerhalb der BPMP-Umgebung zu konfigurieren:

| Offset / Name           | Beschreibung                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| '0x94' boot_cfg         | Bit0: `Force AutoBoot`, Bit1: `Launch-Protokoll anzeigen`, Bit2: `Von ID booten`, Bit3: `Zu emuMMC booten`. |
| '0x95' autoboot         | Wenn `Force AutoBoot`: 0: Erzwingt das Öffnen des Menüs, sonst startet es diesen Eintrag.   |
| '0x96' autoboot_list    | Wenn `Force AutoBoot` und `autoboot`, dann wird aus dem Ini-Ordner gestartet. |
| '0x97' extra_cfg        | Wenn das Menü erzwungen wird: Bit5: `UMS ausführen`.                             |
| '0x98' xt_str[128]      | Abhängig von den gesetzten Konfigurationsbits.                                      |
| '0x98' ums[1]           | Wenn `UMS ausführen` gesetzt ist, wird das ausgewählte UMS gestartet. 0: SD, 1: eMMC BOOT0, 2: eMMC BOOT1, 3: eMMC GPP, 4: emuMMC BOOT0, 5: emuMMC BOOT1, 6: emuMMC GPP,  |
| '0x98' id[8]            | Wenn `Von ID booten` gesetzt ist, werden automatisch alle Ini-Dateien durchsucht und der Starteintrag mit dieser ID gefunden und gestartet. Muss mit NULL beendet sein. |
| '0xA0' emummc_path[120] | Wenn `Zu emuMMC booten` gesetzt ist, wird der aktuelle emuMMC überschrieben (Starteintrag oder emummc.ini). Muss mit NULL beendet sein. |

### Nyx Konfigurationsschlüssel/Werte (nyx.ini):

| Konfigurationsoption | Beschreibung                                                |
| --------------------- | ---------------------------------------------------------- |
| themebg=2d2d2d        | Setzt die Hintergrundfarbe von Nyx in HEX. EXPERIMENTELL.  |
| themecolor=167        | Setzt die Farbe der Text-Hervorhebungen in Nyx.            |
| entries5col=0         | 1: Setzt die Anzahl der Starteinträge von 4 auf 5 pro Zeile. Für insgesamt 10 Einträge. |
| timeoff=100           | Setzt den Zeitoffset in HEX. Muss im HOS-Epoche-Format sein. |
| homescreen=0          | Setzt den Startbildschirm. 0: Startmenü, 1: Alle Konfigurationen (verbindet Start und Weitere Konfigurationen), 2: Start, 3: Weitere Konfigurationen. |
| verification=1        | 0: Deaktiviert die Überprüfung der Sicherung/Wiederherstellung, 1: Sparse (blockbasiert, schnell und größtenteils zuverlässig), 2: Full (sha256-basiert, langsam und zu 100% zuverlässig). |
| --------------------- | ------- Die folgenden Optionen können nur in nyx.ini bearbeitet werden ------- |
| umsemmcrw=0           | 1: eMMC/emuMMC UMS wird standardmäßig als beschreibbar eingebunden. |
| jcdisable=0           | 1: Deaktiviert den Joycon-Treiber vollständig.               |
| jcforceright=0        | 1: Erzwingt, dass der rechte Joycon als Hauptmaussteuerung verwendet wird. |
| bpmpclock=1           | 0: Auto, 1: Schnellster, 2: Schneller, 3: Schnell. Verwenden Sie 2 oder 3, wenn Nyx hängt oder einige Funktionen wie UMS/Backup-Überprüfung fehlschlagen. |

```
hekate  (c) 2018,      naehrwert, st4rk.
        (c) 2018-2023, CTCaer.

Nyx GUI (c) 2019-2023, CTCaer.

Dank an: derrek, nedwill, plutoo, shuffle2, smea, thexyz, yellows8.
Grüße an: fincs, hexkyz, SciresM, Shiny Quagsire, WinterMute.

Verwendete Open-Source- und kostenlose Pakete:
 - FatFs R0.13a, Urheberrechte (c) 2017, ChaN
 - bcl-1.2.0, Urheberrechte (c) 2003-2006, Marcus Geelnard
 - Atmosphère (Exosphere-Typen/Panic, PRC-ID-Kernel-Patches),
   Urheberrechte (c) 2018-2019, Atmosphère-NX
 - elfload, Urheberrechte (c) 2014 Owen Shepherd, Urheberrechte (c) 2018 M4xw
 - Littlev Graphics Library, Urheberrechte (c) 2016 Gabor Kiss-Vamosi

                         ___
                      .-'   `'.
                     /         \
                     |         ;
                     |         |           ___.--,
            _.._     |0) = (0) |    _.---'`__.-( (_.
     __.--'`_.. '.__.\    '--. \_.-' ,.--'`     `""`
    ( ,.--'`   ',__ /./;   ;, '.__.'`    __
    _`) )  .---.__.' / |   |\   \__..--""  """--.,_
   `---' .'.''-._.-'`_./  /\ '.  \ _.--''````'''--._`-.__.'
         | |  .' _.-' |  |  \  \  '.               `----`
          \ \/ .'     \  \   '. '-._)
           \/ /        \  \    `=.__`'-.
           / /\         `) )    / / `"".`\
     , _.-'.'\ \        / /    ( (     / /
      `--'`   ) )    .-'.'      '.'.  | (
             (/`    ( (`          ) )  '-;   [switchbrew]
```
