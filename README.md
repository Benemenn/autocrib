# Dëse Projet beschreift d'Erneierung vun der Krëppschen an der Kierch St Martin

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

            

## Logik

### Statusmaschine

![Krippe_Statusmaschine](./out/diagrams/stateMachine/stateMachine.png)

- Zeitsynchronisierung mit NTPCLient (noch herauszusuchen) und schreiben der Lokalzeit mit ``W_LOC_T`` [doku](https://support.industry.siemens.com/cs/mdm/109747174?c=81662456587&dl=ru&lc=en-US)
- Minimale Beleuchtung solange keine Bewegungen erkannt wurden. 
- Nach Bewegungserkennung, mehr Beleuchtung. 
- Nach Münz- oder Papiergeldeinwurf, Spielen des Glockenspiels und Lichteranimation
- Wenn keine Bewegung erkannt wurde für ``tNoMovementDelay`` (~5 Min), zurück in den minimalen Beleuchtungsmodus. 
- Error Zustand:
    - noch nicht definiert

### Task Diagramm

dtTime = RD_LOC_T(); (alle 30min?)

### Klassendiagramm

![Klassendiagramm_Krippe_StMartin](./out/diagrams/classDiag/classDiag.png "Klassendiagramm_Krippe_StMartin")