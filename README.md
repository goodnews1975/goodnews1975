*English version below.*

Hallo! Hier zeige ich an einem eigenen Projekt, wie ich KI praktisch einsetze: von der Planung über die Einrichtung bis zum täglichen Betrieb.

**Kurz gesagt:** Selbst betriebenes KI-gestütztes Wissenssystem (seit 2026)
- Getrennte Wissensarchive in Obsidian auf eigenem Heimserver, mit Git versioniert, nächtliche Sicherung, Zugriff von außen nur per VPN
- KI-Agent (Claude Code) pflegt die Archive nachts selbstständig, mit festen Regeln und eng begrenzten Rechten
- Anbindung von Kalender, E-Mail und einem Kanban-Board für Bewerbungen über das Model Context Protocol (MCP)
- Lokales Sprachmodell für vertrauliche Daten, ausgewählt per Vergleichstest auf der eigenen Hardware

**Ein eigenes KI-gestütztes Wissensarchiv, zu Hause betrieben**

Ich habe mir mit KI ein persönliches Wissens- und Organisationssystem gebaut, das auf einem kleinen Heimserver läuft. Ein KI-Agent pflegt es jede Nacht selbstständig, mit klaren Regeln und eng begrenzten Rechten.

**Was es ist**
- Getrennte Wissensarchive als einfache Textdateien in Obsidian: eines für Privates, eines für Berufliches und ein kleines für Aufgaben und den Tagesüberblick. Die Trennung ist technisch erzwungen, nicht nur verabredet.
- Die Daten liegen bei mir zu Hause, nicht bei einem fremden Notizdienst. Jede Änderung ist mit Git versioniert und lässt sich zurückholen. Gesichert wird jede Nacht an zwei Orten, die Online-Kopie verschlüsselt.
- Alle Geräte (PC, Laptop, Tablet, Handy) gleichen die Archive automatisch ab. Von außen ist nichts offen, unterwegs geht der Zugriff nur über ein VPN.

**Wie die KI eingebunden ist**
- **Nächtliche Pflege durch einen KI-Agenten (Claude Code):** Er ordnet neue Notizen ein und verlinkt sie, meldet erledigte Aufgaben zurück, prüft die Nachtsicherung, fasst Aufnahmen zusammen, stellt Lernübungen und korrigiert sie, und schreibt jeden Morgen die aktuelle Aufgabenliste.
- **Regeln statt Blindvertrauen:** Jede Aussage im Archiv braucht eine Quelle, Unsicheres wird als offene Frage markiert, meine eigenen Texte werden nie überschrieben. Der Agent darf nur in dem Archiv schreiben, das er pflegt. Alles andere ist gesperrt, auch Administratorrechte und das Internet. Das Festhalten der Änderungen macht ein Skript, nicht die KI.
- **Anbindung an Kalender und E-Mail:** Der Kalender läuft auf einem eigenen Server zu Hause, Handy und Uhr gleichen über einen offenen Standard ab. Kalender und Postfächer sind über kleine Zugänge auf dem Heimserver mit der KI verbunden, geschützt mit einem Schlüssel und nur im Heimnetz erreichbar. Privat und beruflich haben getrennte Zugänge. Die Mail-Zugänge können grundsätzlich keine Mails senden oder löschen. In der nächtlichen Pflege darf die KI im Postfach nur suchen und lesen, zum Beispiel um einen wöchentlichen Stand aus einer Rundmail ins Archiv zu übernehmen. Jeden Morgen entsteht außerdem automatisch eine Tagesnotiz mit den Terminen des Tages und Hinweisen aus den Mails.
- **Kanban-Board für Bewerbungen:** Im beruflichen Archiv steuert ein Kanban-Board in Obsidian die Bewerbungen. Die Spalten reichen von „Merkliste“ über „Beworben“ und „Im Gespräch“ bis „Abgeschlossen“. Jede Karte verweist auf eine Seite mit festen Feldern (Status, Priorität, Quelle, Arbeitsmodell, nächster Schritt) und einem Verlauf aller Kontakte. Die Priorität sieht man farbig. Eine Übersicht im Cockpit zeigt alle offenen Vorgänge mit dem nächsten Schritt.
  - **Ich** verschiebe die Karten und treffe die Entscheidungen. Das Board gibt den Status vor. Meine Notizen fasst die KI nie an.
  - **Die KI** gleicht in der nächtlichen Pflege die Felder mit dem Board ab. Sie findet Antworten im Postfach und trägt sie in den Verlauf ein, wichtige Rückmeldungen auch ins Cockpit. Termine aus dem Kalender übernimmt sie mit einer Aufgabe zur Vorbereitung. Neue Termine legt sie nur auf meinen Wunsch an.
  - Bleibt eine Antwort aus, entsteht automatisch eine Erinnerung zum Nachfassen. Abgeschlossene Vorgänge kommen nach einer Frist ins Archiv, die Lehren daraus auf eine eigene Seite.
