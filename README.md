# 🔍 AIScan - AI-Powered Security Scanner

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Bash](https://img.shields.io/badge/Bash-5.0+-green.svg)](https://www.gnu.org/software/bash/)
[![Ollama](https://img.shields.io/badge/Ollama-Required-blue.svg)](https://ollama.ai)

> An intelligent automated security scanner that combines multiple penetration testing tools with AI analysis powered by Ollama.

## ✨ Features

- 🤖 **AI-Powered Analysis** - Uses Ollama LLMs to intelligently analyze scan results
- 🛠️ **Multi-Tool Integration** - Combines 9+ security scanning tools
- 📊 **Structured Reports** - Beautiful table-based output with detailed attack scenarios
- ⚡ **Flexible Scanning** - Quick, Standard, and Full scan modes
- ⏭️ **Interactive Controls** - Skip slow scans on-the-fly with 's' key
- 📄 **Auto-Save Reports** - Saves complete reports to timestamped files
- 🎯 **Attack Vector Analysis** - Shows HOW vulnerabilities can be exploited
- 🔒 **Educational** - Explains vulnerabilities and exploitation techniques

## 🎬 Demo

```bash
$ aiscan example.com

🎯 Target: example.com
🤖 AI Model: llama3.2
⚡ Scan Mode: Standard

[1/10] Running WhatWeb...
✓ Complete (2s)

[2/10] Running Nmap...
✓ Complete (8s)

...

📊 SCAN RESULTS SUMMARY
⏱️  Total scan time: 1m 45s

🤖 AI SECURITY ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🎯 Executive Summary

| Metric | Value |
|--------|-------|
| Overall Risk Level | HIGH |
| Critical Vulnerabilities | 2 |
| Attack Surface Score | 6.5/10 |

...

🚨 VULNERABILITIES FOUND 🚨
```

## 🚀 Quick Start

### Prerequisites

- Linux/Unix system
- Bash 5.0+
- Root/sudo access (for some scans)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/aiscan.git
cd aiscan

# 2. Install dependencies
sudo apt update
sudo apt install nmap whatweb nikto curl dnsutils dirb sqlmap gobuster -y

# 3. Install Python tools
sudo pip3 install wafw00f sslyze

# 4. Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# 5. Pull an AI model
ollama pull llama3.2

# 6. Make executable and install
chmod +x aiscan
sudo mv aiscan /usr/local/bin/

# 7. Verify installation
aiscan --help
```

## 📖 Usage

### Basic Commands

```bash
# Standard scan
aiscan example.com

# Quick scan (faster, less thorough)
aiscan example.com --quick

# Full scan (comprehensive, includes all tools)
aiscan example.com --full

# Use specific AI model
aiscan example.com -m llama3.1

# Scan IP address
aiscan 192.168.1.1
```

### Configuration

Create a config file for persistent settings:

```bash
# Set default model
echo 'MODEL="llama3.1"' > ~/.aiscan.conf
```

### Interactive Features

- **Skip Scans**: Press `s` during any scan to skip it if it's taking too long
- **Real-time Progress**: Watch live progress with spinner and elapsed time
- **Auto-save**: Reports automatically saved to `aiscan_target_timestamp.txt`

## 🛠️ Integrated Tools

| Tool | Purpose | Required |
|------|---------|----------|
| **Nmap** | Port scanning & service detection | ✅ Yes |
| **WhatWeb** | Web technology fingerprinting | ⚠️ Recommended |
| **Nikto** | Web vulnerability scanning | ⚠️ Recommended |
| **Wafw00f** | WAF/CDN detection | ⚠️ Optional |
| **SSLyze** | SSL/TLS security analysis | ⚠️ Optional |
| **Dirb/Gobuster** | Directory enumeration | ⚠️ Optional |
| **SQLMap** | SQL injection testing | ⚠️ Optional |
| **cURL** | HTTP header analysis | ✅ Yes |
| **OpenSSL** | Certificate inspection | ✅ Yes |
| **dig/host** | DNS information gathering | ✅ Yes |

## 📊 Output Structure

The AI generates comprehensive reports with:

### 1. Executive Summary
- Overall risk level (CRITICAL/HIGH/MEDIUM/LOW)
- Total vulnerabilities found
- Attack surface score
- Immediate action recommendations

### 2. Target Information
- IP addresses, DNS records
- Web server and technology stack
- WAF/CDN detection
- SSL/TLS certificate details

### 3. Open Ports & Services
- All discovered open ports
- Service versions
- Risk assessment per service

### 4. Vulnerability Analysis
For each vulnerability:
- **Severity rating** (CRITICAL/HIGH/MEDIUM/LOW)
- **CVE/CVSS** scores (when applicable)
- **Attack Scenario** - Step-by-step exploitation guide
- **Impact** - What attacker can achieve
- **Remediation** - Specific fix commands

### 5. Attack Surface Analysis
- Potential attack vectors with difficulty ratings
- Attack chain scenarios
- Tools and techniques used by attackers

### 6. Security Headers
- Missing/present security headers
- Recommendations for each

### 7. Remediation Plan
- Prioritized fixes with effort estimates
- Copy-paste ready commands
- Verification steps

### 8. Security Score
- Weighted scoring across multiple categories
- Overall posture rating (X/10)

## 🎓 Educational Mode

AIScan doesn't just find vulnerabilities—it teaches you about them:

- **Why vulnerabilities exist** - Technical explanations
- **How attackers find them** - Reconnaissance techniques
- **How they exploit them** - Real exploitation methods with tools
- **Real-world impact** - Business and security implications

## 🔧 Advanced Usage

### Custom Model Configuration

```bash
# Try different models for different use cases
aiscan target.com -m llama3.3      # Latest, most capable
aiscan target.com -m mistral       # Fast alternative
aiscan target.com -m codellama     # Good for technical analysis
aiscan target.com -m gemma2        # Efficient and quick
```

### Scan Modes Comparison

| Mode | Speed | Tools Used | Best For |
|------|-------|------------|----------|
| **Quick** | ~2-5 min | Core tools only | Initial reconnaissance |
| **Standard** | ~5-10 min | Most tools | Regular security audits |
| **Full** | ~15-30 min | All tools including brute-force | Comprehensive pentest |

### CI/CD Integration

```bash
#!/bin/bash
# Example CI/CD security check

aiscan production-site.com --quick

if [ $? -eq 1 ]; then
    echo "CRITICAL vulnerabilities found!"
    # Send alert, fail pipeline, etc.
    exit 1
fi
```

## 🎯 Example Reports

### Vulnerability Report Sample

```
[VULN-001] Outdated Apache Server

| Field | Details |
|-------|---------|
| Severity | CRITICAL |
| CVE | CVE-2024-12345 |
| Component | Apache 2.4.41 |
| CVSS Score | 9.8 |

Attack Scenario (How to Exploit):
[Step 1] Attacker discovers Apache version via banner grabbing
[Step 2] Searches exploit-db for known exploits
[Step 3] Uses Metasploit module: exploit/linux/http/apache_mod_cgi
[Step 4] Gains remote code execution as www-data user

Impact:
- Remote code execution on web server
- Access to application database
- Potential lateral movement to internal network

Remediation:
- Update Apache to version 2.4.52+
  $ sudo apt update
  $ sudo apt install apache2
  $ sudo systemctl restart apache2
```

## 🐛 Troubleshooting

### Common Issues

**"Ollama not found"**
```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2
```

**"Tool not found" errors**
```bash
# Install missing tools
sudo apt install nmap whatweb nikto
sudo pip3 install wafw00f sslyze
```

**Scans hanging/timing out**
```bash
# Use quick mode
aiscan target.com --quick

# Or press 's' to skip stuck scans
```

**Permission denied errors**
```bash
# Some scans need root
sudo aiscan target.com
```

## ⚠️ Legal Disclaimer

**IMPORTANT**: Only use AIScan on systems you own or have explicit written permission to test.

- ✅ Authorized penetration testing
- ✅ Your own infrastructure
- ✅ Bug bounty programs (follow their rules)
- ❌ Unauthorized scanning
- ❌ Production systems without approval
- ❌ Any illegal activity

Unauthorized access to computer systems is illegal in most jurisdictions. Users are solely responsible for ensuring compliance with applicable laws and regulations.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Development Setup

```bash
git clone https://github.com/yourusername/aiscan.git
cd aiscan

# Test your changes
./aiscan localhost --quick

# Check for shellcheck issues
shellcheck aiscan
```

### Adding New Tools

To add a new scanning tool:

1. Add tool check in `check_dependencies()`
2. Add scan function call in main execution
3. Parse results and add to `ALL_RESULTS`
4. Update prompt to include new data type
5. Update README with tool info

## 📝 Changelog

### v1.0.0 (2025-01-13)
- Initial release
- 9 integrated security tools
- AI-powered analysis with Ollama
- Interactive skip feature
- Auto-save reports
- Three scan modes (quick/standard/full)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Ollama](https://ollama.ai) - Local LLM inference
- [Nmap](https://nmap.org) - Network scanning
- [Nikto](https://cirt.net/Nikto2) - Web vulnerability scanner
- [WhatWeb](https://github.com/urbanadventurer/WhatWeb) - Web fingerprinting
- All other open-source security tools integrated

## 📞 Support

- 🐛 [Report Issues](https://github.com/yourusername/aiscan/issues)
- 💡 [Feature Requests](https://github.com/yourusername/aiscan/issues)
- 📖 [Documentation](https://github.com/yourusername/aiscan/wiki)

## 🌟 Star History

If you find AIScan useful, please consider giving it a star! ⭐

---

**Made with ❤️ for the security community**

*Remember: With great power comes great responsibility. Happy (ethical) hacking!* 🔒
