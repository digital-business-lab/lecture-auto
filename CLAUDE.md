# CLAUDE.md – Projektgedächtnis: Autonome Logistiksysteme und IoT

> Diese Datei dient als persistentes Gedächtnis für die Zusammenarbeit zwischen Claude und dem Dozenten.
> Sie wird nach jeder relevanten Entscheidung oder Änderung aktualisiert.
> Letztes Update: 2026-03-23

---

## 1. Projektübersicht

| Feld | Inhalt |
|---|---|
| **Vorlesung** | Autonome Logistiksysteme und IoT |
| **Niveau** | Master |
| **Thema** | Einsatz von Fahrerlosen Transportsystemen (FTS) in der Intralogistik |
| **Repository** | https://github.com/digital-business-lab/lecture-auto |
| **Zweck des Repos** | Begleitmaterial zur Vorlesung (Aufgaben, Tutorials, Simulationen, Dokumente) |

---

## 2. Ziele des Projekts

Dieses Repository soll die Vorlesung mit strukturiertem, versioniertem Material begleiten und semester-übergreifend weiterentwickelt werden. Konkret geht es um:

1. **Verfeinerung des Vorlesungskonzepts** auf Basis der Erfahrungen aus dem letzten Semester
2. **Erstellung von Begleitmaterial** (Aufgabenblätter, Tutorials, Skripte, Simulationsdateien)
3. **Dokumentation von Entscheidungen** zu Didaktik, Werkzeugen und Inhalten

---

## 3. Vorlesungsstruktur (Stand: letztes Semester)

Die Vorlesung gliedert sich in folgende Blöcke:

### Block 1 – Organisatorisches & Grundlagen (Termin 1–2)
- Gliederung der Vorlesung, Themenvergabe
- Geschichte und moderne Anwendungsgebiete von FTS
- FTS-Technik: Spurführung, Sicherheit, Leitsteuerung, Transportfahrzeug, Umfeld, Zukunft
- **Didaktik:** Dozentenvortrag + Studierendenrecherche (branchenbezogene Aspekte)
- **Entscheidung:** Begriffsdefinition wurde entfernt (Mehrwert gering, Zeitaufwand hoch)

### Block 2 – Klassische FTF mit Webots (Termine 3–8, ca. 6 Wochen)
Hands-On-Phase mit der Simulationsumgebung **Webots** und physischer Hardware.

| Aufgabe | Beschreibung |
|---|---|
| **Hindernisvermeidung** | Eigenen Roboter modellieren, Controller zur Hindernisvermeidung implementieren |
| **Labyrinth** | Labyrinthalgorithmus entwickeln und präsentieren; Hardware-Demo im Alphabot |
| **Spurführung** | Linienverfolgung in Webots (Basis: 4 Sensoren; Extended: 8 Sensoren, andere Farben); Demo mit Dobot |

- **Exkursion:** Eingebettet in diesen Block (26.05.)

### Block 3 – Autonome FTF mit ROS (Termine 9–10, ca. 2 Wochen)
Einstieg in **ROS (Robot Operating System)** als Robotik-Middleware.

| Einheit | Inhalte |
|---|---|
| **ROS-Grundlagen** | Warum ROS? Struktur, Packages, Topics; Demo mit Turtlebot-Sensordaten; Hands-On mit Create 3 Simulator |
| **SLAM & Navigation** | Lokalisierung (GPS, Apriltags, Indoor), SLAM, Pfadplanung; Gazebo-Simulator (Turtlebot 3/4); Demo mit echtem Turtlebot |
| **Manipulation** | Demo: Roboterarm des LoCoBot; Hands-On: Python-Bewegungsablauf im LoCoBot-Simulator |

### Block 4 – FTS-Simulation (Termine 11–13, ca. 3 Wochen)
- **Thema:** Simulation der Wellenfertigung – klassisch vs. mit FTS
- Ausgabe → Bearbeitung → (vermutlich: Präsentation)

### Zusatzleistung – Business Case
- Marktrecherche & Informationsbeschaffung
- Business-Case-Berechnung
- Lastenheft
- Nutzwertanalyse

---

## 4. Bekannte Schwachstellen & Verbesserungsbedarf

Diese Punkte wurden aus den Erfahrungen des letzten Semesters identifiziert und sollen in dieser Iteration adressiert werden:

### 4.1 Webots-Einstieg zu schwer
- **Problem:** Studierende hatten große Schwierigkeiten mit dem Einstieg in Webots; die Bearbeitungszeit musste verlängert werden.
- **Geplante Maßnahmen:**
  - Das Labyrinth bereits vorgeben, damit sich Studierende auf das FTF-Verhalten konzentrieren können (nicht auf die Modellierung der Umgebung)
  - Bessere/strukturiertere Einführungstutorials bereitstellen
  - VM-Setup vereinfachen oder Schritt-für-Schritt-Anleitung ergänzen
- **Status:** ⏳ Offen – Material muss erstellt werden

