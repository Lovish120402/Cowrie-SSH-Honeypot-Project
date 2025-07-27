# Cowrie-SSH-Honeypot-Project
A basic but realistic honeypot project built using Cowrie to simulate a vulnerable SSH server, capture attacker activity, and practice log analysis and blue team defensive skills.
📌 Table of Contents
About the Project

Tools & Environment

Project Objectives

Setup Process

Attack Simulation

Results & Analysis

Real-World Cybersecurity Use

Improvements & Future Work

Screenshots

📖 About the Project
Cowrie is a medium-interaction SSH and Telnet honeypot designed to mimic a real Linux system. This project demonstrates how attackers behave once they brute-force SSH credentials and begin exploring a system.

The goal is to observe, log, and analyze malicious behavior in a controlled and safe virtual lab.

💻 Tools & Environment
Tool	Purpose
Ubuntu 22.04 VM	Host Cowrie honeypot
Kali Linux VM	Attacker machine
VirtualBox	Virtualization platform for VMs
Cowrie	SSH Honeypot
Hydra	Brute-force tool for SSH attacks
Nmap	Network scanner

🎯 Project Objectives
Deploy and configure Cowrie on Ubuntu

Simulate real-world brute-force and SSH attacks from Kali

Capture attacker behavior (logins, commands, scanning)

Analyze logs in real time

Understand how honeypots support threat detection

⚙️ Setup Process
1. Install Dependencies
bash
Copy
Edit
sudo apt update && sudo apt upgrade -y
sudo apt install git python3-virtualenv python3-pip libssl-dev libffi-dev build-essential libpython3-dev libxslt1-dev -y
2. Clone and Setup Cowrie
bash
Copy
Edit
cd /opt
sudo git clone https://github.com/cowrie/cowrie.git
sudo chown -R $USER:$USER cowrie
cd cowrie
3. Create and Activate Python Virtual Environment
bash
Copy
Edit
virtualenv --python=python3 cowrie-env
source cowrie-env/bin/activate
4. Install Python Packages
bash
Copy
Edit
pip install --upgrade pip
pip install -r requirements.txt
5. Configure and Start Cowrie
bash
Copy
Edit
cp etc/cowrie.cfg.dist etc/cowrie.cfg
bin/cowrie start
6. Monitor Logs
bash
Copy
Edit
tail -f /opt/cowrie/var/log/cowrie/cowrie.log
💥 Attack Simulation (From Kali)
✅ Ping the Target
bash
Copy
Edit
ping 192.168.56.10
🔍 Network Scan with Nmap
bash
Copy
Edit
nmap 192.168.56.10
🔓 Brute-Force with Hydra
bash
Copy
Edit
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.56.10 -s 2222 -t 4
🧪 Manual SSH Login (Simulated)
bash
Copy
Edit
ssh root@192.168.56.10 -p 2222
🕵️‍♂️ Commands Executed After Login
bash
Copy
Edit
whoami
pwd
ls -al /
cat /etc/passwd
All attacker interactions are logged by Cowrie.

📊 Results & Analysis
Cowrie logged:

Source IPs

Login attempts (user/pass)

Commands used

Fake file system exploration

Sample log entries (from cowrie.log / cowrie.json):

json
Copy
Edit
{
  "eventid": "cowrie.command.input",
  "input": "whoami",
  "timestamp": "..."
}
🛡️ Real-World Cybersecurity Use
Threat Intelligence: Log real attacker techniques, tools, and patterns.

SOC Monitoring: Integrate with SIEM (e.g. Splunk) for alerting.

Training & Simulation: Practice detection and response in a safe lab.

Deception: Divert attacker focus from real systems.

💡 Improvements & Future Work
🔄 Forward logs to SIEM (e.g., ELK Stack, Splunk)

📩 Send real-time alerts via Discord or Telegram

🧪 Deploy other honeypots (HTTP, FTP) alongside Cowrie

📂 Add fake files like db_backup.sql, confidential.pdf as bait

🌍 Use GeoIP or ASN lookup to track attacker regions

📊 Build a small dashboard to view attacker stats (Python + Flask)

📸 Screenshots
Action	Screenshot Example
Cowrie Log Output	✅ tail -f cowrie.log
Hydra Brute Force in Action	✅ Terminal output with login attempts
SSH Login into Honeypot	✅ Fake shell prompt with whoami, pwd
Nmap Scan Results	✅ Open port 2222 visible

🧑‍💻 Author
Lovish Ramphul
