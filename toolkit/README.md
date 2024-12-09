# README für das Penetration Testing Toolkit

## Features

- **Interaktives Menü**: Benutzer können aus einer Vielzahl von Scans wählen und die Ergebnisse einfach speichern und verwalten.
- **Mehrstufige Scans**:
  - Vollständiger Netzwerkscan (Ping-Scan) zur Identifikation aktiver Hosts.
  - Scan aller gefundenen Hosts mit detaillierter Port- und Dienstanalyse.
  - Tiefenscan (alle Ports) für eine umfassendere Untersuchung.
  - Einzelne Host-Scans nach Bedarf.
  - UDP-Port-Scans für versteckte Hosts.
  - Scan zur Erkennung von versteckten Hosts mit offenen Ports.
- **Ergebnisverwaltung**:
  - Automatische Speicherung der Scan-Ergebnisse in übersichtlichen Ordnerstrukturen.
  - Option zum Löschen aller gespeicherten Scan-Ergebnisse.
- **Timeout-Schutz**: Scans sind zeitlich begrenzt, um Endlosschleifen zu verhindern.
- **Detailliertes Reporting**: Ergebnisse werden in Textdateien und Nmap-kompatiblen Formaten gespeichert.

---

## Installation

### Voraussetzungen

1. **Python 3.7+** ist erforderlich.
2. Folgende Python-Pakete müssen installiert sein:
   - `pyfiglet`
   - `colorama`
3. **Nmap** muss auf dem System installiert sein und über die Kommandozeile ausführbar sein.

### Installation der Abhängigkeiten

```bash
pip install pyfiglet colorama
```

---

## Verwendung

### Starten des Tools

```bash
python pentest-toolkit.py
```

### Hauptmenü

Das Hauptmenü bietet folgende Optionen:

1. **Nmap Full Network Scan**  
   Führt einen Ping-Scan durch, um aktive Hosts im angegebenen Netzwerk zu identifizieren.

2. **Nmap Scan aller gefundenen Hosts**  
   Scannt identifizierte Hosts mit Dienst- und Versionserkennung sowie Standard-Skripten.

3. **Nmap Deep Scan (alle Ports) aller gefundenen Hosts**  
   Führt einen umfassenden Scan durch, der alle Ports auf den gefundenen Hosts überprüft.

4. **Nmap Single Client Scan**  
   Detaillierter Scan eines einzelnen Hosts.

5. **Nmap UDP Ports Scan auf versteckten Hosts**
   Scan von spezifischen UDP-Ports auf versteckten Hosts.

6. **Nmap Hidden Hosts Scan**  
   Erkennung von Hosts, die auf normalen Ping-Scans nicht antworten.

7. **Löschen aller Scan-Ergebnisse**  
   Entfernt alle gespeicherten Scan-Daten.

8. **Beenden**  
   Schließt das Programm.

---

## Ergebnisse

- Alle Scan-Ergebnisse werden automatisch in Verzeichnissen gespeichert, z. B. `scan_results_192.168.1.0_24`.
- Ergebnisse umfassen:
  - Textdateien mit den Scanausgaben.
  - Nmap-kompatible `.xml`- und `.gnmap`-Dateien (bei Verwendung der `-oA`-Option).

---

## Hinweise

- **Timeout**: Scans sind teilweise auf 5 Minuten begrenzt, um Hänger zu vermeiden.
- **Erweiterbarkeit**: Das Tool kann leicht erweitert werden, um zusätzliche Nmap-Befehle oder Funktionen zu integrieren.
- **Sicherheitsaspekt**: Verwenden Sie das Toolkit nur mit Genehmigung des Netzwerkbesitzers.

---

## Haftungsausschluss

Dieses Toolkit dient ausschließlich zu Bildungs- und Sicherheitszwecken. Der Entwickler übernimmt keine Verantwortung für unbefugte oder illegale Nutzung.