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

### 4. Updates im Blick behalten

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