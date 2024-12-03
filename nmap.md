---
title: Nmap
layout: default
nav_order: 7
---

# Nmap

Nmap ist ein mächtiges Open-Source-Tool für Netzwerkerkennung und Sicherheitsaudits. Es wird verwendet, um Netzwerke zu scannen, offene Ports und Dienste zu identifizieren sowie Betriebssysteme und Schwachstellen zu erkennen.

#### **Grundlegende Syntax**
```
nmap [Optionen] <Ziel>
```

---

### **Häufige Scans**

#### **1. Standard-Scan**
```bash
nmap <IP-Adresse/Host>
```
- Scannt die 1000 beliebtesten Ports auf dem Ziel.

Beispiel:
```bash
nmap 192.168.1.1
```

#### **2. Port-Scan**
- **Bestimmte Ports scannen:**
  ```bash
  nmap -p <Port-Bereich> <IP-Adresse/Host>
  ```
  Beispiel:
  ```bash
  nmap -p 80,443 192.168.1.1
  ```
- **Alle Ports scannen:**
  ```bash
  nmap -p- <IP-Adresse/Host>
  ```

#### **3. Service- und Versionsscan**
```bash
nmap -sV <IP-Adresse/Host>
```
- Identifiziert laufende Dienste und ihre Versionen.

Beispiel:
```bash
nmap -sV 192.168.1.1
```

#### **4. Betriebssystem-Erkennung**
```bash
nmap -O <IP-Adresse/Host>
```
- Versucht, das Betriebssystem des Ziels zu identifizieren.

#### **5. Netzwerk-Scan**
```bash
nmap <IP-Bereich>
```
Beispiel:
```bash
nmap 192.168.1.0/24
```
- Scannt alle Hosts im Subnetz.

---

### **Erweiterte Scans**

#### **1. Ping-Scan**
```bash
nmap -sn <IP-Adresse/Host>
```
- Prüft, ob das Ziel erreichbar ist, ohne Ports zu scannen.

#### **2. Stealth-Scan**
```bash
nmap -sS <IP-Adresse/Host>
```
- Halb-offener TCP-Scan (SYN-Scan), oft zur Umgehung von Firewalls verwendet.

#### **3. UDP-Scan**
```bash
nmap -sU <IP-Adresse/Host>
```
- Scannt offene UDP-Ports.

#### **4. Intensiver Scan**
```bash
nmap -T4 -A -v <IP-Adresse/Host>
```
- Führt einen detaillierten Scan mit Service-Erkennung, OS-Erkennung und Script-Scanning durch.

---

### **Optionen für Zielangabe**

- **Einzelne IP-Adresse:**
  ```bash
  nmap 192.168.1.1
  ```
- **Domain:**
  ```bash
  nmap example.com
  ```
- **IP-Bereich:**
  ```bash
  nmap 192.168.1.1-100
  ```
- **Subnetz:**
  ```bash
  nmap 192.168.1.0/24
  ```
- **Liste aus Datei:**
  ```bash
  nmap -iL <Dateipfad>
  ```

---

### **Nützliche Optionen**

#### **1. Ausgabeformate**
- **Normal:**
  ```bash
  nmap -oN <Dateipfad> <Ziel>
  ```
- **Greppable:**
  ```bash
  nmap -oG <Dateipfad> <Ziel>
  ```
- **XML:**
  ```bash
  nmap -oX <Dateipfad> <Ziel>
  ```
- **Alle Formate gleichzeitig:**
  ```bash
  nmap -oA <Basisname> <Ziel>
  ```

#### **2. Geschwindigkeit einstellen**
- **`-T0` bis `-T5`**: Geschwindigkeit (von langsam bis aggressiv).
  ```bash
  nmap -T4 <Ziel>
  ```

#### **3. Script-Scanning**
```bash
nmap --script=<Scriptname> <Ziel>
```
Beispiel:
```bash
nmap --script=vuln 192.168.1.1
```
- Nutzt NSE-Scripts, um Schwachstellen zu analysieren.

---

### **Beispiele für typische Scans**

#### **1. Top 1000 Ports**
```bash
nmap <IP-Adresse/Host>
```

#### **2. Alle Ports**
```bash
nmap -p- <IP-Adresse/Host>
```

#### **3. Ziel hinter Firewall**
```bash
nmap -Pn <IP-Adresse/Host>
```
- Überspringt den Ping-Test und scannt direkt.

#### **4. Schwachstellen-Scan**
```bash
nmap --script=vuln <IP-Adresse/Host>
```

#### **5. Subnetz-Scan**
```bash
nmap 192.168.1.0/24
```

#### **6. OS- und Service-Erkennung**
```bash
nmap -A <IP-Adresse/Host>
```

---

### **Fehlerbehebung und Tipps**

- **Problem:** Keine Antwort vom Ziel.  
  **Lösung:** Nutze `-Pn`, um ICMP-Blockaden zu umgehen.

- **Problem:** Firewall blockiert Scans.  
  **Lösung:** Verwende den Stealth-Scan (`-sS`).

- **Problem:** Ergebnisse unvollständig.  
  **Lösung:** Scanne alle Ports (`-p-`) oder erhöhe die Geschwindigkeit (`-T4`).

---

### **Nützliche Kombinationen**

1. **Pings von aktiven Hosts speichern:**
   ```bash
   nmap -sn 192.168.1.0/24 -oG - | grep "Up" > aktive_hosts.txt
   ```

2. **Service-Erkennung für eine Liste:**
   ```bash
   nmap -sV -iL ip-liste.txt -oA scan_ergebnisse
   ```

3. **Explizite Protokoll-Scans:**
   ```bash
   nmap -sS -sU 192.168.1.1
   ```
