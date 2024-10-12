# hekate - Nyx (Readme - Deutsch)

![Bild von Hekate](https://user-images.githubusercontent.com/3665130/60391760-bc1e8c00-9afe-11e9-8b7a-b065873081b2.png)

Benutzerdefinierter grafischer Nintendo Switch Bootloader, Firmware-Patcher, Werkzeuge und vieles mehr.

- [Funktionen](#features)
- [Bootloader-Verzeichnisse und -Dateien](#bootloader-folders-and-files)
- [Bootloader-Konfiguration](#bootloader-configuration)
  - [Globale Konfigurationsschlüssel/-werte von hekate](#hekate-global-configuration-keysvalues-when-entry-is-config)
  - [Schlüssel/Werte-Kombinationen für Booteinträge](#boot-entry-keyvalue-combinations)
  - [Schlüssel/Werte-Kombinationen für Booteinträge für Exosphère](#boot-entry-keyvalue-combinations-for-exosphère)
  - [Payload-Speicher](#payload-storage)
  - [Konfigurationsschlüssel/-werte von Nyx](#nyx-configuration-keysvalues-nyxini)

## Funktionen

- **Vollständig konfigurierbar und grafisch** mit Touchscreen- und Joycon-Eingabeunterstützung
- **Launcher-Stil, Hintergrund- und Farbthemen**
- **HOS (Switch OS) Bootloader** -- Für CFW Sys/Emu, OFW Sys und Stock Sys
- **Android & Linux Bootloader**
- **Payload-Launcher**
- **eMMC/emuMMC Backup-/Wiederherstellungs-Tools**
- **SD-Karten-Partition Manager** -- Bereitet SD-Karten für jede Kombination von HOS (Sys/emuMMC), Android und Linux vor und formatiert sie
- **emuMMC-Erstellung & -Manager** -- Kann auch bestehende emuMMC migrieren und reparieren
- **Switch Android & Linux Flasher**
- **USB-Massenspeicher (UMS) für SD/eMMC/emuMMC** -- Wandelt die Switch in einen SD-Kartenleser um
- **USB-Gamepad** -- Wandelt die Switch mit Joycon in ein USB-HID-Gamepad um
- **Hardware- und Peripherieinformationen** (SoC, Fuses, RAM, Display, Touch, eMMC, SD, Batterie, PSU, Ladegerät)
- **Viele weitere Tools** wie Archive Bit Fixer, Touch-Kalibrierung, SD/eMMC-Benchmark, AutoRCM-Enabler und mehr

## Bootloader-Verzeichnisse und -Dateien

| Verzeichnis/Datei              | Beschreibung                                                           |
| ------------------------------ | ----------------------------------------------------------------------- |
| bootloader                     | Hauptverzeichnis.                                                      |
|  \|__ bootlogo.bmp             | Wird verwendet, wenn kein `logopath`-Schlüssel gefunden wird. Benutzerdefiniert. Kann übersprungen werden. |
|  \|__ hekate_ipl.ini           | Haupt-Bootloader-Konfiguration und Boot-Einträge im Menü `Launch`.      |
|  \|__ nyx.ini                  | Nyx GUI-Konfiguration                                                  |
|  \|__ patches.ini              | Externe Patches hinzufügen. Kann übersprungen werden. Eine Vorlage kann [hier](./res/patches_template.ini) gefunden werden. |
|  \|__ update.bin               | Wird beim Booten geladen, wenn neuer. Normalerweise für Modchips. Automatisch aktualisiert und beim ersten Booten erstellt. |
| bootloader/ini/                | Für einzelne ini-Dateien. Menü `More configs`. Autoboot wird unterstützt. |
| bootloader/res/                | Nyx-Benutzerressourcen. Icons und mehr.                                |
|  \|__ background.bmp           | Nyx - Benutzerdefinierter Hintergrund. Benutzerdefiniert.              |
|  \|__ icon_switch.bmp          | Nyx - Standard-Icon für CFWs.                                          |
|  \|__ icon_payload.bmp         | Nyx - Standard-Icon für Payloads.                                      |
| bootloader/sys/                | hekate- und Nyx-Systemmodule-Verzeichnis.                              |
|  \|__ emummc.kipm              | emuMMC KIP1-Modul. Wichtig!                                            |
|  \|__ libsys_lp0.bso           | LP0 (Schlafmodus)-Modul. Wichtig!                                      |
|  \|__ libsys_minerva.bso       | Minerva Training Cell. Wird für das DRAM-Frequenztraining verwendet. Wichtig! |
|  \|__ nyx.bin                  | Nyx - Hekates GUI. Wichtig!                                            |
|  \|__ res.pak                  | Nyx-Ressourcenpaket. Wichtig!                                          |
|  \|__ thk.bin                  | Atmosphère Tsec Hovi Keygen. Wichtig!                                  |
| bootloader/screenshots/        | Verzeichnis, in dem Nyx-Screenshots gespeichert werden                 |
| bootloader/payloads/           | Für das Menü `Payloads`. Alle CFW-Bootloader, Tools, Linux-Payloads werden unterstützt. Autoboot wird nur unterstützt, indem sie in eine ini-Datei aufgenommen werden. |
| bootloader/libtools/           | Reserviert                                                            |

## Bootloader-Konfiguration

Der Bootloader kann über 'bootloader/hekate_ipl.ini' konfiguriert werden (wenn er auf der SD-Karte vorhanden ist). Jede ini-Sektion stellt einen Boot-Eintrag dar, außer der speziellen Sektion 'config', die die globale Konfiguration steuert.

Es gibt vier mögliche Eintragsarten. "**[ ]**": Boot-Eintrag, "**{ }**": Beschriftung, "**#**": Kommentar, "*neue Zeile*": .ini kosmetische neue Zeile.

**Du kannst eine Vorlage [hier](./res/hekate_ipl_template.ini) finden**

## Globale Konfigurationsschlüssel/-werte von hekate (wenn Eintrag *[config]* ist)

| Konfigurationsoption   | Beschreibung                                                |
| ---------------------- | ----------------------------------------------------------- |
| autoboot=0             | 0: Deaktivieren, #: Nummer des Boot-Eintrags zum automatischen Booten.             |
| autoboot_list=0        | 0: Liest den `autoboot`-Boot-Eintrag aus hekate_ipl.ini, 1: Liest aus ini-Verzeichnis (ini-Dateien sind ASCII-sortiert). |
| bootwait=3             | 0: Deaktivieren (Deaktiviert auch das Bootlogo. Wenn **VOL-** seit der Injektion gedrückt gehalten wird, wird das Menü angezeigt.), #: Wartezeit für **VOL-**, um das Menü aufzurufen. Max.: 20s. |
| noticker=0             | 0: Animierte Linie wird während des benutzerdefinierten Bootlogos gezeichnet und zeigt die verbleibende Zeit an, um zum Menü zu springen. 1: Deaktivieren. |
| autohosoff=1           | 0: Deaktivieren, 1: Wenn aus HOS durch einen RTC-Alarm aufgeweckt, zeigt es das Logo und schaltet dann vollständig aus, 2: Kein Logo, schaltet sofort aus.|
| autonogc=1             | 0: Deaktivieren, 1: Wendet automatisch den nogc-Patch an, wenn nicht gebrannte Sicherungen gefunden werden und ein HOS >= 4.0.0 gestartet wird. |
| bootprotect=0          | 0: Deaktivieren, 1: Schützt das Bootloader-Verzeichnis vor Beschädigung, indem Lesen oder Bearbeiten in HOS nicht erlaubt wird. |
| updater2p=0            | 0: Deaktivieren, 1: Erzwingt Updates (falls erforderlich) der reboot2payload-Binärdatei zu hekate. |
| backlight=100          | Bildschirm-Helligkeitsstufe. 0-255.                             |

## Schlüssel/Werte-Kombinationen für Booteinträge

| Konfigurationsoption      | Beschreibung                                                |
| ------------------------ | ---------------------------------------------------------- |
| warmboot={DATEIPFAD}     | Ersetzt die Warmboot-Binärdatei                               |
| secmon={DATEIPFAD}       | Ersetzt die Sicherheitsmonitor-Binärdatei                     |
| kernel={DATEIPFAD}       | Ersetzt die Kernel-Binärdatei                                 |
| kip1={DATEIPFAD}         | Ersetzt/Fügt Kernel-Initialprozess hinzu. Mehrere können eingestellt werden. |
| kip1={VERZEICHNISPFAD}/* | Lädt jede .kip/.kip1 innerhalb eines Verzeichnisses. Kompatibel mit einzelnen kip1-Schlüsseln. |
| fss0={DATEIPFAD}         | Nimmt eine Atmosphere `package3`-Binärdatei (ehemals fusee-secondary.bin) und `extrahiert` alle benötigten Teile daraus. kips, exosphere, warmboot und mesosphere, falls aktiviert. |
| fss0experimental=1       | Ermöglicht das Laden von experimentellem Inhalt aus einem FSS0-Speicher |
| exofatal={DATEIPFAD}     | Ersetzt die exosphere-fatal-Binärdatei für Mariko             |
| ------------------------ | ---------------------------------------------------------- |
| kip1patch=patchname      | Aktiviert einen kip1-Patch. Mit mehreren Zeilen und/oder in einer Zeile mit `,` als Trennzeichen angeben. Wenn der eigentliche Patch nicht gefunden wird, wird eine Warnung angezeigt |
| emupath={VERZEICHNISPFAD}| Erzwingt die Verwendung des ausgewählten emuMMC. (=emuMMC/RAW1, =emuMMC/SD00 usw.). emuMMC muss von hekate erstellt werden, da es die raw_based/file_based-Dateien verwendet. |
| emummcforce=1            | Erzwingt die Verwendung von emuMMC. Wenn emummc.ini deaktiviert ist oder nicht gefunden wird, wird ein Fehler verursacht. |
| emummc_force_disable=1   | Deaktiviert emuMMC, falls es aktiviert ist.                   |
| stock=1                  | Deaktiviert unnötiges Kernel-Patching und CFW-kips beim Ausführen von Stock oder Semi-Stock. `Wenn emuMMC aktiviert ist, wird emummc_force_disable=1 benötigt.` emuMMC wird im Stock-Modus nicht unterstützt. Wenn zusätzliche KIPs benötigt werden, außer den OFW-KIPs, kannst du sie mit dem Schlüssel `kip1` definieren. Kein kip sollte verwendet werden, der auf Atmosphère-Patching angewiesen ist, da es hängen bleibt. Wenn `NOGC` benötigt wird, verwende `kip1patch=nogc`. |
| fullsvcperm=1            | Deaktiviert SVC-Überprüfung (volle Dienstberechtigungen). Funktioniert nicht mit Mesosphere als Kernel. |
| debugmode=1              | Aktiviert den Debug-Modus. Veraltet bei Verwendung mit exosphere als secmon. |
| atmosphere=1             | Aktiviert Atmosphère-Patching. Nicht erforderlich, wenn `fss0` verwendet wird. |
| ------------------------ | ---------------------------------------------------------- |
| payload={DATEIPFAD}      | Payload-Start. Werkzeuge, Android/Linux, CFW-Bootloader usw. Jeder Schlüssel oben, der damit verwendet wird, wird nicht berücksichtigt. |
| ------------------------ | ---------------------------------------------------------- |
| l4t=1                    | L4T Linux/Android nativer Start.                            |
| boot_prefixes={VERZEICHNISPFAD} | L4T-Bootstack-Verzeichnis.                              |
| ram_oc=0                 | L4T RAM Overclocking. Weitere Informationen findest du in README_CONFIG.txt. |
| ram_oc_vdd2=1100         | L4T RAM VDD2-Spannung. Setzt VDD2 (T210B01) oder VDD2/VDDQ (T210) Spannung. 1050-1175. |
| ram_oc_vddq=600          | L4T RAM VDDQ-Spannung. Setzt VDDQ (T210B01). 550-650.         |
| uart_port=0              | Aktiviert Logging auf dem seriellen Port für L4T uboot/kernel. |
| Zusätzliche Schlüssel    | Jede Distribution unterstützt weitere Schlüssel. Weitere Informationen findest du in README_CONFIG.txt. |
| ------------------------ | ---------------------------------------------------------- |
| bootwait=3               | Überschreibt globalen bootwait aus `[config]`.                 |
| id=IDNAME                | Identifiziert Booteintrag für erzwungenes Booten über ID. Max. 7 Zeichen. |
| logopath={DATEIPFAD}     | Wenn es existiert, wird das angegebene Bitmap geladen. Andernfalls wird `bootloader/bootlogo.bmp` verwendet, falls vorhanden. |
| icon={DATEIPFAD}         | Erzwingt, dass Nyx das hier definierte Icon verwendet. Wenn dies nicht gefunden wird, wird nach einer bmp gesucht, die wie der Booteintrag benannt ist ([Test 2] -> `bootloader/res/Test 2.bmp`). Andernfalls werden Standard-Icons verwendet. |

**Hinweis1**: Bei Verwendung des Platzhalters (`/*`) mit `kip1` kannst du weiterhin die normale `kip1`-Option danach verwenden, um zusätzliche einzelne kips zu laden.

**Hinweis2**: Bei Verwendung von FSS0 werden exosphere, warmboot und alle Kern-kips analysiert. Du kannst die ersten beiden durch Verwendung von `secmon`/`warmboot` nach Definition von `fss0` überschreiben.
Du kannst `kip1` definieren, um einen zusätzlichen kip oder mehrere über die Verwendung des Platzhalters (`/*`) zu laden.

**Warnung**: Vorsicht, wenn du *fss0-Kern*-kips definierst, wenn `fss0` verwendet wird oder das Verzeichnis (bei Verwendung von `/*`) diese enthält.
Dies ist der Fall, wenn die kips untereinander inkompatibel sind. Wenn sie kompatibel sind, kannst du `fss0`-kips ohne Probleme überschreiben (nützlich zum Testen mit Zwischen-kip-Änderungen). In solchen Fällen muss die `kip1`-Zeile unter der `fss0`-Zeile stehen.

## Schlüssel/Werte-Kombinationen für Booteinträge für Exosphère

| Konfigurationsoption      | Beschreibung                                                |
| ------------------------ | ---------------------------------------------------------- |
| nouserexceptions=1       | Deaktiviert Benutzermodus-Ausnahme-Handler, wenn mit Exosphère gepaart. |
| userpmu=1                | Ermöglicht Benutzern den Zugriff auf PMU, wenn mit Exosphère gepaart.     |
| cal0blank=1              | Überschreibt Exosphère-Konfig `blank_prodinfo_{sys/emu}mmc`. Wenn dieser Schlüssel nicht existiert, wird `exosphere.ini` verwendet. |
| cal0writesys=1           | Überschreibt Exosphère-Konfig `allow_writing_to_cal_sysmmc`. Wenn dieser Schlüssel nicht existiert, wird `exosphere.ini` verwendet. |
| usb3force=1              | Überschreibt die Systemsettings-mitm-Konfig `usb30_force_enabled`. Wenn dieser Schlüssel nicht existiert, wird `system_settings.ini` verwendet. |

**Hinweis**: `cal0blank`, `cal0writesys`, `usb3force`, wie angegeben, überschreiben die `exosphere.ini` oder `system_settings.ini`. 0: Deaktivieren, 1: Aktivieren, Schlüssel fehlt: Originalwert verwenden.

**Hinweis2**: `blank_prodinfo_{sys/emu}mmc`, `allow_writing_to_cal_sysmmc` und `usb30_force_enabled` in `exosphere.ini` und `system_settings.ini` sind die einzigen Atmosphere-Konfigurationsschlüssel, die die hekate-Boot-Konfiguration extern beeinflussen können, **wenn** die entsprechenden Schlüssel in der hekate-Konfig fehlen.

## Payload-Speicher

hekate hat einen Bootspeicher in der Binärdatei, der ihm hilft, außerhalb der BPMP-Umgebung zu konfigurieren:

| Offset / Name           | Beschreibung                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| '0x94' boot_cfg         | bit0: `Force AutoBoot`, bit1: `Show launch log`, bit2: `Boot from ID`, bit3: `Boot to emuMMC`. |
| '0x95' autoboot         | Wenn `Force AutoBoot`, 0: Erzwingt das Menü, sonst wird dieser Eintrag gebootet.   |
| '0x96' autoboot_list    | Wenn `Force AutoBoot` und `autoboot`, dann wird aus dem ini-Verzeichnis gebootet. |
| '0x97' extra_cfg        | Wenn Menü erzwungen: bit5: `Run UMS`.                             |
| '0x98' xt_str[128]      | Hängt von den gesetzten cfg-Bits ab.                                      |
| '0x98' ums[1]           | Wenn `Run UMS` gesetzt ist, wird das ausgewählte UMS gestartet. 0: SD, 1: eMMC BOOT0, 2: eMMC BOOT1, 3: eMMC GPP, 4: emuMMC BOOT0, 5: emuMMC BOOT1, 6: emuMMC GPP,  |
| '0x98' id[8]            | Wenn `Boot from ID` gesetzt ist, wird automatisch nach allen ini-Dateien gesucht und der Booteintrag mit dieser ID wird gebootet. Muss NULL-terminiert sein. |
| '0xA0' emummc_path[120] | Wenn `Boot to emuMMC` gesetzt ist, wird der aktuelle emuMMC (Booteintrag oder emummc.ini) überschrieben. Muss NULL-terminiert sein. |

## Konfigurationsschlüssel/-werte von Nyx (nyx.ini)

| Konfigurationsoption      | Beschreibung                                                |
| ------------------------ | ---------------------------------------------------------- |
| themebg=2d2d2d           | Setzt Nyx-Hintergrundfarbe in HEX. EXPERIMENTELL.            |
| themecolor=167           | Setzt Nyx-Farbe der Text-Highlights.                         |
| entries5col=0            | 1: Setzt Launch-Eintrags-Spalten von 4 auf 5 pro Zeile. Für insgesamt 10 Einträge. |
| timeoff=100              | Setzt Zeitversatz in HEX. Muss im HOS-Epoch-Format sein       |
| homescreen=0             | Setzt Startbildschirm. 0: Startmenü, 1: Alle Konfigurationen (führt `Launch` und `More configs` zusammen), 2: Launch, 3: Weitere Konfigurationen. |
| verification=1           | 0: Deaktiviert Backup-/Wiederherstellungsüberprüfung, 1: Sparse (blockbasiert, schnell und meist zuverlässig), 2: Vollständig (sha256-basiert, langsam und 100% zuverlässig). |
| ------------------------ | ------- Die folgenden Optionen können nur in nyx.ini bearbeitet werden ------- |
| umsemmcrw=0              | 1: eMMC/emuMMC UMS wird standardmäßig als beschreibbar eingebunden. |
| jcdisable=0              | 1: Deaktiviert Joycon-Treiber vollständig.                      |
| jcforceright=0           | 1: Erzwingt die Verwendung des rechten Joycon als Hauptmaussteuerung.   |
| bpmpclock=1              | 0: Auto, 1: Schnellste, 2: Schneller, 3: Schnell. Verwende 2 oder 3, wenn Nyx hängt oder einige Funktionen wie UMS/Backup-Überprüfung fehlschlagen. |

```plaintext
hekate  (c) 2018,      naehrwert, st4rk.
        (c) 2018-2024, CTCaer.

Nyx GUI (c) 2019-2024, CTCaer.

Danke an: derrek, nedwill, plutoo, shuffle2, smea, thexyz, yellows8.
Grüße an: fincs, hexkyz, SciresM, Shiny Quagsire, WinterMute.

Verwendete Open-Source- und kostenlose Pakete:
 - Littlev Graphics Library,
   Copyright (c) 2016-2018 Gabor Kiss-Vamosi
 - FatFs R0.13c,
   Copyright (c) 2006-2018, ChaN
   Copyright (c) 2018-2022, CTCaer
 - bcl-1.2.0,
   Copyright (c) 2003-2006, Marcus Geelnard
 - blz,
   Copyright (c) 2018, SciresM
 - elfload,
   Copyright (c) 2014 Owen Shepherd,
   Copyright (c) 2018 M4xw

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

---

## hekate - Nyx (Readme - English)

![Image of Hekate](https://user-images.githubusercontent.com/3665130/60391760-bc1e8c00-9afe-11e9-8b7a-b065873081b2.png)

Custom Graphical Nintendo Switch bootloader, firmware patcher, tools, and many more.

- [Features](#features)
- [Bootloader folders and files](#bootloader-folders-and-files)
- [Bootloader configuration](#bootloader-configuration)
  - [hekate global Configuration keys/values](#hekate-global-configuration-keysvalues-when-entry-is-config)
  - [Boot entry key/value combinations](#boot-entry-keyvalue-combinations)
  - [Boot entry key/value combinations for Exosphère](#boot-entry-keyvalue-combinations-for-exosphère)
  - [Payload storage](#payload-storage)
  - [Nyx Configuration keys/values](#nyx-configuration-keysvalues-nyxini)

## Features

- **Fully Configurable and Graphical** with Touchscreen and Joycon input support
- **Launcher Style, Background and Color Themes**
- **HOS (Switch OS) Bootloader** -- For CFW Sys/Emu, OFW Sys and Stock Sys
- **Android & Linux Bootloader**
- **Payload Launcher**
- **eMMC/emuMMC Backup/Restore Tools**
- **SD Card Partition Manager** -- Prepares and formats SD Card for any combo of HOS (Sys/emuMMC), Android and Linux
- **emuMMC Creation & Manager** -- Can also migrate and fix existing emuMMC
- **Switch Android & Linux flasher**
- **USB Mass Storage (UMS) for SD/eMMC/emuMMC** -- Converts Switch into a SD Card Reader
- **USB Gamepad** -- Converts Switch with Joycon into a USB HID Gamepad
- **Hardware and Peripherals info** (SoC, Fuses, RAM, Display, Touch, eMMC, SD, Battery, PSU, Charger)
- **Many other tools** like Archive Bit Fixer, Touch Calibration, SD/eMMC Benchmark, AutoRCM enabler and more

## Bootloader folders and files

| Folder/File              | Description                                                           |
| ------------------------ | --------------------------------------------------------------------- |
| bootloader               | Main folder.                                                          |
|  \|__ bootlogo.bmp       | It is used if no `logopath` key is found. User provided. Can be skipped. |
|  \|__ hekate_ipl.ini     | Main bootloader configuration and boot entries in `Launch` menu.      |
|  \|__ nyx.ini            | Nyx GUI configuration                                                 |
|  \|__ patches.ini        | Add external patches. Can be skipped. A template can be found [here](./res/patches_template.ini) |
|  \|__ update.bin         | If newer, it is loaded at boot. Normally for modchips. Auto updated and created at first boot. |
| bootloader/ini/          | For individual inis. `More configs` menu. Autoboot is supported.   |
| bootloader/res/          | Nyx user resources. Icons and more.                                   |
|  \|__ background.bmp     | Nyx - Custom background. User provided.                               |
|  \|__ icon_switch.bmp    | Nyx - Default icon for CFWs.                                          |
|  \|__ icon_payload.bmp   | Nyx - Default icon for Payloads.                                      |
| bootloader/sys/          | hekate and Nyx system modules folder.                                 |
|  \|__ emummc.kipm        | emuMMC KIP1 module. !Important!                                       |
|  \|__ libsys_lp0.bso     | LP0 (sleep mode) module. Important!                                   |
|  \|__ libsys_minerva.bso | Minerva Training Cell. Used for DRAM Frequency training. !Important!  |
|  \|__ nyx.bin            | Nyx - hekate's GUI. !Important!                                       |
|  \|__ res.pak            | Nyx resources package. !Important!                                    |
|  \|__ thk.bin            | Atmosphère Tsec Hovi Keygen. !Important!                              |
| bootloader/screenshots/  | Folder where Nyx screenshots are saved                                |
| bootloader/payloads/     | For the `Payloads` menu. All CFW bootloaders, tools, Linux payloads are supported. Autoboot only supported by including them into an ini. |
| bootloader/libtools/     | Reserved                                                              |

## Bootloader configuration

The bootloader can be configured via 'bootloader/hekate_ipl.ini' (if it is present on the SD card). Each ini section represents a boot entry, except for the special section 'config' that controls the global configuration.

There are four possible type of entries. "**[ ]**": Boot entry, "**{ }**": Caption, "**#**": Comment, "*newline*": .ini cosmetic newline.

**You can find a template [Here](./res/hekate_ipl_template.ini)**

### hekate Global Configuration keys/values (when entry is *[config]*)

| Config option      | Description                                                |
| ------------------ | ---------------------------------------------------------- |
| autoboot=0         | 0: Disable, #: Boot entry number to auto boot.             |
| autoboot_list=0    | 0: Read `autoboot` boot entry from hekate_ipl.ini, 1: Read from ini folder (ini files are ASCII ordered). |
| bootwait=3         | 0: Disable (It also disables bootlogo. Having **VOL-** pressed since injection goes to menu.), #: Time to wait for **VOL-** to enter menu. Max: 20s. |
| noticker=0         | 0: Animated line is drawn during custom bootlogo, signifying time left to skip to menu. 1: Disable. |
| autohosoff=1       | 0: Disable, 1: If woke up from HOS via an RTC alarm, shows logo, then powers off completely, 2: No logo, immediately powers off.|
| autonogc=1         | 0: Disable, 1: Automatically applies nogc patch if unburnt fuses found and a >= 4.0.0 HOS is booted. |
| bootprotect=0      | 0: Disable, 1: Protect bootloader folder from being corrupted by disallowing reading or editing in HOS. |
| updater2p=0        | 0: Disable, 1: Force updates (if needed) the reboot2payload binary to be hekate. |
| backlight=100      | Screen backlight level. 0-255.                             |

### Boot entry key/value combinations

| Config option          | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| warmboot={FILE path}   | Replaces the warmboot binary                               |
| secmon={FILE path}     | Replaces the security monitor binary                       |
| kernel={FILE path}     | Replaces the kernel binary                                 |
| kip1={FILE path}       | Replaces/Adds kernel initial process. Multiple can be set. |
| kip1={FOLDER path}/*   | Loads every .kip/.kip1 inside a folder. Compatible with single kip1 keys. |
| fss0={FILE path}       | Takes an Atmosphere `package3` binary (formerly fusee-secondary.bin) and `extracts` all needed parts from it. kips, exosphere, warmboot and mesophere if enabled. |
| fss0experimental=1     | Enables loading of experimental content from a FSS0 storage |
| exofatal={FILE path}   | Replaces the exosphere fatal binary for Mariko             |
| ---------------------- | ---------------------------------------------------------- |
| kip1patch=patchname    | Enables a kip1 patch. Specify with multiple lines and/or in one line with `,` as separator. If actual patch is not found, a warning will show up |
| emupath={FOLDER path}  | Forces emuMMC to use the selected one. (=emuMMC/RAW1, =emuMMC/SD00, etc). emuMMC must be created by hekate because it uses the raw_based/file_based files. |
| emummcforce=1          | Forces the use of emuMMC. If emummc.ini is disabled or not found, then it causes an error. |
| emummc_force_disable=1 | Disables emuMMC, if it's enabled.                           |
| stock=1                | OFW via hekate bootloader. Disables unneeded kernel patching and CFW kips when running stock. `If emuMMC is enabled, emummc_force_disable=1` is required. emuMMC is not supported on stock. If additional KIPs are needed other than OFW's, you can define them with `kip1` key. No kip should be used that relies on Atmosphère patching, because it will hang. If `NOGC` is needed, use `kip1patch=nogc`. |
| fullsvcperm=1          | Disables SVC verification (full services permission). Doesn't work with Mesosphere as kernel. |
| debugmode=1            | Enables Debug mode. Obsolete when used with exosphere as secmon. |
| atmosphere=1           | Enables Atmosphère patching. Not needed when `fss0` is used. |
| ---------------------- | ---------------------------------------------------------- |
| payload={FILE path}    | Payload launching. Tools, Android/Linux, CFW bootloaders, etc. Any key above when used with that, doesn't get into account. |
| ---------------------- | ---------------------------------------------------------- |
| l4t=1                  | L4T Linux/Android native launching.                        |
| boot_prefixes={FOLDER path} | L4T bootstack directory.                              |
| ram_oc=0               | L4T RAM Overclocking. Check README_CONFIG.txt for more info. |
| ram_oc_vdd2=1100       | L4T RAM VDD2 Voltage. Set VDD2 (T210B01) or VDD2/VDDQ (T210) voltage. 1050-1175. |
| ram_oc_vddq=600        | L4T RAM VDDQ Voltage. Set VDDQ (T210B01). 550-650.         |
| uart_port=0            | Enables logging on serial port for L4T uboot/kernel.       |
| Additional keys        | Each distro supports more keys. Check README_CONFIG.txt  for more info. |
| ---------------------- | ---------------------------------------------------------- |
| bootwait=3             | Overrides global bootwait from `[config]`.                 |
| id=IDNAME              | Identifies boot entry for forced boot via id. Max 7 chars. |
| logopath={FILE path}   | If it exists, it will load the specified bitmap. Otherwise `bootloader/bootlogo.bmp` will be used if exists |
| icon={FILE path}       | Force Nyx to use the icon defined here. If this is not found, it will check for a bmp named as the boot entry ([Test 2] -> `bootloader/res/Test 2.bmp`). Otherwise defaults will be used. |

**Note1**: When using the wildcard (`/*`) with `kip1` you can still use the normal `kip1` after that to load extra single kips.

**Note2**: When using FSS0 it parses exosphere, warmboot and all core kips. You can override the first 2 by using `secmon`/`warmboot` after defining `fss0`.
You can define `kip1` to load an extra kip or many via the wildcard (`/*`) usage.

**Warning**: Careful when you define *fss0 core* kips when using `fss0` or the folder (when using `/*`) includes them.
This is in case the kips are incompatible between them. If compatible, you can override `fss0` kips with no issues (useful for testing with intermediate kip changes). In such cases, the `kip1` line must be under `fss0` line.

### Boot entry key/value combinations for Exosphère

| Config option          | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| nouserexceptions=1     | Disables usermode exception handlers when paired with Exosphère. |
| userpmu=1              | Enables user access to PMU when paired with Exosphère.     |
| cal0blank=1            | Overrides Exosphère config `blank_prodinfo_{sys/emu}mmc`. If that key doesn't exist, `exosphere.ini` will be used. |
| cal0writesys=1         | Overrides Exosphère config `allow_writing_to_cal_sysmmc`. If that key doesn't exist, `exosphere.ini` will be used. |
| usb3force=1            | Overrides system settings mitm config `usb30_force_enabled`. If that key doesn't exist, `system_settings.ini` will be used. |

**Note**: `cal0blank`, `cal0writesys`, `usb3force`, as stated override the `exosphere.ini` or `system_settings.ini`. 0: Disable, 1: Enable, Key Missing: Use original value.

**Note2**: `blank_prodinfo_{sys/emu}mmc`, `allow_writing_to_cal_sysmmc` and `usb30_force_enabled` in `exosphere.ini` and `system_settings.ini` respectively, are the only atmosphere config keys that can affect hekate booting configuration externally, **if** the equivalent keys in hekate config are missing.

### Payload storage

hekate has a boot storage in the binary that helps it configure it outside of BPMP enviroment:

| Offset / Name           | Description                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| '0x94' boot_cfg         | bit0: `Force AutoBoot`, bit1: `Show launch log`, bit2: `Boot from ID`, bit3: `Boot to emuMMC`. |
| '0x95' autoboot         | If `Force AutoBoot`, 0: Force go to menu, else boot that entry.   |
| '0x96' autoboot_list    | If `Force AutoBoot` and `autoboot` then it boots from ini folder. |
| '0x97' extra_cfg        | When menu is forced: bit5: `Run UMS`.                             |
| '0x98' xt_str[128]      | Depends on the set cfg bits.                                      |
| '0x98' ums[1]           | When `Run UMS` is set, it will launch the selected UMS. 0: SD, 1: eMMC BOOT0, 2: eMMC BOOT1, 3: eMMC GPP, 4: emuMMC BOOT0, 5: emuMMC BOOT1, 6: emuMMC GPP,  |
| '0x98' id[8]            | When `Boot from ID` is set, it will search all inis automatically and find the boot entry with that id and boot it. Must be NULL terminated. |
| '0xA0' emummc_path[120] | When `Boot to emuMMC` is set, it will override the current emuMMC (boot entry or emummc.ini). Must be NULL terminated. |

### Nyx Configuration keys/values (nyx.ini)

| Config option      | Description                                                |
| ------------------ | ---------------------------------------------------------- |
| themebg=2d2d2d     | Sets Nyx background color in HEX. EXPERIMENTAL.            |
| themecolor=167     | Sets Nyx color of text highlights.                         |
| entries5col=0      | 1: Sets Launch entry columns from 4 to 5 per line. For a total of 10 entries. |
| timeoff=100        | Sets time offset in HEX. Must be in HOS epoch format       |
| homescreen=0       | Sets home screen. 0: Home menu, 1: All configs (merges Launch and More configs), 2: Launch, 3: More Configs. |
| verification=1     | 0: Disable Backup/Restore verification, 1: Sparse (block based, fast and mostly reliable), 2: Full (sha256 based, slow and 100% reliable). |
| ------------------ | ------- The following options can only be edited in nyx.ini ------- |
| umsemmcrw=0        | 1: eMMC/emuMMC UMS will be mounted as writable by default. |
| jcdisable=0        | 1: Disables Joycon driver completely.                      |
| jcforceright=0     | 1: Forces right joycon to be used as main mouse control.   |
| bpmpclock=1        | 0: Auto, 1: Fastest, 2: Faster, 3: Fast. Use 2 or 3 if Nyx hangs or some functions like UMS/Backup Verification fail. |

```plaintext
hekate  (c) 2018,      naehrwert, st4rk.
        (c) 2018-2024, CTCaer.

Nyx GUI (c) 2019-2024, CTCaer.

Thanks to: derrek, nedwill, plutoo, shuffle2, smea, thexyz, yellows8.
Greetings to: fincs, hexkyz, SciresM, Shiny Quagsire, WinterMute.

Open source and free packages used:
 - Littlev Graphics Library,
   Copyright (c) 2016-2018 Gabor Kiss-Vamosi
 - FatFs R0.13c,
   Copyright (c) 2006-2018, ChaN
   Copyright (c) 2018-2022, CTCaer
 - bcl-1.2.0,
   Copyright (c) 2003-2006, Marcus Geelnard
 - blz,
   Copyright (c) 2018, SciresM
 - elfload,
   Copyright (c) 2014 Owen Shepherd,
   Copyright (c) 2018 M4xw

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
