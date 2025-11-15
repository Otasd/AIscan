# 🔥 AIScan - AI-Powered Security Scanner

![Version](https://img.shields.io/badge/version-2.0-red)
![License](https://img.shields.io/badge/license-MIT-blue)
![Bash](https://img.shields.io/badge/bash-5.0+-green)
![Platform](https://img.shields.io/badge/platform-Linux-lightgrey)

**AIScan** is an aggressive automated security scanner with AI-powered vulnerability analysis. It integrates multiple security tools (Nmap, Nikto, SQLMap, etc.) and uses AI (via Ollama) to provide detailed exploitation guidance and remediation steps.

```
╔════════════════════════════════════════════╗
║                                            ║
║   🔥 AIScan - AGGRESSIVE MODE 🔥          ║
║        Security Deconstructor              ║
║                                            ║
╚════════════════════════════════════════════╝
```

## ⚡ Features

- 🎯 **15+ Security Tools Integration**: Nmap, Nikto, SQLMap, Nuclei, WhatWeb, and more
- 🤖 **AI-Powered Analysis**: Uses Ollama for detailed vulnerability analysis and exploitation guidance
- 📊 **Multiple Scan Modes**: Quick, Standard, and Full Aggressive scanning
- 📋 **Batch Scanning**: Scan multiple targets from a file
- 📝 **Comprehensive Logging**: Save all scan results to organized log files
- 🚫 **Flexible AI Options**: AI-less mode, external AI analysis, or Ollama integration
- ⚡ **Progress Indicators**: Real-time progress with skip functionality
- 🎨 **Beautiful Output**: Color-coded results with formatted tables

## 📦 Installation

### Prerequisites

**Required:**
- Bash 5.0+
- Nmap
- Curl
- Ollama (optional, only for AI analysis)

**Optional (for maximum power):**
- WhatWeb
- Nikto
- SQLMap
- Nuclei
- Wafw00f
- Commix
- XSStrike
- FFUF/Gobuster
- TestSSL

### Quick Install

```bash
# Clone the repository
git clone https://github.com/yourusername/aiscan.git
cd aiscan

# Make executable
chmod +x aiscan

# Install dependencies (Debian/Ubuntu)
sudo apt update
sudo apt install -y nmap curl whatweb nikto sqlmap ffuf

# Install Ollama (for AI analysis)
curl -fsSL https://ollama.com/install.sh | sh

# Pull AI model
ollama pull llama3.2
```

### Advanced Tool Installation

```bash
# Python-based tools
sudo pip3 install wafw00f commix xsstrike

# Nuclei (Go required)
GO111MODULE=on go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# TestSSL
git clone --depth 1 https://github.com/drwetter/testssl.sh.git ~/testssl.sh
```

## 🚀 Usage

### Basic Scanning

```bash
# Standard scan with AI analysis
./aiscan example.com

# Quick scan (fast, less intensive)
./aiscan example.com --quick

# Full aggressive scan
./aiscan example.com --full

# Scan without AI analysis
./aiscan example.com --no-ai
```

### Advanced Options

```bash
# Custom AI model
./aiscan example.com -m llama3.1

# Specific URL for injection tests
./aiscan example.com -u 'http://example.com/page.php?id=1'

# Save logs to custom directory
./aiscan example.com -o ./my_scans

# Combine options
./aiscan example.com --full --no-ai -o ./results
```

### Batch Scanning

```bash
# Create target list
cat > targets.txt << EOF
example.com
google.com
github.com
EOF

# Scan all targets
./aiscan -l targets.txt --no-ai -o ./batch_results

# Full aggressive batch scan
./aiscan -l targets.txt --full -o ./full_results
```

### AI Modes

```bash
# Standard mode (with Ollama)
./aiscan example.com

# AI-less mode (skip AI analysis)
./aiscan example.com --no-ai

# External AI analysis (from ChatGPT/Claude)
./aiscan example.com --external-ai analysis.txt

# Pipe external AI analysis
echo "AI analysis here" | ./aiscan example.com --external-ai -

# AI-only mode (analyze existing scan results)
./aiscan example.com --ai-only previous_scan.txt
```

## 📊 Scan Modes

| Mode | Description | Ports Scanned | Time Estimate | AI Analysis |
|------|-------------|---------------|---------------|-------------|
| **Quick** (`-q`) | Fast reconnaissance | Top 100 | 3-5 min | Optional |
| **Standard** (default) | Balanced scanning | Top 200 | 5-10 min | Yes |
| **Full** (`-f`) | Comprehensive scan | Top 1000 | 15-30 min | Yes |

## 🛠️ Tools Used

AIScan integrates the following security tools:

| Tool | Purpose | Required |
|------|---------|----------|
| **Nmap** | Port scanning & service detection | ✅ Yes |
| **Nikto** | Web server vulnerability scanning | ⭐ Recommended |
| **SQLMap** | SQL injection testing | ⭐ Recommended |
| **WhatWeb** | Web technology fingerprinting | ⭐ Recommended |
| **Nuclei** | Template-based vulnerability scanning | ⭐ Recommended |
| **Wafw00f** | WAF detection | ⚪ Optional |
| **Commix** | Command injection testing | ⚪ Optional |
| **XSStrike** | XSS vulnerability detection | ⚪ Optional |
| **FFUF/Gobuster** | Directory brute forcing | ⚪ Optional |
| **TestSSL** | SSL/TLS security analysis | ⚪ Optional |

## 📝 Configuration

Create a config file for persistent settings:

```bash
# Create config file
cat > ~/.aiscan.conf << EOF
# Default AI model
MODEL="llama3.2"

# Default output directory
OUTPUT_DIR="$HOME/security_scans"

# Default scan mode (quick/standard/full)
# QUICK_SCAN=true
# FULL_SCAN=true
EOF
```

## 📄 Output Examples

### Console Output

```
🎯 Target: example.com
🤖 AI Model: llama3.2
⚡ Scan Mode: Standard Aggressive
📁 Temp Directory: /tmp/aiscan_12345

[1/15] Running Nmap (Standard - Top 200 Ports + Vuln Scripts)...
✓ Complete (45s)

[2/15] Running WhatWeb (Aggressive Mode)...
✓ Complete (12s)

━━━ NMAP ━━━
PORT    STATE SERVICE  VERSION
80/tcp  open  http     nginx 1.18.0
443/tcp open  ssl/http nginx 1.18.0

🤖 AI SECURITY ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🎯 Executive Summary
| Metric | Value |
|--------|-------|
| **Overall Risk Level** | MEDIUM |
| **Total Critical Issues** | 0 |
| **Total High Issues** | 2 |
...
```

### Log File Structure

```
~/aiscan_logs/
├── example.com_20241115_143000.log
│   ├── NMAP results
│   ├── WhatWeb results
│   ├── Nikto results
│   ├── SQLMap results
│   ├── AI Analysis
│   └── Summary report
├── google.com_20241115_144000.log
└── github.com_20241115_145000.log
```

## 🔒 Security & Ethics

**⚠️ IMPORTANT WARNINGS:**

- ✅ **Only scan systems you own or have explicit written permission to test**
- ❌ **Unauthorized security testing is ILLEGAL**
- 🔐 **Keep scan reports secure - they contain sensitive information**
- 📋 **Document your authorization before scanning**
- ⚖️ **Respect rate limits and don't DoS targets**

This tool is designed for:
- ✅ Authorized penetration testing
- ✅ Security audits on your own systems
- ✅ Bug bounty programs (with permission)
- ✅ Educational purposes in controlled environments

## 🎓 AI Analysis Features

The AI analysis provides:

- 🎯 **Executive Summary**: Risk level, vulnerability counts, attack surface score
- 🌐 **Target Information**: Technologies, server details, open ports
- 🚨 **Critical Vulnerabilities**: With CVE numbers, CVSS scores, and exploitation steps
- ⚠️ **High Priority Issues**: Detailed technical descriptions
- 🔸 **Medium Priority Issues**: Tabulated findings
- 🔐 **Security Headers Analysis**: Missing headers and recommendations
- 📋 **Remediation Roadmap**: Prioritized action items with exact commands

## 🤖 Supported AI Models

Any Ollama model can be used. Popular choices:

```bash
# Install models
ollama pull llama3.2          # Fast, good balance
ollama pull llama3.1:70b      # More detailed analysis
ollama pull mistral           # Alternative option
ollama pull codellama         # Good for code analysis
ollama pull gemma2            # Lightweight option

# Use custom model
./aiscan example.com -m mistral
```

## 🐛 Troubleshooting

### Nmap freezing?
- Use `--quick` mode for faster scans
- Press 's' to skip slow scans
- Script automatically limits to common ports

### Ollama not found?
```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Or use AI-less mode
./aiscan example.com --no-ai
```

### Permission denied?
```bash
# Make script executable
chmod +x aiscan

# Some tools need sudo
sudo ./aiscan example.com
```

### Tool not found?
```bash
# Check which tools are missing
./aiscan --help

# Install missing tools (Ubuntu/Debian)
sudo apt install nmap nikto sqlmap whatweb

# Or run without optional tools
./aiscan example.com --quick --no-ai
```

## 📈 Roadmap

- [ ] Web UI dashboard
- [ ] JSON output format
- [ ] Integration with Metasploit
- [ ] Docker containerization
- [ ] API endpoint scanning
- [ ] Report templates (PDF, HTML)
- [ ] Continuous monitoring mode
- [ ] Vulnerability database integration

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This tool is provided for educational and authorized testing purposes only. The authors and contributors are not responsible for any misuse or damage caused by this tool. Always ensure you have explicit permission before scanning any systems that you do not own.

## 🌟 Star History

If you find this tool useful, please consider giving it a star! ⭐

## 📞 Contact

- Issues: [GitHub Issues](https://github.com/yourusername/aiscan/issues)
- Discussions: [GitHub Discussions](https://github.com/yourusername/aiscan/discussions)

---

**Made with ❤️ for the security community**

**Remember: With great power comes great responsibility. Hack ethically! 🛡️**
