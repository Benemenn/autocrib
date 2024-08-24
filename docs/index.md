# Dëse Projet beschreift d'Erneierung vun der Krëppchen an der Kierch St Martin

***

# Inhaltsverzeichnis


1. [Beschreibung](#beschreibung)
    1. [Komponenten](#komponenten)
        1. [Datenblätter](#datenblätter)
1. [Logik](#logik)
    1. [Statusmaschine](#statusmaschine)
    1. [Task Diagramm](#task-diagramm)
    1. [Klassendiagramm](#klassendiagramm)
1. [CAD](#cad)
    1. [Münzerkennung](#münzerkennung)

***

# Beschreibung

## Einführung

In der Kirch St Martin in Düdelingen ist es in unserer Familie mittlerweile zu einer Tradition geworden, um Weihanchten in die Kirche zu gehen und uns die Krippe anzusehen. Vor vielen Jahren wurde dieses Krippenmodell elektrifiziert und mit verschiedenen Licht und Toneffekten ausgestattet. 

Für eine kleine geldliche Spende von 1€ können die Lichteffekte in einem bestimmten Zyklus abgespielt werden. Ein zweiter Münzeinwurf lässt den Besucher ein weiteres kleinereres Krippenmodell bewundern. Dieses Krippenmodell wird durch die sich öffnenden Tore zusammen mit einem mechanischen Glockenspiel sichtbar. 

Die Elektronische Steuerung der gesamten Krippe wurde mit einem Zeitmodul von einer Waschmaschine realisiert. 

Das Krippenmodell und vor allem die Elektronik des Krippenmodelles ist in die Jahre gekommen. Die Gruppe, welche sich um die Krippe kümmert hat sich daher entschieden das gesamte Krippenmodell zu sanieren, und die Elektronik in eine moderne Steuerung zu erneuern. 

<img src="https://github.com/Benemenn/autocrib/blob/gh-pages/images/Krippe.jpeg?raw=true" class="center">

## Sanierungsplan:

- Januar 2024: Zusammensetzen der Gruppe um das Projekt zu besprechen.
- Februar 2024: Konzeptionierung des Ersten Sanierungsschrittes.
- März 24 bis Juli 24: Implementierung der neuen Elektronik.
- Juli 24 bis September 24: Sommerpause & Implementierung der neuen Software.
- September 24 bis November 24: Implementierung und Testen der Software auf der Hardware, Fertigstellung der Hardware.
- Dezember 24: Abschluss des ersten Sanierungsschrittes.
- 2025: Sanierung der kleinen Krippe mit dem Glockenspiel.

## Sanierung

Für die Sanierung und Erneuerung wurde sich für moderne Komponenten entschieden. Hier eine kleine Übersicht:

## Komponenten

### Krippe

Die Krippe an sich wird seit vielen Jahren in der Kirche St Martin aufgebaut. Der Stammplatz für das Display ist die linke Seitenkapelle (aus Sicht auf den Hochaltar). 

<img src="https://dynamic-media-cdn.tripadvisor.com/media/photo-o/19/7a/09/7e/photo2jpg.jpg?w=1100&h=-1&s=1"> (image from Tripadvisor.com)

### Kleine Krippe

Neben dem großen Krippenaufbau steht darin noch ein kleinerer Krippenaufbau. Diese Krippe ist in einem Stallmodell versteckt und mit zwei Türen verschlossen. Durch einen geldlichen Einwurf, öffnen sich diese beiden Türen in Begleitung von einem glockenspiel. 

### Beleuchtung

Beleuchtet wird die Krippe mit mehreren Scheinwerfern und Effektlichern. 

- Beleuchtung:
    - 3x 6 Bretter mit Par18 für die Wandmontage
    - 2x 1 Par 15 zur Montage auf der Platte (Unter Baumstamm)
    - 1x Laterne
    - 1x Theater-feuer
    - Lichterketten im Hintergrund

### Elektronik

Bei den Sanierungsgesprächen wurde sich dafür entschieden die Steuerung durch eine moderne Automatieriungssteuerung zu ersetzen. Als Kopfstation wurde sich dabei für eine Siemens S7-1215C AC/DC/RLY entschieden. Die SPS ermöglicht es dem Team die Krippe über eine lange Zeit sicher und zuverlässig zu betreiben.

Die Möglichkeit mit einem Münzeinwurf funktionen zu aktivieren wird beibehalten. Die Erkennung der geldlichen Mittel bilden verschiedene Sensoren. 

Ein an dem Modell verbauten Bewegungssensor ermöglicht das Abschalten der Elektronik, sofern diese nicht benötigt wird, was eine erhebliche Stromersparnis darstellt. 

***

### Datenblätter

- [Siemens S7-1215C AC DC RLY](./Datasheets/Siemens_S71215_AC-DC-RLY.pdf)
- [SICK WL27-3P2430](./Datasheets/Sick_Lichtschranke_WL27-3P2430_1027769_de.pdf)
- [M12-4 Buchse&Kabel](./Datasheets/SICK_M12-5_Buchse_dataSheet_YF2A14-050VB3XLEAX_2096235_de.pdf)

***           

## Logik

Die Programmierung der Steuerung wird in der Siemens eigenen Entwicklungsumgebung TIA-Portal realisiert. Um die verschiedenen Effekte zeitlich abspielen zu können wurde sich für das Konzept einer Statusmaschine entschieden. 

### Statusmaschine

<img src="https://github.com/Benemenn/autocrib/blob/main/diagrams/Lights_StateMachine.png?raw=true" >

- Zeitsynchronisierung mit ``RD_LOC_T`` um einen Abschaltungsbetrieb bei Nacht zu ermöglichen. [doku](https://support.industry.siemens.com/cs/mdm/109747174?c=81662456587&dl=ru&lc=en-US)
- keine Beleuchtung solange keine Bewegungen erkannt wurden. 
- Nach Bewegungserkennung, minimale Beleuchtung. 
- Nach Münz- oder Papiergeldeinwurf, Spielen des Glockenspiels und Lichteranimation
- Wenn keine Bewegung erkannt wurde für eine gewisse Zeit (~5 Min), zurück in den minimalen Beleuchtungsmodus. 
- Error Zustand:
    - noch nicht definiert


***

## CAD

3D Druck mit dem FDM Verfahren bietet bei diesen Sanierungsarbeiten eine einfache und schnelle Prototyping phase ohne hohe Kosten zu verursachen. Bei dem Projekt wurden mehrere Teile für dieses Verfahren designed und verwendet. 

### Münzerkennung

Die Halterung behaust den SICK WL27-3P2430 Reflextionslichttaster. Ein Reflektor (in schwarz dargestellt) dient zur Reflextion des Laser-Sensors. Münzen werden von Oben in den Spalt hineinfallen gelassen. Der Schacht ist breit genug, dass alle Münzarten dadruchlaufen können. Der Scan-Schacht ist klein genug, dass auch die kleinen Münzen nicht in den ScanSchacht hineinfallen können und Blockierungen verursachen. 

<img src="https://github.com/Benemenn/autocrib/blob/gh-pages/CAD/CoinSensorTray/CoinSensorTray.png?raw=true">