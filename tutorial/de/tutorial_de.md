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

***

### 4. Die Installation selbst

Du bist jetzt im Livesystem und siehst eine schwarze Konsole. Keine Panik, das ist der unbequemste Moment der ganzen Installation und er dauert etwa zehn Minuten.

<details>
<summary><strong>Erstmal Tastatur und Internet</strong></summary>

> Deutsches Tastaturlayout, sonst suchst du dich beim Passwort dumm und dämlich:
>
> ```bash
> loadkeys de-latin1
> ```
>
> Per Kabel bist du schon online. Für WLAN:
>
> ```bash
> iwctl
> station wlan0 get-networks
> station wlan0 connect DEIN_WLAN
> exit
> ```
>
> Testen mit `ping -c3 archlinux.org`.

</details>

<details>
<summary><strong>archinstall starten</strong></summary>

> ```bash
> archinstall
> ```
>
> Das ist der offizielle Installer, du klickst dich mit den Pfeiltasten durch ein Menü. Die Punkte, auf die es ankommt:
>
> | Menüpunkt              | Was du willst                                                    |
> | ---------------------- | ---------------------------------------------------------------- |
> | Disk configuration     | Die Platte, auf die Arch soll (siehe Warnung unten)              |
> | Bootloader             | `grub`, wenn du Dualboot planst, sonst ist `systemd-boot` schlanker |
> | Profile                | `Desktop` und darin `KDE Plasma`                                  |
> | Audio                  | `pipewire`                                                        |
> | Network configuration  | `Use NetworkManager`                                              |
> | Additional packages    | `git base-devel pacman-contrib`                                   |
> | User account           | Benutzer anlegen und als Superuser markieren, sonst kein `sudo`  |
>
> Danach "Install" und warten. Der Rest läuft von allein.

</details>

