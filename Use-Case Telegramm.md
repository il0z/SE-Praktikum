##Use Case Telegramme

- System: Geräterechner
- Use-Case: Telegramm
- Actors: Förderband, Leitrechner, Geräterechner
- Data: Der Geräterechner erstellt ein Telegramm aus den Daten die es vom Förderband gesammelt hat. Diese Telegramme werden in einem AusgabeSpeicher gespeichert und es wird versucht sie an den Leitrechner zu senden. Das Telegramm beinhaltet die lokale Systemzeit, die Kennzeichnung des Anlagenteils (Maschine) und der Einheit (u.a. Antriebe, Getriebe, Spannungsversorgung, … ), die Messstelle oder Signalquelle und den Messwert bzw. den Zustandswert.
- Stimulus: Damit diese zentrale Datenhaltung erfolgen kann, senden die Geräterechner zyklisch oder spontan sog. Telegramme an die Leitrechner. Messwerte werden zyklisch übertragen. Die Zykluszeiten hängen von den Messstellen ab.
- Response: Der Leitrechner übergibt eine Empfangsbestätigung bei erhalt der Daten. Nach einer Bestätigung wird das Telegramm als bestätigt markiert. Die Telegramme werden nur dann gelöscht wenn der Speicherplatz benötigt wird.