# TUTORIAL

## Pros und Cons der Installation von Arch/KDE Plasma

| Pros                                                      | Cons                                                          |
| --------------------------------------------------------- | ------------------------------------------------------------- |
| Rolling Release: Immer aktuelle Software und Treiber      | Manchmal Bastelarbeit durch Updates/eventuelle Bugs           |
| Extrem gut dokumentierte Problemlösungen                  | Nur eingeschränkter Support für Kernel-Level-AntiCheats (z.B. Riot Vanguard)               |
| KDE Plasma: Moderne, benutzerfreundliche Desktop-Umgebung | Manuelle Installation und Konfiguration erforderlich          |
| Große Community und umfangreiche Dokumentation            | Eingeschränkterer offizieller Support als bei kommerziellen Distributionen |

## Hier erstmal eine einfache Anleitung zur Installation

### 1. Vorbereitung

Du benötigst:

- USB-Stick (darf keine wichtigen Daten enthalten, wird gelöscht!) mit mindestens 8 GB Speicherplatz, ich würde allerdings maximal 32/64 GB empfehlen.
- ca 2 GB Speicherplatz auf deinem System
- einen PC mit mindestens 64 GB, auf dem Linux installiert werden soll

### 2. [Installationsmedium erstellen](https://wiki.archlinux.org/title/USB_flash_installation_medium)

<details>
<summary><strong><a href=https://wiki.archlinux.org/title/USB_flash_installation_medium#In_GNU/Linux>Linux</a></strong></summary>

#### Methode 1: [dd](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_basic_command_line_utilities) (empfohlen)

<details>
    <summary>dd</summary>

```bash
dd bs=4M if=archlinux.iso of=/dev/sdx conv=fsync oflag=direct status=progress
```

</details>

#### Methode 2: [cp](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_basic_command_line_utilities)

<details>
 <summary>cp</summary>

```bash
cp path/to/archlinux.iso /dev/sdx
```

</details>

#### Methode 3: [KDE ISO Image Writer](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_KDE_ISO_Image_Writer)

<details>
 <summary>KDE ISO Image Writer</summary>

> Der KDE ISO Image Writer ist in den meisten Distributionen enthalten (apt, pacman etc.). Dort wählt man dann den Stick und die zugehörige ISO aus und der Installationsstick wird erstellt.


</details>
</details>

***

<details>
<summary><strong><a href=https://wiki.archlinux.org/title/USB_flash_installation_medium#In_Windows>Windows</a></strong></summary>

#### Methode 1: [KDE ISO Image Writer](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_KDE_ISO_Image_Writer_2) (empfohlen)

<details>
 <summary>KDE ISO Image Writer</summary>


> Der KDE ISO Image Writer ist unter [dieser Adresse](https://download.kde.org/stable/isoimagewriter/1.0.0/isoimagewriter-1.0.0.exe) kostenlos zum Download verfügbar. Empfohlen wird eine Installation über WinGet, sofern möglich. Dort wählt man dann den Stick und die zugehörige ISO aus und der Installationsstick wird erstellt.


</details>

#### Methode 2: [Rufus](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_Rufus)

<details>
 <summary>Rufus</summary>

> [Rufus](https://rufus.ie/de/) ermöglich genauso wie der ISO Image Writer eine einfache GUI, mit der man das Installationsmedium erstellen kann.

</details>

#### Methode 3: [DD for Windows](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_dd_for_Windows)

<details>
 <summary>dd</summary>

> Bitte folge dem Tutorial auf der [offiziellen Arch-Linux-Wiki-Seite](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_dd_for_Windows)

</details>
</details>

***

<details>
<summary><strong><a href=https://wiki.archlinux.org/title/USB_flash_installation_medium#In_macOS>MacOS</a></strong></summary>

> [Arch-Wiki](https://wiki.archlinux.org/title/USB_flash_installation_medium#In_macOS)

</details>

### 3. Reboot ins Arch Linux

Unterschiedlich von Gerät zu Gerät, aber normalerweise: 
- Runterfahren
- Anschalten
- Beim Hochfahren direkt nach dem Drücken der Anschalttaste meistens "entfernen/ENTF" gedrückt halten/wiederholt drücken
- Beim Auswahlbildschirm die ausgewählte Option mit Enter-Taste bestätigen