> **Achtung bei der Plattenauswahl:** Der Punkt "Use a best-effort default partition layout" löscht die ausgewählte Platte komplett. Wenn auf dem Rechner noch Windows liegt und bleiben soll, darfst du das auf keinen Fall nehmen. Dann brauchst du manuelle Partitionierung und freien, nicht zugewiesenen Speicher. Mehr dazu unten bei [Dualboot](#6-dualboot-mit-windows).

Am Ende fragt archinstall, ob du noch ins neue System willst ("chroot"). Kannst du mit Nein beantworten. Stick rausziehen, neu starten, fertig.

***

### 5. Der erste Start

Du landest im Login und danach auf einem leeren KDE-Desktop. Die folgenden Sachen machst du einmal und danach nie wieder.

<details>
<summary><strong>Netzwerk</strong></summary>

> Wenn du bei archinstall `NetworkManager` gewählt hast, ist alles schon da. WLAN wählst du oben rechts im Systemabschnitt der Leiste aus.
>
> Falls das Symbol fehlt:
>
> ```bash
> sudo pacman -S networkmanager plasma-nm
> sudo systemctl enable --now NetworkManager
> ```

</details>

<details>
<summary><strong>Grafiktreiber</strong></summary>

> Der offene AMD- und Intel-Treiber ist schon im Kernel, du installierst nur die Grafikbibliotheken dazu. Die `lib32`-Pakete brauchst du für Spiele und Wine, dafür muss `multilib` in `/etc/pacman.conf` aktiv sein.
>
> AMD:
>
> ```bash
> sudo pacman -S mesa lib32-mesa vulkan-radeon lib32-vulkan-radeon
> ```
>
> Intel:
>
> ```bash
> sudo pacman -S mesa lib32-mesa vulkan-intel lib32-vulkan-intel
> ```
>
> NVIDIA ist der einzige Fall, wo es etwas fummeliger wird. Für alles ab RTX 2000:
>
> ```bash
> sudo pacman -S nvidia-open-dkms nvidia-utils lib32-nvidia-utils
> ```
>
> Bei älteren Karten nimmst du `nvidia-dkms` statt `nvidia-open-dkms`. Danach einmal neu starten. Details stehen im [Wiki](https://wiki.archlinux.org/title/NVIDIA).

</details>

<details>
<summary><strong>Ton</strong></summary>

> Mit `pipewire` aus dem Installer läuft der Ton normalerweise sofort. Wenn nicht:
>
> ```bash
> sudo pacman -S pipewire pipewire-pulse pipewire-alsa wireplumber
> ```
>
> Danach ab- und wieder anmelden. Ausgabegerät wählst du per Klick auf das Lautsprechersymbol in der Leiste.

</details>

<details>
<summary><strong>yay installieren</strong></summary>

> Das brauchst du für alles aus dem AUR, und das ist der halbe Grund für Arch. Siehe auch [Kapitel 9](#9-updates-im-blick-behalten).
>
> ```bash
> sudo pacman -S --needed base-devel git
> git clone https://aur.archlinux.org/yay.git
> cd yay
> makepkg -si
> ```
>
> Danach kannst du den `yay`-Ordner löschen. Ab jetzt installierst du mit `yay -S paketname` und bekommst offizielle Pakete und AUR aus demselben Befehl.

</details>

***

### 6. Dualboot mit Windows

Nur für dich, wenn Windows auf dem Rechner bleiben soll. Wenn du eh alles plattgemacht hast, überspring das Kapitel.

<details>
<summary><strong>Zuerst: Windows-Schnellstart ausschalten</strong></summary>

> Das ist der wichtigste Punkt im ganzen Kapitel und wird am häufigsten vergessen. Windows fährt mit "Schnellstart" nicht wirklich runter, sondern legt sich schlafen und lässt seine Platte dabei als "in Benutzung" markiert. Linux weigert sich dann, sie zu beschreiben, oder du schießt dir im schlimmsten Fall die Dateien kaputt.
>
> In Windows: Systemsteuerung, Energieoptionen, "Auswählen, was beim Drücken von Netzschaltern geschehen soll", dann "Einige Einstellungen sind momentan nicht verfügbar" anklicken und den Haken bei "Schnellstart aktivieren" rausnehmen.
>
> Winterschlaf gleich mit aus, in einer Eingabeaufforderung als Administrator:
>
> ```
> powercfg /h off
> ```

</details>

<details>
<summary><strong>Windows-Platte unter Linux öffnen</strong></summary>

> ```bash
> sudo pacman -S ntfs-3g
> lsblk -f
> ```
>
> `lsblk -f` zeigt dir alle Partitionen mit Dateisystem. Die große mit `ntfs` ist deine Windows-Platte. Öffnen kannst du sie danach einfach in Dolphin über die Seitenleiste, um sie automatisch bei jedem Start einzuhängen, brauchst du einen Eintrag in der [fstab](https://wiki.archlinux.org/title/Fstab).

</details>

<details>
<summary><strong>Windows ins Bootmenü holen</strong></summary>

> Wenn du bei archinstall `grub` genommen hast:
>
> ```bash
> sudo pacman -S os-prober
> ```
>
> Dann in `/etc/default/grub` die Zeile `GRUB_DISABLE_OS_PROBER=false` eintragen oder das `#` davor entfernen. Die Sperre ist Absicht, ohne sie durchsucht GRUB fremde Platten. Danach:
>
> ```bash
> sudo grub-mkconfig -o /boot/grub/grub.cfg
> ```
>
> In der Ausgabe muss Windows auftauchen. Wenn nicht, ist die Windows-EFI-Partition gerade nicht eingehängt.
>
> Alternativ kannst du GRUB weglassen und im BIOS-Bootmenü (meist F8, F11 oder F12) jedes Mal auswählen, was starten soll. Ist unbequemer, geht aber nie kaputt.

</details>

<details>
<summary><strong>Die Uhr geht plötzlich falsch</strong></summary>

> Klassiker: Nach dem Wechsel zwischen Linux und Windows ist die Uhrzeit um ein paar Stunden verschoben. Grund ist, dass Linux die Hardwareuhr auf UTC stellt und Windows sie als Ortszeit liest.
>
> Reparieren solltest du das auf der Windows-Seite, nicht auf der Linux-Seite. In einer Eingabeaufforderung als Administrator:
>
> ```
> reg add "HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /t REG_DWORD /d 1 /f
> ```

</details>

#### Secure Boot

Arch startet mit eingeschaltetem Secure Boot erstmal nicht, weil der Bootloader keine Signatur hat, der dein Mainboard vertraut. Zwei Wege raus.

<details>
<summary><strong>Der einfache Weg: ausschalten</strong></summary>

> Ins BIOS (beim Hochfahren meist ENTF oder F2), unter "Boot" oder "Security" Secure Boot auf Disabled. Fertig.
>
> **Vorher wichtig, wenn du Windows behältst:** Prüf in Windows unter "Geräteverschlüsselung" oder "BitLocker", ob deine Platte verschlüsselt ist. Wenn ja, sichere den Wiederherstellungsschlüssel oder setz BitLocker vorher aus. BitLocker merkt sich den Secure-Boot-Zustand, und wenn der sich ändert, fragt Windows beim nächsten Start nach dem 48-stelligen Schlüssel. Ohne den kommst du nicht mehr an deine Daten.

</details>

<details>
<summary><strong>Die Kür: eigene Schlüssel mit sbctl</strong></summary>

> Damit bleibt Secure Boot an und dein Rechner vertraut deinem eigenen Arch. Braucht ein BIOS, in dem sich die vorhandenen Schlüssel löschen lassen ("Setup Mode", oft versteckt hinter "Clear Secure Boot Keys" oder "Reset to Custom Mode").
>
> ```bash
> sudo pacman -S sbctl
> sudo sbctl status
> ```
>
> Bei `Setup Mode: Enabled` kann es losgehen:
>
> ```bash
> sudo sbctl create-keys
> sudo sbctl enroll-keys -m
> ```
>
> Das `-m` ist bei Dualboot Pflicht. Es behält die Microsoft-Schlüssel, sonst startet Windows nicht mehr. Manche Mainboards und Grafikkarten brauchen sie auch für sich selbst, also lass es auch ohne Windows lieber drin.
>
> Dann signieren, was am Start beteiligt ist:
>
> ```bash
> sudo sbctl sign -s /boot/vmlinuz-linux
> sudo sbctl sign -s /boot/EFI/GRUB/grubx64.efi
> sudo sbctl verify
> ```
>
> `sbctl verify` listet auf, was noch unsigniert ist. Der Pfad zur EFI-Datei hängt von deinem Bootloader ab, deshalb erst `verify` laufen lassen und dann die genannten Dateien signieren. Um Kernel-Updates musst du dich danach nicht kümmern, sbctl hängt sich in pacman ein und signiert automatisch nach. Zum Schluss Secure Boot im BIOS wieder an.
>
> Volle Anleitung im [Wiki](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#sbctl).

</details>

***

### 7. KDE nach deinem Geschmack

Der Teil, für den sich der ganze Aufwand lohnt. KDE lässt sich bis zur Unkenntlichkeit umbauen, und zwar komplett per Klick in den Systemeinstellungen.

<details>
<summary><strong>Aussehen ändern</strong></summary>

> Systemeinstellungen, "Erscheinungsbild und Design". Bei "Designs" gibt es unten den Knopf "Neue Designs holen", der lädt direkt aus dem [KDE Store](https://store.kde.org/). Dasselbe gibt es getrennt für Symbole, Mauszeiger, Fensterdekorationen und Anmeldebildschirm.
>
> Wenn du ein komplettes Design nimmst, ändert es Farben, Symbole und Leiste auf einmal. Rückgängig machen geht immer, das Standarddesign heißt "Breeze".

</details>

<details>
<summary><strong>Leiste und Miniprogramme</strong></summary>

> Rechtsklick auf die Leiste, "Miniprogramme hinzufügen". Über "Neue Miniprogramme holen" kommst du wieder in den Store. Die Leiste selbst kannst du unter "Leiste einrichten" verschieben, verstecken oder in der Höhe ändern.
>
> Ein Miniprogramm, das sich für Arch wirklich lohnt, steht in [Kapitel 9](#9-updates-im-blick-behalten).

</details>

<details>
<summary><strong>Flatpak dazu</strong></summary>

> Manche Programme gibt es weder im Repo noch im AUR, dafür als Flatpak. Lohnt sich vor allem bei Sachen, die sonst ewig zu bauen wären.
>
> ```bash
> sudo pacman -S flatpak
> flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
> ```
>
> Installiert wird dann mit `flatpak install flathub name.des.programms`. Halt dich damit trotzdem zurück, Flatpaks sind größer und brauchen ihre eigenen Updates (`flatpak update`).

</details>

***

### 8. Gaming

Läuft besser, als die meisten denken. Der Großteil der Windows-Spiele startet einfach.

<details>
<summary><strong>Steam und Proton</strong></summary>

> Steam braucht `multilib`. Falls du es noch nicht aktiviert hast, in `/etc/pacman.conf` die beiden Zeilen bei `[multilib]` entkommentieren, dann `sudo pacman -Syu`.
>
> ```bash
> sudo pacman -S steam
> ```
>
> In Steam unter Einstellungen, "Compatibility", beide Haken für Steam Play setzen. Damit laufen auch Spiele, die offiziell kein Linux können. Ob dein Spiel dabei ist, steht auf [ProtonDB](https://www.protondb.com/).
>
> Wenn ein Spiel zickt, lohnt sich eine andere Proton-Version. Die holst du dir bequem mit `yay -S protonup-qt`.

</details>

<details>
<summary><strong>Alles außerhalb von Steam</strong></summary>

> ```bash
> sudo pacman -S lutris
> yay -S heroic-games-launcher-bin
> ```
>
> Lutris deckt GOG und einzelne Windows-Spiele ab, Heroic ist für Epic, GOG und Amazon.

</details>

<details>
<summary><strong>Nützliches Beiwerk</strong></summary>

> ```bash
> sudo pacman -S gamemode lib32-gamemode mangohud lib32-mangohud
> ```
>
> `gamemode` stellt den Rechner beim Spielen auf Leistung um, `mangohud` blendet FPS und Auslastung ein. In Steam trägst du das pro Spiel unter Startoptionen ein:
>
> ```
> gamemoderun mangohud %command%
> ```

</details>

> **Der eine Haken:** Spiele mit Kernel-AntiCheat laufen nicht, dazu gehören unter anderem Valorant, League of Legends und Fortnite. Das ist keine fehlende Einstellung, sondern eine Entscheidung der Hersteller, und daran wirst du nichts ändern. Wenn eins dieser Spiele für dich Pflicht ist, behalte Windows als Dualboot (siehe [Kapitel 6](#6-dualboot-mit-windows)). Ob deins betroffen ist, steht auf [areweanticheatyet.com](https://areweanticheatyet.com/).

***

### 9. Updates im Blick behalten

Arch ist ein [Rolling Release](https://wiki.archlinux.org/title/Arch_Linux#Rolling_release). Es gibt also keinen großen Versionssprung einmal im Jahr, bei dem sich alles auf einmal ändert, sondern laufend kleine Updates. Das klingt erstmal nach mehr Arbeit, ist in der Praxis aber ein Befehl und ein paar Minuten warten.

#### Der eine Befehl, den du brauchst

```bash
sudo pacman -Syu
```

`S` installiert, `y` holt die aktuelle Paketdatenbank, `u` bringt alle installierten Pakete auf den neuesten Stand. Mehr ist es nicht. Einmal die Woche reicht völlig, wenn du länger nicht am PC warst, machst du es halt dann.

<details>
<summary><strong>Wichtig: niemals nur "-Sy" benutzen</strong></summary>

> `sudo pacman -Sy paketname` sieht harmlos aus, ist aber der häufigste Weg, sich Arch kaputt zu machen. Du holst dir damit die neue Paketdatenbank, installierst aber nur ein einziges Paket daraus. Das neue Paket erwartet dann Bibliotheken in Versionen, die auf deinem System noch gar nicht liegen. Das nennt sich [partial upgrade](https://wiki.archlinux.org/title/System_maintenance#Partial_upgrades_are_unsupported) und wird von Arch nicht unterstützt.
>
> Merksatz: Das `y` kommt nie ohne das `u`. Wenn du ein einzelnes Paket willst, nimm `sudo pacman -S paketname` ohne `y`, oder mach direkt ein volles `-Syu`.

</details>

***

#### AUR dazu

Das [AUR](https://wiki.archlinux.org/title/Arch_User_Repository) ist die von Nutzern gepflegte Paketsammlung neben den offiziellen Repos, und ehrlich gesagt der Grund, warum sich Arch überhaupt lohnt. Da liegt nicht nur vieles drin, was es sonst nirgends gibt. Ein AUR-Paket ist auch kein fertiges Programm, sondern ein Bauplan (`PKGBUILD`), der auf deinem Rechner übersetzt wird. Du kannst also Software für dein Setup bauen statt zu nehmen, was jemand anderes für alle vorkompiliert hat.

AUR-Pakete werden nicht von `pacman` aktualisiert, dafür brauchst du einen Helper wie [yay](https://github.com/Jguer/yay).

```bash
yay -Qua   # zeigt nur, was im AUR ein Update hat
yay        # aktualisiert offizielle Repos und AUR in einem Rutsch
```

Wenn du `yay` benutzt, ersetzt der zweite Befehl dein `sudo pacman -Syu`. Beides doppelt machen musst du nicht.

> [paru](https://github.com/Morganamilo/paru) macht im Grunde dasselbe und ist genauso in Ordnung, und `pacman` allein reicht dir auch, solange du nichts aus dem AUR willst. In diesem Tutorial bleiben wir bei `yay`, damit die Befehle überall gleich aussehen.

***

#### Updates sehen, ohne dran zu denken

Wenn du nicht jedes Mal selbst nachschauen willst, gibt es ein Plasma-Miniprogramm, das die anstehenden Updates direkt in der Leiste anzeigt: [Arch Update Counter](https://github.com/bouteillerAlan/archupdate) von Bouteiller Alan. Kleines Icon mit Zähler, Klick öffnet die Liste der anstehenden Pakete mit den Versionssprüngen.

<details>
<summary><strong>Installation</strong></summary>

```bash
yay -S plasma6-applets-arch-update-notifier
```

> Als Abhängigkeit kommt `pacman-contrib` mit, das liefert den Befehl `checkupdates`. Zusätzlich empfohlen sind `yay` (für die AUR-Zählung) und `konsole` (das Terminal, in dem das Update dann läuft).
>
> Danach Rechtsklick auf die Leiste, "Miniprogramme hinzufügen", nach "Arch Update" suchen und reinziehen.

</details>

<details>
<summary><strong>Wie es zählt</strong></summary>

> Die Befehle stehen als Standard in der Konfiguration des Miniprogramms und lassen sich frei ändern:

| Zweck            | Befehl                 |
| ---------------- | ---------------------- |
| Offizielle Repos | `checkupdates \| wc -l` |
| AUR              | `yay -Qua \| wc -l`     |
| Update ausführen | `yay`                  |

> `checkupdates` ist dabei der saubere Weg. Es lädt die Paketdatenbank in einen temporären Ordner statt nach `/var/lib/pacman` und macht damit eben kein `-Sy` auf deinem System. Du kannst also gefahrlos zählen lassen, ohne dir aus Versehen ein partial upgrade einzufangen.

</details>

<details>
<summary><strong>Was das Miniprogramm nicht macht</strong></summary>

> Die Oberfläche ist nur die Anzeige. Das eigentliche Update startet über den eingestellten Befehl, und das ist standardmäßig `yay` in einem Konsole-Fenster. Du siehst also am Ende trotzdem ein Terminal, das nach deinem Passwort fragt. Finden wir auch richtig so, bei einem Update willst du sehen was passiert.

</details>

***

#### Die drei Sachen, über die Neulinge stolpern

<details>
<summary><strong>1. Arch-News vor größeren Updates lesen</strong></summary>

> Ein paar Mal im Jahr braucht ein Update einen Handgriff von dir, zum Beispiel wenn ein Paket umbenannt wird oder eine Konfiguration umzieht. Das steht dann vorher auf [archlinux.org/news](https://archlinux.org/news/). Wenn ein Update ungewöhnlich groß ist oder `pacman` sich über einen Konflikt beschwert, ist das die erste Adresse.

</details>

<details>
<summary><strong>2. .pacnew-Dateien</strong></summary>

> Wenn du eine Konfigurationsdatei angepasst hast und das Update eine neue Standardversion mitbringt, überschreibt `pacman` deine Datei nicht. Stattdessen legt es die neue daneben als `datei.pacnew` und sagt dir das am Ende der Ausgabe.
>
> Ignorieren geht eine ganze Weile gut und irgendwann nicht mehr. Aufräumen kannst du mit `pacdiff` (kommt auch aus `pacman-contrib`), das zeigt dir die Unterschiede und fragt, was bleiben soll. Mehr dazu im [Wiki](https://wiki.archlinux.org/title/Pacman/Pacnew_and_Pacsave).

</details>

<details>
<summary><strong>3. Nach einem Kernel-Update neu starten</strong></summary>

> Wurde der Kernel aktualisiert, laufen die alten Module nicht mehr zum neuen Kernel auf der Platte. Solange du nicht neu startest, kann es passieren, dass ein frisch eingesteckter USB-Stick nicht erkannt wird oder ein Programm mit einer komischen Fehlermeldung abbricht. Der Rechner stürzt davon nicht ab, es ist einfach ein Neustart fällig.

</details>

***

#### Und was ist mit Discover?

KDE bringt mit [Discover](https://apps.kde.org/discover/) einen grafischen Paketmanager mit, der Updates auch anzeigen und installieren kann. Ganz ohne Terminal, wenn du das willst.

Wir raten trotzdem davon ab:

- Discover ignoriert das AUR komplett. Ein Teil deiner Pakete bleibt also stehen, ohne dass du es merkst, und genau der Teil ist der Grund, warum du Arch installiert hast.
- Wenn beim Update etwas schiefgeht, bekommst du eine kurze Fehlermeldung statt der eigentlichen Ausgabe von `pacman`. Genau die brauchst du aber zum Googeln.
- Es lädt Flatpaks und Systempakete in denselben Topf, was am Anfang eher verwirrt.

Vor allem aber: Wer nur klickt und nur nimmt, was vorkompiliert bei ihm ankommt, kann auch gleich bei Windows bleiben. Da funktioniert genau das nämlich schon ziemlich gut. Arch wird erst interessant, wenn du dir mit `yay` Sachen holst und baust, die zu deinem Rechner passen.

Und `sudo pacman -Syu` ist ein Befehl, den du dir einmal merkst und danach nie wieder nachschlägst. Das ist ehrlich weniger Aufwand als es aussieht.