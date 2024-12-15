# Dëse Projet beschreift d'Erneierung vun der Krëppchen an der Kierch St Martin

***

# Inhaltsverzeichnis


1. [Beschreibung](#beschreibung)
    1. [Einführung](#einführung)
    1. [Sanierungsplan](#sanierungsplan)
    1. [Komponenten](#komponenten)
        1. [Krippe](#krippe)
        1. [Kleine Krippe](#kleine-krippe)
        1. [Beleuchtung](#beleuchtung)
        1. [Elektronik](#elektronik)
        1. [Datenblätter](#datenblätter)
1. [Logik](#logik)
    1. [Main](#main)
    1. [Statusmaschine](#statusmaschine)
    1. [Task Diagramm](#task-diagramm)
    1. [Klassendiagramm](#klassendiagramm)
1. [CAD](#cad)
    1. [Münzerkennung](#münzerkennung)

***

# Beschreibung

## Einführung

In der Kirche St Martin in Düdelingen ist es in unserer Familie mittlerweile zu einer Tradition geworden, um Weihanchten in die Kirche zu gehen und uns die Krippe anzusehen. Vor vielen Jahren wurde dieses Krippenmodell elektrifiziert und mit verschiedenen Licht und Toneffekten ausgestattet. 

Für eine kleine geldliche Spende können die Lichteffekte in einem bestimmten Zyklus abgespielt werden. Ein zweiter Münzeinwurf lässt den Besucher ein weiteres kleinereres Krippenmodell bewundern. Dieses Krippenmodell wird durch die sich öffnenden Tore zusammen mit einem mechanischen Glockenspiel sichtbar. 

Die Elektronische Steuerung der gesamten Krippe wurde mit einem Zeitmodul von einer Waschmaschine realisiert. 

Die Elektrik-Komponenten der Krippe wurden zuletzt vor rund 25Jahren erneuert. Die Krippengruppe hat sich daher enschieden die Elektronik zu erneuern. 

<img src="https://github.com/Benemenn/autocrib/blob/gh-pages/images/Krippe.jpeg?raw=true">

## Sanierungsplan:

- Januar 2024: Zusammensetzen der Gruppe um das Projekt zu besprechen.
- Februar 2024: Konzeptionierung des Ersten Sanierungsschrittes.
- März 24 bis November 24: Implementierung der neuen Elektronik. (Schritt 1)
- Dezember 24: Abschluss des ersten Sanierungsschrittes.
- 2025: todo
    - Sanierung der kleinen Krippe mit dem Glockenspiel.
    - Sanierung der Eletronik des Münzeinwurfes


### Krippe

Die Krippe an sich wird seit vielen Jahren in der Kirche St Martin aufgebaut. Der Stammplatz für das Display ist die linke Seitenkapelle (aus Sicht auf den Hochaltar). 

<img src="https://dynamic-media-cdn.tripadvisor.com/media/photo-o/19/7a/09/7e/photo2jpg.jpg?w=1100&h=-1&s=1"> (image from Tripadvisor.com)

### Kleine Krippe

Neben dem großen Krippenaufbau steht darin noch ein kleinerer Krippenaufbau. Diese Krippe ist in einem Stallmodell versteckt und mit zwei Türen verschlossen. Durch einen geldlichen Einwurf, öffnen sich diese beiden Türen in Begleitung von einem glockenspiel. 
Hierbei handelt es sich um eine autak funktionierende Krippenautomatik. (Im ersten Schritt wird diese nicht erneuert.)

### Beleuchtung

Beleuchtet wird die Krippe mit mehreren Scheinwerfern und Effektlichern. 

- Beleuchtung:
    - 3x Bretter mit jeweils 6 Scheinwerfen (Wandmontage)
    - 2x Bretter für direktere Beleuchtung (Montage in Krippendisplay)
    - 1x Laterne
    - 1x Feuer
    - Lichterketten im Hintergrund

### Elektronik

Bei den Sanierungsgesprächen wurde sich dafür entschieden die Steuerung durch eine moderne Automatieriungssteuerung zu ersetzen. Als Kopfstation wurde sich dabei für eine Siemens S7-1215C AC/DC/RLY entschieden. Die SPS ermöglicht es dem Team die Krippe über eine lange Zeit sicher und zuverlässig zu betreiben.

Die Möglichkeit mit einem Münzeinwurf funktionen zu aktivieren wird beibehalten. Die Erkennung der geldlichen Mittel bilden verschiedene Sensoren. 

Ein an dem Modell verbauten Bewegungssensor ermöglicht das Abschalten der Elektronik, sofern diese nicht benötigt wird, was eine erhebliche Stromersparnis darstellt. 


***           

## Logik

Die Programmierung der Steuerung wird in der Siemens eigenen Entwicklungsumgebung TIA-Portal realisiert. Um die verschiedenen Effekte zeitlich abspielen zu können wurde sich für das Konzept einer Statusmaschine entschieden. 

### Ein- und Ausgänge der Steuerung

Die Steuerung verfügt über 10 DC Eingänge und 10 potentialfreie Relais-Ausgänge. Die Ausgänge werden mit 24V versorgt, welche ebenfalls Relais auf 230V schalten. Jeder Ausgang kann dadurch 24VDC und 230VAC schalten. 

#### Eingänge

- I0.0 -> 
- I0.1 -> 
- I0.2 -> TasterTestmodusß
- I0.3 -> Bewegungsmelder
- I0.4 -> Münzsensor Beleuchtung
- I0.5 ->
- I0.6 ->
- I0.7 -> 

#### Ausgänge

- Q0.0 -> Minimalbeleuchtungsgruppe (keine Bewegung erkannt) -> Blau & Rot, dunkler Nachthimmel + Lichterketten Bäume
- Q0.1 -> MinimalPlusBeleuchtungGruppe (Bei erkannter Bewegung) -> Gelbe Grundhelligkeit
- Q0.2 -> LeuchtGruppe 1 -> Kaltweiss, Engel
- Q0.3 -> LeuchtGruppe 2 -> Rot, Hirten
- Q0.4 -> LeuchtGruppe 3 -> Grün, Josef/Maria => Hoffnung
- Q0.5 -> LeuchtGruppe 4 -> Fokus Jesus, WarmWeiss
- Q0.6 -> n.b.
- Q0.7 -> n.b.

- Q1.0 -> n.b.
- Q1.1 -> LeuchtGruppe Feuer/Laterne/Krippenautomat


### Ablauf

Lichtzyklus -> 80 sec

- Wenn eine gegebene Uhrzeit am Morgen erreicht ist, dann wird das Display aktiv. -> minimalbeleuchtung Q0.0
- Wird Bewegung an der Krippe erkannt, so wird Q0.1 & Q1.1 aktiv.
- Wird dann eine Münze in den Lichtschlichtz geworfen, so startet ein Lichtzyklus.
- Verschidene Lichtgruppen werden zunächst einzeln angezeigt. (Idee: Engel, Hirten, Familie, Kind)
- Anschließend werden die Lichtgruppen nacheinander zusammen eingeschaltet. Sind alle Lichtgruppen aktiv, bleibt dieser zustand etwas bestehen. 
- Zum Schluss werden die Lichtgruppen schnell nacheinander ausgeschaltet. Beleuchtung vom Kind als letztes.
- Wenn für eine gegebene Zeit keine Bewegung registriert wurde (100sek), so wechselt die Anlage wieder in den Minimal Modus, Feuer, Laterne und Krippenautomat werden deaktiviert. 

<img src="https://github.com/Benemenn/autocrib/blob/main/diagrams/Ablaufdiag_Logik.png?raw=true">

***

### Steuerungsprogrammierung

Das Hauptprogramm ist in LadderDiagram geschrieben. 

#### Network 1 - Zeit aus CPU lesen für Nachtbetrieb

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Code_Main_Netw1.png?raw=true">

Der Funktionsbaustein ``RD_LOC_T`` liest die CPU Zeit aus. Dasierend auf diesem Resultat wird nach einer Zeitenumwandlung die Krippe in den Nachtbetrib versetzt oder aus diesem aufgeweckt. 

#### Network 2 - Triggers updaten

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Code_Main_Netw2_Triggers.png?raw=true">

Da die Anlage über mehrere mechanische Taster verfügt, wird für die Erkennung eines Signals eine Flankensteuerung verwendet. Dies wird mit den Funktionsbausteinen ``R_TRIG`` realisiert. 

#### Network 3 - Main State Machine

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Code_Main_Netw3_FBSM.png?raw=true">

Im Network 3 wird die Statusmaschine aufgerufen. Siehe [Statusmaschine](#statusmaschine)

### Statusmaschine

<img src="https://github.com/Benemenn/autocrib/blob/main/diagrams/Lights_StateMachine.png?raw=true" >

- Zeitsynchronisierung mit ``RD_LOC_T`` um einen Abschaltungsbetrieb bei Nacht zu ermöglichen. [doku](https://support.industry.siemens.com/cs/mdm/109747174?c=81662456587&dl=ru&lc=en-US)
- keine Beleuchtung solange keine Bewegungen erkannt wurden. 
- Nach Bewegungserkennung, minimale Beleuchtung. 
- Nach Münz- oder Papiergeldeinwurf, Spielen des Glockenspiels und Lichteranimation
- Wenn keine Bewegung erkannt wurde für eine gewisse Zeit, zurück in den minimalen Beleuchtungsmodus. 
- Error Zustand:
    - noch nicht definiert

#### FB_MainStateMachine

Die Statusmaschine ist ein in SCL programmierter Funktionsbaustein. Das Haupt Statement ist dabei eine ``CASE OF``Anweisung. In dieser Anweisung werden die oben beschriebenen Status durchgewechselt. 

Repositories: 

- [PLC TiaPortal hier](https://github.com/Benemenn/autocrib_tia)
- [Raspberry für Sound & Co (Repo passwortgeschützt)](https://github.com/Benemenn/autocrib_dashboard)
- [Digitale Feuerstelle](https://github.com/Benemenn/autocrib_digifire)

***

## Hardware

### Seitenpanele

Die Seitenpanele auf der Linken und rechten Seite der Krippe bestehen aus 6 Scheinwerfern, welche durch das Ausrichten verschiedene Bereiche der Krippe fokussieren können. 

Um den Aufbau zu vereinfachen werden diese Seitenpanele mit Harting Steckern verpolungssicher am Verteilerkasten angeschlossen. In den Seitenpanelen sind unter anderem der Bewegungsmelder, eine 230V PowerCon Steckdose und eine 24V Steckdose verbaut worden. 

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Seitenpanele.jpeg?raw=true">

### Feuerstelle

Die alte Feuerstelle der Krippe war eine RLC-Schwinkreis um 2 E10 Birnen zum Flackern zu bringen. Die modernisierte Lösung beinhaltet einen Arduino Nano und eine Ringplatte mit NeoPixeln. 

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Kreppchen_Feier.jpeg?raw=true">

### Laterne

Ein neues Feature der Krippe stelle eine Laterne mit einem simulierten Feuer da. Wie bei der Feuerstelle wurde bei der Laterne auch ein Arduino Nano und Stäbe mit Neopixel verwendet. 

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Kreppchen_Lanter.jpeg?raw=true">

## CAD & eCAD

3D Druck mit dem FDM Verfahren bietet bei diesen Sanierungsarbeiten eine einfache und schnelle Prototyping phase ohne hohe Kosten zu verursachen. Bei dem Projekt wurden mehrere Teile für dieses Verfahren designed und verwendet. 

### Feuerschale

<img src="https://github.com/Benemenn/autocrib/blob/main/images/Feuerschale_techDraw.png?raw=true" >