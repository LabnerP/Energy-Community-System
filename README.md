# Energy Community System – Semesterprojekt DISYS (FHTW SS2025)

![BWI-VZ-4-SS2025-DISYS-EN_154847_ 📄 Specification Semester Project _ FHTW Moodle](https://github.com/user-attachments/assets/a208c322-ef44-476a-a9e3-8938ec534ca0)

### Projektziel

Ziel dieses Projekts ist der Aufbau eines verteilten Systems zur Simulation einer **Energie-Community**. Eine Energie-Community besteht aus mehreren Teilnehmer:innen, die gemeinschaftlich Energie **produzieren**, **nutzen**, und mit dem öffentlichen **Stromnetz interagieren**.

Die Energieflüsse werden über eine **Message Queue** koordiniert, von verschiedenen Diensten verarbeitet und über eine **grafische Oberfläche visualisiert**.

---

### Technologien

- **Spring Boot (REST API & Services)**
- **JavaFX (GUI)**
- **RabbitMQ**
- **Wetter-API** (für realistische Produktionswerte)
- **PostgreSQL**
- **Docker**

---
### Component Diagram 
![BWI-VZ-4-SS2025-DISYS-EN_154847_ 📄 Specification Semester Project _ FHTW Moodle](https://github.com/user-attachments/assets/d52f6883-d847-49b1-b7ea-389008cfb654)

---
### Systemkomponenten

#### 1. Community Energy Producer
- Sendet PRODUCER-Nachrichten an die Message Queue
- Enthält: `kwh`, `datetime`, `type: PRODUCER`, `association: COMMUNITY`
- Nutzt Wetterdaten zur Bestimmung der Produktionsmenge
- Hauptzuständig: Niklas Sterling

#### 2. Community Energy User 
- Sendet USER-Nachrichten an die Queue
- Enthält: `kwh`, `datetime`, `type: USER`, `association: COMMUNITY`
- Benötigt mehr Energie zu Spitzenzeiten (z. B. morgens, abends)
- Hauptzuständig: Niklas Sterling

#### 3. Usage Service
- Verarbeitet PRODUCER/USER-Messages
- Berechnet pro Stunde:
  - community_produced
  - community_used
  - grid_used
- Aktualisiert `usage_hourly`-Tabelle
- Hauptzuständig: Johannes Voraberger

#### 4. Current Percentage Service
- Reagiert auf Usage-Updates
- Berechnet:
  - `community_depleted` (%)
  - `grid_portion` (%)
- Speichert Werte in `current_percentage`-Tabelle
- Hauptzuständig: Philipp Labner

#### 5. REST API (Spring Boot) 
- Endpunkte:
  - `GET /energy/current` → Aktuelle Prozentwerte
  - `GET /energy/historical?start=...&end=...` → Daten für Zeitraum
- Liest Daten aus der Datenbank
- Wird von der GUI genutzt
- Hauptzuständig: Johannes Voraberger

#### 6. JavaFX GUI
- Visualisiert Energieverteilung:
  - Aktueller Grid-/Community-Anteil
  - Historischer Verlauf (z.B. Charts, Tabellen)
- Fragt die REST API ab
- Hauptzuständig: Philipp Labner

### Team 
Studentisches Entwicklerteam des FH Technikum Wiens, bestehend aus:

- Philipp Labner
- Johannes Voraberger
- Niklas Sterling

### Status
Das Projekt ist Abgeschlossen.

### Hinweise
Dieses Projekt dient ausschließlich zu Lernzwecken im Rahmen der Lehrveranstaltung Distributed Systems SSe2025.

### Repository-Historie
Aufgrund des fehlenden Zugriffs auf den ursprünglichen GitHub-Account wurde das Projekt in ein neues Repository migriert. Die vollständige Git-Historie, einschließlich der ursprünglichen Commits und Branches, wurde dabei erhalten.
