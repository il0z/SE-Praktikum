# Aufgabe Projekt SE 2018 SS

## Hintergrund und Umfeld

In einem räumlich weit ausgedehnten Abbaugebiet von mehreren hundert
Quadratkilometern werden Bodenschätze (z.B. Kohle, Erze) im Tagebau abgebaut.
Die dazu benötigten Maschinen sind Bagger (Eimerkettenbagger, Radbagger,
Schaufelbagger), Förderbänder, Bunker (zur Lagerung des geförderten Materials),
Absetzer (zum Verteilen des Abraums, der keine oder zu wenig Wertstoffe
enthält, Sand, Erde, Gestein). Die Maschinen sind in typischen
Produktionslinien angeordnet: an erster Stelle Bagger. Sie fördern den Aushub
bzw. das Abbaumaterial auf eine Reihe hintereinander und/oder parallel
angeordnete Förderbänder von beträchtlicher Lauflänge (in einzelnen Segmenten
von je einigen hundert Metern) bis ca. 10-20km Strecke. Über Weichen in den
Bandsystemen kann gesteuert werden, ob die aktuelle Förderung/ das Material in
einen Bunker oder als Abraum zu einem Absetzer transportiert wird.

## Das IT-System

### Geräterechner

Jeder Maschine ist wenigstens ein lokaler Geräterechner zugeordnet (komplexe
Maschinen, wie z.B. Bagger, enthalten mehrere Geräterechner, die einzelnen
Aggregaten zugeordnet sind). Seine Aufgabe ist die lokale Steuerung und
Regelung der Maschine im Sinn einer Ablaufsteuerung, Zustandsüberwachung, auch
der Regelung von Vorgängen. Die Steuerungsfunktionen laufen vollautomatisch,
halbautomatisch mit Eingriffen von Personal oder handgesteuert ab. Bei
Eingriffen von Bedienpersonal hat die SW im Steuerungssystem die Aufgabe,
Abläufe im Sinn der Bedienung zu steuern. Halbautomatik bedeutet, die Maschine
läuft lange Zeit ohne Eingriff, ruft aber in bestimmten Situationen die
Entscheidung eines Bedieners ab, um mit der Arbeit fortfahren zu können.
Handsteuerung liegt vor, wenn ein Steuergerät nur Bedienkommandos umsetzt. In
allen Fällen wird die SW prüfen, ob eine bestimmte Bedienung im jeweils
aktuellen Maschinenzustand möglich ist. Auf Notabschaltung reagiert die
Steuerung sofort.

Weitere Aufgabe der Geräterechner ist, ein Zustandsabbild des zugeordneten
Anlagenteils (der Maschine, …) zu verwalten und aktuell zu halten. Das
Zustandsabbild umfasst binäre Zustände (aus der Steuerung, von Schaltern z.B.)
oder Messwerte von Messwertfühlern (Sensoren). Die Elemente des Zustandsabbilds
können auf einer maschinennahen Ebene in vielfältigen Ausprägungen realisiert
sein: Variablen, Speicherstellen, Bits innerhalb von Speicherstellen. `Durch
die Zusammenschau der Zustandsabbilder aller beteiligten Geräterechner entsteht
ein Gesamtabbild der Anlage. Diese Gesamtschau wird in (den Geräterechnern
übergeordneten) Zentralen Leitstandsrechnern erzeugt und gespeichert`.

Damit diese zentrale Datenhaltung erfolgen kann, senden die Geräterechner
zyklisch oder spontan sog. `Telegramme an die Leitrechner. Messwerte werden
zyklisch übertragen.` Die Zykluszeiten hängen von den Messstellen ab. Die
Messwerte aus trägen Prozessen mit großen Zeitkonstanten werden mit geringeren
Abtastfrequenzen erfasst, als die aus flinken Prozessen. Binäre
Zustandsänderungen werden in Spontantelegrammen codiert und als sog.
`Ereignistelegramme versandt`. Der Aufbau der Telegramme folgt einer festen
Struktur und umfasst: die lokale Systemzeit, die Kennzeichnung des Anlagenteils
(Maschine) und der Einheit (u.a. Antriebe, Getriebe, Spannungsversorgung, …),
die Messstelle oder Signalquelle und den Messwert bzw. den Zustandswert. `Vor
dem Versenden eines Telegramms wird es im Geräterechner in einen Ausgabe- und
Sendepuffer geschrieben.` Dort verbleibt es so lange, bis der `empfangende
Leitrechner den Empfang bestätigt.` Nach einer Bestätigung wird es als bestätigt
markiert. Es wird nicht sofort gelöscht, sondern überschrieben, wenn der
Speicherplatz aufgrund der Pufferstrategie benötigt wird.

