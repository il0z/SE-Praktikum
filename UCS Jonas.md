- Beschreibung: 
	- Die automatische Steuerung regelt den Ablauf des Förderbands im automatischen Modus bis der User den Steuerungsmodus ändert.

- Akteure: 
	- Mitarbeiter

- Verwendete Anwendung:
	- Steuerung des Förderbandes
	- versenden von Telegramen
	- generierung der Zustandsdaten 
	- Telegramme im Puffer speichern
	- auf Empfangsbestätigung warten
	- Puffer frei geben

- Auslöser:
	- Wahl der automatischen Steuerung

- Vorbedingungen:
	- Keine

- Invarianten:
	- Notabschaltung
	- Dispaly
	- Statusmeldungen

- Nachbedingung/Ergebnis (postconditions)
	- Keine 

- Standardablauf
	- Empfangen und verarbeiten der Telegramme des Leitrechners
	- Empfangen und verarbeiten der Sensordaten
	- Geschwindigkeit an die Steuerung senden 
	- **wiederholen**
