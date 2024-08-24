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
    1. [Münzerkennung](#münzerkennung)]

***

## Beschreibung

### Komponenten

- Gerüst Krippe, Figuren, Rindenmulsch, ...
- Kleine Krippe mit Glockenspiel
- Beleuchtung:
    - 3x 6 Bretter mit Par18 für die Wandmontage
    - 2x 1 Par 15 zur Montage auf der Platte (Unter Baumstamm)
    - 1x Laterne
    - 1x Theater-feuer
    - Lichterketten im Hintergrund

- Elektronik
    - Münzfach:
        - Reflexlichttaster in Münzkanal 
        - Gabellichtschranke für Papiergeld
    - Kleine Krippe:
        - Glockenspiel
    - Schaltschrank:
        - SPS:
            - Siemens S7-1215C AC/DC/RLY


#### Datenblätter

- [Siemens S7-1215C AC DC RLY](./Datasheets/Siemens_S71215_AC-DC-RLY.pdf)
- [SICK WL27-3P2430](./Datasheets/Sick_Lichtschranke_WL27-3P2430_1027769_de.pdf)
- [M12-4 Buchse&Kabel](./Datasheets/SICK_M12-5_Buchse_dataSheet_YF2A14-050VB3XLEAX_2096235_de.pdf)

***           

## Logik

### Statusmaschine

![Krippe_Statusmaschine](../diagrams/Lights_StateMachine.png?raw=true)

- Zeitsynchronisierung mit ``RD_LOC_T`` und schreiben der Lokalzeit mit ``W_LOC_T`` [doku](https://support.industry.siemens.com/cs/mdm/109747174?c=81662456587&dl=ru&lc=en-US)
- Minimale Beleuchtung solange keine Bewegungen erkannt wurden. 
- Nach Bewegungserkennung, mehr Beleuchtung. 
- Nach Münz- oder Papiergeldeinwurf, Spielen des Glockenspiels und Lichteranimation
- Wenn keine Bewegung erkannt wurde für ``tNoMovementDelay`` (~5 Min), zurück in den minimalen Beleuchtungsmodus. 
- Error Zustand:
    - noch nicht definiert

### Task Diagramm

dtTime = RD_LOC_T(); (alle 30min?)

Zeitlesung auf eigenen Task legen? mit einer Zykluszeit von 30min?
- Sinnvoll?
- does it even work?
- write time in global variable list in datatype DATE AND TIME

***

## CAD

### Münzerkennung

Die Halterung behaust den SICK WL27-3P2430 Reflextionslichttaster. Ein Reflektor (in schwarz dargestellt) dient zur Reflextion des Laser-Sensors. Münzen werden von Oben in den Spalt hineinfallen gelassen. Der Schacht ist breit genug, dass alle Münzarten dadruchlaufen können. Der Scan-Schacht ist klein genug, dass auch die kleinen Münzen nicht in den ScanSchacht hineinfallen können und Blockierungen verursachen. 

[Image here](https://github.com/Benemenn/autocrib/blob/gh-pages/CAD/CoinSensorTray/CoinSensorTray.png?raw=true)