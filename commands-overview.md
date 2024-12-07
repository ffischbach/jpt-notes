# Pentesting Command Reference

## Inhaltsverzeichnis
1. [Reconnaissance (Aufklärung)](#reconnaissance)
2. [Scanning und Enumeration](#scanning-und-enumeration)
3. [Exploitation](#exploitation)
4. [Post-Exploitation](#post-exploitation)
5. [Privilege Escalation](#privilege-escalation)
6. [Persistenz](#persistenz)
7. [Abschluss und Reporting](#abschluss-und-reporting)

---

## Setup

Ordner für anstehenden Pentest anlegen.
```
mkdir 172.28.255.0
```

Directory Setup Skripte herunterladen: [Hier Herunterladen](example.com) 

## Scanning und Enumeration

### Hostscanning
```
nmap -sn 172.28.255.0/24 -oG - | awk '/Up$/{print $2}' > reachable_hosts.txt 
```
> **Pingscan alle Hosts im Subnetz & Ergebnis in reachable_hosts.txt Datei speichern.**<br /> 
Parameter: -sn = Ping scan ohne Ports, -oG - = Grepable format output;

<br />

### Port und Service Enumeration
```
 
```
> **.**<br /> 

<br />

---

## Exploitation
### Schwachstellenanalyse
- Tools und Techniken zur Identifikation von Schwachstellen

### Ausnutzung
- Exploits für Schwachstellen ausführen
- Beispiele: Metasploit, manueller Exploit-Code

---

## Post-Exploitation
### Zugangssicherung
- Shell-Zugriff stabilisieren oder absichern
- Beispiele: Reverse Shells, Bind Shells

### Datensammlung
- Sammeln von sensiblen Informationen
- Beispiele: Passwort-Hashes, Datenbanken

---

## Privilege Escalation
### Lokale Privilegien-Eskalation
- Erhöhen von Berechtigungen auf dem Zielsystem
- Beispiele: Kernel-Exploits, SUID-Binaries

### Netzwerkbasierte Privilegien-Eskalation
- Seitliche Bewegung im Netzwerk oder auf andere Hosts
- Beispiele: Pass-the-Hash, Kerberos-Attacken

---

## Persistenz
### Hintertüren und Zugangspunkte
- Sicherstellen, dass der Zugriff nach dem Angriff bestehen bleibt
- Beispiele: Cronjobs, Autostart-Einträge

### Vermeidung von Erkennung
- Verschleierung von Aktivitäten
- Beispiele: Anti-Forensik, Logs manipulieren

---

## Abschluss und Reporting
### Log- und Artefaktprüfung
- Überprüfen und Entfernen von Spuren

### Erstellung des Berichts
- Strukturierte Dokumentation der Erkenntnisse, Schwachstellen und Empfehlungen

---

## Anmerkungen
- Platz für zusätzliche Informationen, Notizen oder Verweise auf Ressourcen
