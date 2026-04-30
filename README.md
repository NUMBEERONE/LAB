# LAB
Alright—here’s the **full, structured, production-style process** to turn your Kali WSL (now on E: drive) into a proper **pentesting lab**, not just a tool dump.

We’re building this like a mini cyber range: clean, repeatable, and actually useful for CTFs, bug bounty practice, and coursework.

---

# 🧱 PHASE 1 — Clean Foundation (Kali Core Setup)

Inside Kali:

```bash id="base1"
sudo apt update && sudo apt full-upgrade -y
```

### Install Kali meta tools (balanced, not bloated)

```bash id="base2"
sudo apt install -y kali-linux-default
```

👉 If you want heavier arsenal later:

* `kali-linux-large` (more tools)
* avoid `kali-linux-everything` (chaos + disk waste)

---

# 🧰 PHASE 2 — Core Pentesting Stack

## 🔍 Recon & Enumeration

```bash id="tool1"
sudo apt install -y nmap masscan whois dnsutils
```

## 🌐 Web Exploitation

```bash id="tool2"
sudo apt install -y burpsuite sqlmap gobuster ffuf nikto
```

## 💣 Exploitation Frameworks

```bash id="tool3"
sudo apt install -y metasploit-framework
```

Initialize:

```bash id="tool4"
sudo msfdb init
```

## 🔐 Password Attacks

```bash id="tool5"
sudo apt install -y john hashcat hydra crunch
```

## 🧪 Post Exploitation

```bash id="tool6"
sudo apt install -y netcat-traditional socat rlwrap
```

---

# 📚 PHASE 3 — Intelligence + Wordlists (Critical)

```bash id="intel1"
sudo apt install -y seclists wordlists
```

Optional upgrade:

```bash id="intel2"
git clone https://github.com/danielmiessler/SecLists.git ~/SecLists
```

---

# 🐳 PHASE 4 — Build Your Vulnerable Lab (MOST IMPORTANT)

This is where Kali becomes a *real lab*.

## Install Docker

```bash id="dock1"
sudo apt install -y docker.io
sudo service docker start
sudo usermod -aG docker $USER
```

Restart WSL after this.

---

## 🧨 Deploy vulnerable apps

### 🔹 DVWA (classic web hacking)

```bash id="lab1"
docker run -d -p 8080:80 vulnerables/web-dvwa
```

### 🔹 OWASP Juice Shop (modern target)

```bash id="lab2"
docker run -d -p 8081:3000 bkimminich/juice-shop
```

### 🔹 vulnerable API / lab (optional)

```bash id="lab3"
docker run -d -p 5000:5000 vulnerables/web-nodejs
```

---

## 🌍 Your local targets now:

* [http://localhost:8080](http://localhost:8080) → DVWA
* [http://localhost:8081](http://localhost:8081) → Juice Shop
* [http://localhost:5000](http://localhost:5000) → API lab

---

# 🧠 PHASE 5 — Shell & Exploit Workflow Setup

```bash id="shell1"
sudo apt install -y python3 python3-pip python3-venv
pip3 install pwntools requests
```

Reverse shell tools:

```bash id="shell2"
nc -lvnp 4444
```

Upgrade shells:

```bash id="shell3"
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

---

# 🕵️ PHASE 6 — Web Hacking Toolkit

```bash id="web1"
sudo apt install -y feroxbuster wfuzz dirsearch
```

---

# 🔐 PHASE 7 — Privilege Escalation Tools

```bash id="priv1"
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
chmod +x linpeas.sh
```

Run later on targets:

```bash id="priv2"
./linpeas.sh
```

---

# 🧩 PHASE 8 — Networking Reality Setup (Important Limitation)

WSL = NOT full network lab.

### ❌ You CANNOT:

* use Wi-Fi monitor mode
* do packet injection
* run wireless hacking labs

### ✔ You CAN:

* web hacking
* internal network simulation
* API exploitation
* CTF practice

---

# 🖥️ PHASE 9 — Upgrade Environment (Make it usable daily)

## ZSH shell

```bash id="ui1"
sudo apt install -y zsh git curl
chsh -s /bin/zsh
```

Install Oh My Zsh:

```bash id="ui2"
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

---

# ⚙️ PHASE 10 — Lab Organization (Pro setup mindset)

Create structure:

```bash id="org1"
mkdir -p ~/lab/{recon,exploits,notes,tools,wordlists}
```

Suggested workflow:

* `recon/` → scans, nmap results
* `exploits/` → payloads, scripts
* `notes/` → findings, writeups
* `tools/` → custom scripts

---

# 🚀 PHASE 11 — Final Test (Make sure everything works)

Run:

```bash id="test1"
nmap localhost
```

Open:

* DVWA
* Juice Shop

Try:

* login bypass
* SQL injection
* directory brute force

---

# 🧠 Reality Check (no sugar coating)

This setup makes you:
✔ CTF-ready
✔ Bug bounty capable
✔ Web exploitation focused

But:

* It is NOT a full wireless hacking lab
* It is NOT a full network simulation environment

---

# 🔥 If you want next level (serious upgrade path)

I can help you build:

### 🧪 Option A: Full Cyber Range

* attacker VM (Kali)
* victim VM (Windows/Linux)
* logging server (SIEM)

### 🧠 Option B: SOC + SIEM Lab

* Wazuh
* ELK stack
* attack detection pipeline

### 💣 Option C: Advanced Exploitation Lab

* buffer overflows
* binary exploitation
* reverse engineering setup

---

Just tell me your direction.
