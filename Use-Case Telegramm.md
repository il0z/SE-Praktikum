##Use Case Telegramme

- System: Geräterechner
- Use-Case: Telegramm
- Actors: Förderband, Leitrechner, Geräterechner
- Data: Der Geräterechner erstellt ein Telegramm aus den Daten die er vom Förderband gesammelt hat. Diese Telegramme werden in einem AusgabeSpeicher gespeichert und es wird versucht sie an den Leitrechner zu senden. Das Telegramm beinhaltet die lokale Systemzeit, die Kennzeichnung des Anlagenteils (Maschine) und der Einheit (u.a. Antriebe, Getriebe, Spannungsversorgung, … ), die Messstelle oder Signalquelle und den Messwert bzw. den Zustandswert.
- Stimulus: Die Geräterechner senden die Telegramme zyklisch an den Leitrechner. Die Zykluszeiten hängen von den Messstellen ab.
- Response: Der Leitrechner antwortet mit einer Empfangsbestätigung, mit der das Telegram als bestätigt markiert wird. 
