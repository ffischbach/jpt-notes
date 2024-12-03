---
title: HashCat
layout: default
nav_order: 4
---

# Hashcat

Hashcat ist ein Tool zum Knacken von Passwörtern, das verschiedene Angriffsmodi und Hash-Typen unterstützt.

### **Grundlegende-Syntax**
```bash
hashcat -m <hash_mode> -a <attack_mode> [optionen] <hash_file> [dictionary|mask]
```

### **Wichtige Parameter**
- **`-m` (Hash-Modus):** Gibt den Typ des Hashes an (z. B. NTLM, SHA256).  
  **Beispiel:**
  - `0` → MD5
  - `1000` → NTLM
  - `1800` → SHA512crypt (Unix)
  - Weitere Modi: [Hashcat-Modi Liste](https://hashcat.net/wiki/doku.php?id=hashcat)

- **`-a` (Angriffsmodus):** Legt die Angriffsmethode fest.
  **Beispiele:**
  - `0` → Wörterbuchangriff
  - `1` → Kombinationsangriff
  - `3` → Brute-Force-Angriff
  - `6` → Wörterbuch + Maskenangriff
  - `7` → Maskenangriff + Wörterbuch

- **`-o` (Output-Datei):** Speichert geknackte Hashes in einer Datei.

- **`-r` (Regeln):** Wendet Regeln auf Wörterlisten an (z. B. Permutationen).

- **`--show`:** Zeigt bereits geknackte Hashes aus der Ergebnisdatei an.

### **Beispiele für Hashcat-Befehle**

#### **1. Wörterbuchangriff (Dictionary Attack)**
```bash
hashcat -m 1000 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```
- **`-m 1000`** → NTLM-Hashes.
- **`-a 0`** → Wörterbuchangriff.
- **`hashes.txt`** → Datei mit Hashes.
- **`rockyou.txt`** → Wörterliste (z. B. RockYou).

#### **2. Brute-Force-Angriff**
```bash
hashcat -m 1000 -a 3 hashes.txt ?a?a?a?a
```
- **`-a 3`** → Brute-Force-Angriff.
- **`?a?a?a?a`** → Maskensyntax für alle möglichen Zeichen (4 Zeichen lang).

#### **3. Maskenangriff**
```bash
hashcat -m 1000 -a 3 hashes.txt ?u?l?l?d?d
```
- **`?u`** → Ein Großbuchstabe.
- **`?l`** → Zwei Kleinbuchstaben.
- **`?d`** → Zwei Ziffern.
- **Ergebnis:** Passwörter wie `Abc12`.

#### **4. Kombination aus Wörterbuch und Regeln**
```bash
hashcat -m 1000 -a 0 -r rules/best64.rule hashes.txt /usr/share/wordlists/rockyou.txt
```
- **`-r rules/best64.rule`** → Wendet häufige Permutationen auf die Wörterliste an (z. B. Passwort123).


