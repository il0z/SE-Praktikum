<h1>
	AB - Informatik - 2. Semester <br/>
	Software Engineering - Prof. Dr. Eck
</h1>

(Vollständige Sätze bilden. Punkte nummerieren. Anweisung von Eck.)

## Aufgabe 1 - Anforderungen

1. Funktional

   1. Im Betriebsmodus "Vollautomatik" steuert der Geräterechner das Förderband
    selbstständig.

   2. Im Halbautomatischen Modus läuft die Maschine lange Zeit ohne Eingriff,
      ruft aber in bestimmten Situationen die Entscheidung eines Bedieners ab,
      um mit der Arbeit fortfahren zu können.

   3. Im Handgesteuerten Modus reagiert der Geräterechner nur auf
      Bedienkommandos.

   4. Der Geräterechner prüft vor jeder Umschaltung in einen anderen
      Betriebsmodi ob die Bedienung im jeweils aktuellen Maschinenzustand
      möglich ist.

   5. Der Geräterechner soll auf die Notabschaltung reagieren und sofort zum
      Stillstand kommen.

   6. Sollte es zu einem Stromausfall kommen, gewährleistet eine Batterie /
      Notstromaggregat die Stromversorgung für die nächsten 6 Stunden, um einen
      Datenverlust zu verhindern.

   7. Der Geräterechner übernimmt die Ablaufsteuerung, Zustandsüberwachung und
      die Regelung von Vorgängen des Förderbandes.

   8. Der Geräterechner das Zustandsabbild des Förderbandes verwalten und
      aktuell halten.

2. Nicht funktional

   1. Der Geräterechner versendet das Zustandsabbild per Telegramm an den
      Leitrechner und wartet auf die Empfangsbestätigung vom Leitrechner.

   2. (Die Messwerte aus trägen Prozessen mit großen Zeitkonstanten werden mit
      geringeren Abtastfrequenzen erfasst, als die aus flinken Prozessen.)

   3. (Binäre Zustandsänderungen werden in Spontantelegrammen codiert und als
      sog. Ereignistelegramme versandt.)

   4. (--nicht Teil der Aufgabe)

      1. Gewährleistung niedriger Latenzen bei der Kommunikation zwischen den
         Systemen an den verschiedenen Schlüsselstellen im Betrieb

      2. Meldung von Fehlerereignissen an alle weiteren Systeme, um Konflikte
         innerhalb der Kommunikation und der damit verbundenen Steuerung des
         Betriebs zu vermeiden (Wir wollen nicht, dass z.B. ein Bagger weiter
         Material auf das Band wirft, während es aufgrund eines Defekts nicht
         mehr in Betrieb ist)
