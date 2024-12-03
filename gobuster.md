---
title: GoBuster
layout: default
nav_order: 3
---

#### Table of Contents
{: .no_toc .text-delta }

- 1
- 2
- 3
{:toc}

# GoBuster

GoBuster ist ein Tool zum Directory- und DNS-Fuzzing. Es wird hauptsächlich verwendet, um versteckte Verzeichnisse, Dateien und Subdomains auf Webservern zu entdecken. Es ist ein schnelles, command-line-basiertes Tool, das auf Bruteforce-Techniken basiert.

#### **Grundlegende Syntax**
```bash
gobuster <Modus> -u <URL/Ziel> -w <Wordlist> [Optionen]
```

---

### **Modi**

- **`dir`** → Suche nach versteckten Verzeichnissen und Dateien.  
- **`dns`** → Suche nach Subdomains basierend auf einer Wordlist.  
- **`vhost`** → Bruteforce für virtuelle Hosts.  
- **`fuzz`** → Generisches Fuzzing basierend auf Platzhaltern.  

---

### **Häufige Anwendungsfälle**

#### **1. Directory-Bruteforcing (dir-Modus)**
```bash
gobuster dir -u <URL> -w <Wordlist> [Optionen]
```

Beispiel:
```bash
gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt
```
- `-u` → Ziel-URL.  
- `-w` → Wordlist mit möglichen Verzeichnisnamen.  

Optionen:
- **`-x`** → Dateiendungen angeben (z. B. `.php, .html`).  
  ```bash
  gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt -x php,html
  ```
- **`-k`** → Ignoriert SSL-Zertifikatsfehler bei HTTPS.  
- **`-t`** → Anzahl gleichzeitiger Threads festlegen (Standard: 10).  
  ```bash
  gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt -t 20
  ```

#### **2. Subdomain-Bruteforcing (dns-Modus)**
```bash
gobuster dns -d <Domain> -w <Wordlist>
```

Beispiel:
```bash
gobuster dns -d example.com -w /usr/share/wordlists/dns/subdomains-top1million-5000.txt
```
- `-d` → Ziel-Domain.  

Optionen:
- **`-r`** → DNS-Server angeben.  
  ```bash
  gobuster dns -d example.com -w /path/to/wordlist.txt -r 8.8.8.8
  ```

#### **3. Virtuelle Hosts (vhost-Modus)**
```bash
gobuster vhost -u <URL> -w <Wordlist>
```

Beispiel:
```bash
gobuster vhost -u example.com -w /path/to/wordlist.txt
```

#### **4. Generisches Fuzzing (fuzz-Modus)**
```bash
gobuster fuzz -u <URL> -w <Wordlist>
```

Beispiel:
```bash
gobuster fuzz -u https://example.com/FUZZ -w /path/to/wordlist.txt
```
- Der Platzhalter `FUZZ` wird mit Werten aus der Wordlist ersetzt.

---

### **Erweiterte Optionen**

- **HTTP-Header anpassen:**  
  ```bash
  gobuster dir -u https://example.com -w /path/to/wordlist.txt -H "Authorization: Bearer <Token>"
  ```
- **Ausgabeformat:**  
  ```bash
  gobuster dir -u https://example.com -w /path/to/wordlist.txt -o ergebnisse.txt
  ```
- **Timeout festlegen:**  
  ```bash
  gobuster dir -u https://example.com -w /path/to/wordlist.txt --timeout 5s
  ```
- **Proxy nutzen:**  
  ```bash
  gobuster dir -u https://example.com -w /path/to/wordlist.txt --proxy http://127.0.0.1:8080
  ```

---

### **Typische Wordlists**

- **Für Directory-Scan:**  
  - `/usr/share/wordlists/dirb/common.txt`  
  - `/usr/share/wordlists/dirb/big.txt`  
- **Für DNS-Scan:**  
  - `/usr/share/wordlists/dns/subdomains-top1million-5000.txt`

---

### **Fehlerbehebung und Tipps**

- **Problem:** Langsame Scans.  
  **Lösung:** Erhöhe die Anzahl der Threads mit `-t`, z. B. `-t 50`.  

- **Problem:** Viele Fehler bei HTTPS-URLs.  
  **Lösung:** Nutze die Option `-k`, um SSL-Warnungen zu ignorieren.

- **Problem:** Kein Zugriff auf Ergebnisse.  
  **Lösung:** Verwende `-o`, um Ergebnisse in eine Datei zu speichern.  

---

### **Beispiele für verschiedene Szenarien**

1. **Verzeichnisse auf HTTPS-Server scannen (inkl. SSL-Fehler ignorieren):**
   ```bash
   gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt -k
   ```

2. **Subdomains scannen mit spezifischem DNS-Server:**
   ```bash
   gobuster dns -d example.com -w /usr/share/wordlists/dns/subdomains-top1million-5000.txt -r 8.8.8.8
   ```

3. **Verzeichnisse mit spezifischen Dateiendungen scannen:**
   ```bash
   gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt -x php,txt
   ```

4. **Scans durch Proxy leiten (z. B. Burp Suite):**
   ```bash
   gobuster dir -u https://example.com -w /path/to/wordlist.txt --proxy http://127.0.0.1:8080
   ```

---

### **Nützliche Ressourcen**

- [Offizielle GoBuster-Dokumentation](https://github.com/OJ/gobuster)  
- Wordlists: [SecLists Repository](https://github.com/danielmiessler/SecLists)  
