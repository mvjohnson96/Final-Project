# 🛡️ Honeypot Security Automation Project

## 📌 Project Overview

This project implements a basic **honeypot** using Python on a **Windows Server 2019** environment. Its purpose is to simulate a vulnerable system to attract, log, and analyze unauthorized access attempts. A secondary **Windows 11 laptop** is used to simulate attacks for testing purposes.

This project supports cybersecurity learning objectives by providing hands-on experience with network security monitoring, automation scripting, and intrusion detection fundamentals.

---

## 🎯 Objectives

- Build and deploy a Python-based honeypot on Windows Server 2019.
- Simulate threat actor behavior using a Windows 11 client machine.
- Log incoming connection attempts and record them for future analysis.
- Implement optional enhancements like port filtering and geolocation tracking.
- Use AI tools to assist in design, coding, and debugging.

---

## 🚀 Getting Started

### Prerequisites

Ensure the following are installed on your system:

- Windows Server 2019 with PowerShell 5.1+
- Python 3.10+ (Download: https://www.python.org/downloads/)
- Windows 11 client (for simulation)
- Text editor (e.g., Notepad++, VS Code)
- Optional: Git and GitHub CLI

### Installation

1. **Install Python on Windows Server 2019:**
   - Download the installer from [python.org](https://www.python.org/)
   - Add Python to PATH during setup
   - Confirm installation:
     ```powershell
     python --version
     ```

2. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/honeypot-security-project.git
   cd honeypot-security-project