Die Speicherausstattung und die Stromversorgung sollen einen Spannungsausfall
von 6h überbrücken können. Kommt es nach einem längeren Totalausfall der
Stromversorgung zu einem vollständigen Datenverlust im Geräterechner, muss eine
Generalabfrage aller Messstellen und Signalquellen erfolgen und daraus das
lokale Prozessabbild rekonstruiert werden.

#### Aufgabe 1

> (Zu einem Geräterechner --Zoltan)

Versuchen Sie, in der Beschreibung funktionale und nichtfunktionale
**Anforderungen** zu erkennen und als Anforderungen zu formulieren. Entdecken
Sie Möglichkeiten zur **Gliederung**? Können Sie Anwendungs- („soll passieren“,
laut dem Kunden --Claudio) und Systemanforderungen („wird passieren“, laut uns
--Claudio) unterscheiden?

#### Aufgabe 2

Entwickeln sie das **Kontextdiagramm** nach SA/RT und eine Verfeinerungsstufe.

#### Aufgabe 3

Entwickeln Sie ein **Use-Case-Diagramm** und verfeinern Sie es um
unterstützende UCes ("uses") und Spezialfälle ("extends"). Greifen Sie einen UC
heraus und versuchen Sie eine Beschreibung in **Formularform**.

### Der Leitrechner

Die Geräterechner sind über ein Kommunikationsnetzwerk (hier nicht genauer
spezifiziert) mit dem Leitrechner verbunden. Der Leitrechner nimmt die zentrale
Rolle bei der Datensammlung aus dem Prozess ein. Alle versendeten
Datentelegramme werden an ihn gesandt. In den Geräterechnern werden die
Ereignis- bzw. Sendepuffer erst überschrieben, wenn die entsprechenden Empfänge
durch den Leitrechner bestätigt werden (Quittung, Acknowledge)

Seine Aufgabe besteht darin, die Daten aus den einzelnen Geräterechnern zu
sammeln und in eine zentrale Datenhaltung zu übernehmen. In diesem Datenpool
werden die Ereignisse in zeitlicher Reihenfolge quasi als Logbucheinträge
abgelegt. Dazu werden die Zeitstempel der Ereignisse als Ordnungskriterium
benutzt (aus den Systemzeiten der eingehenden Telegramme werden Datum/Uhrzeiten
gebildet). Außerdem werden die Ereignisse benutzt um im Leitrechner die
Prozessabbilder aller externen Geräte zu pflegen. D.h. die eingehenden
Ereignisse werden nach Maschinen gefiltert und weiter verarbeitet.

Der Leitrechner versorgt aus der zentralen Datenhaltung unterschiedliche
Displays mit aktueller Information:

- Alarmanzeige, schwerwiegende Ereignisse, die sofortiges Handel erfordern,
  z.B. Abschaltungen, sofern diese nicht schon automatisch eintreten;
- laufende Ereignisse, selektiert nach Maschinen oder Linien, oder
  Gesamtereignisstrom;
- Schichtprotokolle über die Produktion/Förderung insgesamt oder nach Linien
  selektiert;
- vorausschauende Analyse für prophylaktische Wartungseinsätze an Maschinen
  durch statistische Verfahren, die auf den Ereignissen basieren

#### Aufgaben 4 – 7

Erweitern Sie Ihre bisherigen Lösungen um die Anforderungen aus der erweiterten
Beschreibung:

4) machen Sie einen Vorschlag für die **Strukturen der Datenhaltung**
5) ergänzen sie die Use-Cases
6) entwickeln Sie für eine Auswahl der Use-Cases **Szenarios**. (Anzahl je nach
   Gruppengröße)
7) beschreiben Sie den Ereignis-/Quittungsverkehr mit einem **Zustandsdiagramm
   / Sequenzdiagramm** der beteiligten Kommunikationspartner (vgl.
   Zustandsdiagramm Digitaluhr). Stellen Sie diese dazu als Objekte dar, die
   gegenseitige Methodenaufrufe tätigen.