- **Assistenten mit Dateizugriff:** Über das Model Context Protocol (MCP) bekommen KI-Assistenten im Browser Zugriff auf genau ein Archiv, nicht auf alle.
- **Lokales Sprachmodell für Sensibles:** Ein kleines, offenes Sprachmodell (Gemma 4 E2B) läuft komplett offline auf dem Server. Es hat ein eigenes Archiv für vertrauliche Notizen, das den Server nie verlässt.
  - **Auswahl per Vergleichstest:** Vier kleine Modelle bekamen auf dem Server dieselben Fragen zu echten Notizen, eine Fangfrage und ein Foto, bewertet nach Tempo, Richtigkeit und Deutsch. Das gewählte Modell beantwortet Nachfragen in wenigen Sekunden, die erste Frage zu einer ganzen Notizseite in gut 20 Sekunden, und liest auch Bilder. Das vorige Modell brauchte für dieselbe Frage über drei Minuten.
  - **Pflegt sein eigenes Archiv:** Nachts arbeitet es neue Notizen ein und ergänzt das Verzeichnis. Einmal pro Woche prüft es, ob eine Seite etwas behauptet, das nicht in der zugehörigen Notiz steht. Ein Programm prüft jede Ausgabe, bevor sie gespeichert wird, und das Modell darf nichts löschen oder überschreiben.
  - **Grenze:** Als Lexikon taugt es nicht. Eine einfache Wissensfrage hat keines der getesteten Modelle richtig beantwortet. Für Fragen zu den eigenen Notizen reicht es.

**Wie ich mit der KI gearbeitet habe**
- Ich habe die Ziele und die Architektur festgelegt und jede grundlegende Entscheidung selbst getroffen: was getrennt bleibt, was die KI darf, was lokal bleiben muss.
- Die KI hat Pläne geschrieben, Skripte und Konfigurationen erstellt, Fehler eingegrenzt und jeden Schritt geprüft. Beispiele: ein Dateisystem-Problem beim Umzug auf neue Hardware, ein Fehler im Abgleich mehrerer Archive, Netzabbrüche durch einen Energiesparmodus, der Vergleichstest der lokalen Sprachmodelle.
- Hardware, Netzwerk und alle Schritte mit Administratorrechten habe ich selbst gemacht.

**Was ich dabei gelernt habe**
- KI ist dann verlässlich, wenn Rechte, Regeln und Prüfungen klar sind, nicht wenn man ihr einfach vertraut.
- Eine saubere Trennung von Daten (privat, beruflich, sensibel) muss man von Anfang an einplanen.
- Ehrlich prüfen gehört dazu: Das erste lokale Modell war zu langsam. Erst ein Test auf der eigenen Hardware hat ein passendes gefunden, und die Messungen wichen deutlich von den Angaben im Netz ab. Einzelne Aufgaben brauchen noch den PC.

### English version (as of 2026-11-20)

Hi! This is a personal project that shows how I use AI in practice, from planning and setup to day-to-day operation.

**In short:** Self-hosted AI-supported knowledge system (since 2026)
- Separate knowledge bases in Obsidian on my own home server, versioned with Git, nightly backups, remote access only via VPN
- AI agent (Claude Code) maintains the knowledge bases every night on its own, under fixed rules and with tightly limited permissions
- Calendar, email and a Kanban board for job applications connected via the Model Context Protocol (MCP)
- Local language model for confidential data, chosen by benchmark on my own hardware