### 4.2 ROS-Einheit ausbauen
- **Problem:** ROS-Block ist inhaltlich skizziert, aber die Hands-On-Aufgaben sind noch nicht vollständig ausgearbeitet.
- **Geplante Maßnahmen:**
  - Detaillierte Aufgabenblätter für ROS-Grundlagen, SLAM und Navigation
  - Demo-Apriltags integrieren
  - Mini-Projekt: Programmierung eines ROS-Nodes
- **Status:** ⏳ Offen – Aufgaben müssen konkretisiert werden

### 4.3 FTS-Simulation konkretisieren
- **Problem:** Die Aufgabenstellung zur Wellenfertigung-Simulation ist noch zu vage.
- **Geplante Maßnahmen:**
  - Klare Aufgabenstellung mit Szenario, Anforderungen und Bewertungskriterien formulieren
  - Entscheiden, welches Simulationswerkzeug eingesetzt wird
- **Status:** ⏳ Offen – Aufgabenstellung muss geschrieben werden

### 4.4 Prüfungsleistung / Business Case strukturieren
- **Problem:** Business Case ist als Zusatzleistung aufgeführt, aber nicht klar strukturiert.
- **Geplante Maßnahmen:**
  - Vorlage / Template für den Business Case erstellen
  - Bewertungsrubrik definieren
  - Prüfen, ob als Pflicht- oder Wahlleistung sinnvoll
- **Status:** ⏳ Offen – Konzept und Vorlage ausstehend

---

## 5. Entscheidungslog

Hier werden alle getroffenen Entscheidungen dokumentiert, damit sie nachvollziehbar bleiben.

| Datum | Entscheidung | Begründung |
|---|---|---|
| 2026-03-23 | CLAUDE.md als zentrales Projektgedächtnis eingeführt | Persistente Dokumentation über Sitzungen hinweg; versioniert im Git-Repo |
| 2026-03-23 | Begriffsdefinition aus Block 1 entfernt (aus Vorjahr übernommen) | Mehrwert gering, Zeitaufwand für Studierende zu hoch |
| 2026-03-23 | Labyrinth soll künftig vorgegeben werden | Studierende sollen sich auf FTF-Algorithmen konzentrieren, nicht auf Webots-Modellierung |

---

## 6. Geplante Arbeitspakete

Die folgende Liste gibt den geplanten Arbeitsfortschritt wieder und wird laufend aktualisiert.

- [ ] **AP1:** Überarbeitetes Vorlesungskonzept als strukturiertes Dokument (Word/Markdown)
- [ ] **AP2:** Webots-Einführungstutorial erstellen (VM-Setup, erster Roboter, erste Controller)
- [ ] **AP3:** Labyrinth-Aufgabe überarbeiten (vorgegebenes Labyrinth + klare Aufgabenstellung)
- [ ] **AP4:** Spurführungs-Tutorial für Webots definieren (Basis + Extended)
- [ ] **AP5:** ROS-Aufgabenblatt: Grundlagen + Umgebungsaufbau
- [ ] **AP6:** ROS-Aufgabenblatt: SLAM und Navigation im Gazebo-Simulator
- [ ] **AP7:** Mini-Projekt ROS-Node definieren und ausarbeiten
- [ ] **AP8:** Aufgabenstellung FTS-Simulation (Wellenfertigung) schreiben
- [ ] **AP9:** Business-Case-Template erstellen + Bewertungsrubrik
- [ ] **AP10:** Gesamtkonzept finalisieren und mit neuem Semester-Terminplan aktualisieren

---

## 7. Werkzeuge und Technologien

| Werkzeug | Verwendung in der Vorlesung |
|---|---|
| **Webots** | Simulation klassischer FTF (Hindernisvermeidung, Labyrinth, Spurführung) |
| **Alphabot** | Hardware-Demo für Labyrinth-Algorithmen |
| **Dobot** | Hardware-Demo für Spurführung |
| **ROS** | Middleware für autonome FTF (Grundlagen, SLAM, Navigation, Manipulation) |
| **Gazebo** | Simulator für ROS-Aufgaben (Turtlebot 3/4) |
| **Create 3 Simulator** | Erste ROS-Versuche |
| **LoCoBot** | Manipulation: Demo + Python-Simulation |
| **Turtlebot 3/4** | SLAM & Navigation Demo (echte Hardware) |

---

## 8. Konventionen für dieses Repository

- **Sprache:** Deutsch (Vorlesungsmaterial), Englisch (Code, Kommentare)
- **Ordnerstruktur:** wird mit erstem Arbeitspaket definiert
- **Commits:** Aussagekräftige Commit-Messages auf Deutsch, z.B. `feat: Webots-Tutorial Grundlagen hinzugefügt`
- **Branches:** Feature-Branches für größere Arbeitspakete, direkte Commits auf `main` für Dokumentation
- **CLAUDE.md:** Wird bei jeder relevanten Entscheidung oder abgeschlossenen Aufgabe aktualisiert

---

*Erstellt von Claude (Anthropic) in Zusammenarbeit mit dem Dozenten – 2026-03-23*