**A personal AI-supported knowledge base, self-hosted at home**

Using AI, I built a personal knowledge and organisation system that runs on a small home server. An AI agent maintains it on its own every night, under clear rules and with tightly limited permissions.

**What it is**
- Separate knowledge bases stored as plain text files in Obsidian: one for personal matters, one for work, and a small one for tasks and the daily overview. The separation is enforced technically, not just agreed upon.
- The data stays with me at home, not with a third-party note service. Every change is versioned with Git and can be restored. Backups run every night to two locations, with the online copy encrypted.
- All devices (PC, laptop, tablet, phone) sync the knowledge bases automatically. Nothing is exposed to the internet; remote access works only through a VPN.

**How the AI is integrated**
- **Nightly maintenance by an AI agent (Claude Code):** It files and links new notes, reports completed tasks back, checks the nightly backup, summarises recordings, sets and corrects learning exercises, and writes the current task list every morning.
- **Rules instead of blind trust:** Every statement in the knowledge base needs a source, uncertain points are marked as open questions, and my own texts are never overwritten. The agent may only write to the knowledge base it maintains. Everything else is blocked, including administrator rights and internet access. Changes are committed by a script, not by the AI.
- **Calendar and email integration:** The calendar runs on my own server at home; phone and watch sync via an open standard. Calendar and mailboxes are connected to the AI through small access services on the home server, protected by a key and reachable only from the home network. Personal and work use separate access services. The mail services cannot send or delete emails at all. During nightly maintenance the AI may only search and read the mailbox, for example to copy a weekly status from a circular email into the knowledge base. Every morning a daily note is also created automatically, with the day's appointments and pointers from the inbox.
- **Kanban board for job applications:** In the work knowledge base, a Kanban board in Obsidian drives the job applications. The columns run from "Watchlist" through "Applied" and "Interviewing" to "Closed". Each card links to a page with fixed fields (status, priority, source, work model, next step) and a log of every contact. Priorities are colour-coded. An overview on the dashboard lists all open applications with their next step.
  - **I** move the cards and make the decisions. The board defines the status. The AI never touches my own notes.
  - **The AI** aligns the fields with the board during nightly maintenance. It finds replies in the mailbox and adds them to the log, and important responses also to the dashboard. It picks up appointments from the calendar together with a preparation task. It only creates new appointments when I ask it to.
  - If no reply arrives, a follow-up reminder is created automatically. Closed applications are archived after a set period, and lessons learned go to a separate page.
- **Assistants with file access:** Through the Model Context Protocol (MCP), AI assistants in the browser get access to exactly one knowledge base, not all of them.
- **Local language model for sensitive data:** A small open language model (Gemma 4 E2B) runs completely offline on the server. It has its own knowledge base for confidential notes that never leaves the server.
  - **Chosen by benchmark:** Four small models got the same questions about real notes on the server, plus a trick question and a photo, rated for speed, accuracy and German. The chosen model answers follow-up questions in a few seconds, the first question about a full note page in just over 20 seconds, and it also reads images. The previous model needed more than three minutes for the same question.
  - **Maintains its own knowledge base:** Every night it processes new notes and updates the index. Once a week it checks whether a page claims anything that is not in the underlying note. A program checks every output before it is saved, and the model may not delete or overwrite anything.
  - **Limit:** It is no encyclopedia. None of the tested models answered a simple general-knowledge question correctly. For questions about my own notes it is good enough.

**How I worked with the AI**
- I defined the goals and the architecture and made every fundamental decision myself: what stays separate, what the AI is allowed to do, what must stay local.
- The AI wrote plans, created scripts and configurations, narrowed down errors and verified every step. Examples: a file system issue when moving to new hardware, a bug in syncing several knowledge bases, network dropouts caused by a power-saving mode, and the benchmark of local language models.
- I handled the hardware, the network and every step that needed administrator rights myself.

**What I learned**
- AI becomes reliable when permissions, rules and checks are clear, not when you simply trust it.
- A clean separation of data (personal, work, sensitive) has to be planned from the start.
- Honest testing is part of it: the first local model was too slow. Only a test on my own hardware found a suitable one, and the measurements differed clearly from the figures published online. Some tasks still need the PC.
