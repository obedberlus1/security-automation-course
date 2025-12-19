# Automated Vulnerability Scanning and Notification System

## Project Overview
An automated vulnerability scanning and notification system designed to schedule scans, process data, send severity-based alerts, and maintain historical vulnerability tracking. This project demonstrates professional cybersecurity automation practices using open-source tools, Python scripting, and controlled testing environments.

## Table of Contents
- [Features](#features)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Screenshots](#screenshots)
- [Dependencies](#dependencies)
- [Development Environment](#development-environment)
- [Testing](#testing)
- [Ethical Considerations](#ethical-considerations)
- [Contributing](#contributing)
- [License](#license)

## Features
- **Automated Vulnerability Scanning**: Scheduled scans of target systems using industry-standard vulnerability scanners
- **Intelligent Parsing Engine**: Extracts and processes vulnerability data from scan outputs
- **Severity-Based Alerting**: Prioritizes vulnerabilities and sends notifications based on severity levels
- **Historical Tracking**: Maintains logs of vulnerabilities over time for trend analysis
- **Email Notifications**: Automated alerts for high-severity findings
- **Dashboard Reporting**: Visual representation of vulnerability status and trends
- **Virtual Environment Testing**: Isolated and safe testing environment for development

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Vulnerability Scanner                     │
│                   (Nmap/OpenVAS/Nessus)                      │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                   Scheduling Mechanism                       │
│              (Cron Jobs / Python Schedule)                   │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                     Parsing Engine                           │
│         (Python Script - Extract & Classify Data)            │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                   Alerting Component                         │
│              (Email / Dashboard Notifications)               │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                  Historical Tracking Log                     │
│                  (JSON / Database Storage)                   │
└─────────────────────────────────────────────────────────────┘
```

## Installation

### Prerequisites
- Python 3.8 or higher
- Anaconda (recommended for dependency management)
- Visual Studio Code (recommended IDE)
- Virtual machine software (VirtualBox, VMware, or Hyper-V)
- Git

### Step 1: Clone the Repository
```bash
git clone https://github.com/[your-username]/vulnerability-scanner.git
cd vulnerability-scanner
```

### Step 2: Create Virtual Environment
```bash
# Using Anaconda
conda create -n vuln-scanner python=3.8
conda activate vuln-scanner

# Or using venv
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Install Vulnerability Scanner
Choose one of the following scanners:

**Option A: Nmap**
```bash
# Ubuntu/Debian
sudo apt-get install nmap

# macOS
brew install nmap

# Windows
# Download from https://nmap.org/download.html
```

**Option B: OpenVAS**
```bash
# Ubuntu/Debian
sudo apt-get install openvas
sudo gvm-setup
```

### Step 5: Configure the System
```bash
cp config.example.yml config.yml
# Edit config.yml with your settings
```

## Configuration

### config.yml
```yaml
scanner:
  type: "nmap"  # Options: nmap, openvas, nessus
  scan_targets:
    - "192.168.1.0/24"
  scan_interval: "daily"  # Options: hourly, daily, weekly
  
alerting:
  email:
    enabled: true
    smtp_server: "smtp.gmail.com"
    smtp_port: 587
    sender: "your-email@gmail.com"
    recipients:
      - "admin@example.com"
    password: "your-app-password"
  
  severity_threshold: "medium"  # Options: low, medium, high, critical
  
logging:
  level: "INFO"  # Options: DEBUG, INFO, WARNING, ERROR
  file: "logs/scanner.log"
  retention_days: 90
  
database:
  type: "json"  # Options: json, sqlite, postgresql
  path: "data/vulnerabilities.json"
```

## Usage

### Running a Manual Scan
```bash
python scripts/vulnerability_scanner.py --target 192.168.1.0/24
```

### Starting the Automated Scheduler
```bash
python scripts/scheduler.py
```

### Viewing Results
```bash
# View latest scan results
python scripts/view_results.py --latest

# View historical data
python scripts/view_results.py --history --days 30

# Generate report
python scripts/generate_report.py --format pdf --output reports/
```

### Dashboard Access
```bash
# Start the web dashboard
python scripts/dashboard.py

# Access at http://localhost:5000
```

## Project Structure

```
vulnerability-scanner/
├── config.yml                    # Configuration file
├── requirements.txt              # Python dependencies
├── README.md                     # This file
├── LICENSE                       # License information
│
├── scripts/
│   ├── vulnerability_scanner.py  # Main scanner script
│   ├── scheduler.py              # Automated scheduling
│   ├── parser.py                 # Output parsing engine
│   ├── alerting.py               # Notification system
│   ├── dashboard.py              # Web dashboard
│   ├── view_results.py           # Results viewer
│   └── generate_report.py        # Report generator
│
├── data/
│   ├── vulnerabilities.json      # Historical vulnerability data
│   └── scan_results/             # Raw scan outputs
│
├── logs/
│   ├── scanner.log               # Application logs
│   └── test_results/             # Test execution logs
│
├── templates/
│   ├── email_alert.html          # Email notification template
│   └── dashboard.html            # Dashboard template
│
├── screenshots/
│   ├── scanner_execution.png
│   ├── scan_output.png
│   ├── parsing_results.png
│   ├── alert_notification.png
│   └── dashboard_view.png
│
├── tests/
│   ├── test_scanner.py
│   ├── test_parser.py
│   └── test_alerting.py
│
└── docs/
    ├── architecture.md
    ├── api_documentation.md
    └── troubleshooting.md
```

## Screenshots

### Scanner Execution
![Scanner Execution](screenshots/scanner_execution.png)
*Initial vulnerability scanner setup and configuration*

### Scan Output
![Scan Output](screenshots/scan_output.png)
*Real-time scan progress and vulnerability detection*

### Parsing Results
![Parsing Results](screenshots/parsing_results.png)
*Parsing engine extracting and classifying vulnerability data*

### Alert Notifications
![Alert Notification](screenshots/alert_notification.png)
*Email notification for critical vulnerabilities*

### Dashboard View
![Dashboard](screenshots/dashboard_view.png)
*Web dashboard showing vulnerability trends and statistics*

## Dependencies

### Core Dependencies
- `python-nmap==0.7.1` - Nmap scanner interface
- `requests==2.31.0` - HTTP requests for API interactions
- `pyyaml==6.0` - Configuration file parsing
- `schedule==1.2.0` - Job scheduling
- `flask==2.3.2` - Web dashboard framework
- `pandas==2.0.3` - Data analysis and manipulation
- `matplotlib==3.7.2` - Visualization and charts

### Email Dependencies
- `secure-smtplib==0.1.1` - Secure email sending

### Testing Dependencies
- `pytest==7.4.0` - Testing framework
- `pytest-cov==4.1.0` - Code coverage

Install all dependencies:
```bash
pip install -r requirements.txt
```

## Development Environment

### Recommended IDE Setup
- **Visual Studio Code** with extensions:
  - Python
  - Pylance
  - GitHub Copilot (optional)
  - Jupyter

### Virtual Machine Configuration
- **Operating System**: Ubuntu 24.04 LTS or Kali Linux
- **RAM**: Minimum 4GB, recommended 8GB
- **Storage**: 20GB minimum
- **Network**: Isolated network for testing (NAT or Host-Only)

### Version Control
This project uses Git for version control:
```bash
# Initialize Git (if not already done)
git init

# Add files
git add .

# Commit changes
git commit -m "Initial commit"

# Push to GitHub
git remote add origin https://github.com/[your-username]/vulnerability-scanner.git
git push -u origin main
```

## Testing

### Unit Tests
```bash
# Run all tests
pytest tests/

# Run with coverage
pytest --cov=scripts tests/

# Run specific test file
pytest tests/test_scanner.py
```

### Integration Tests
```bash
# Test full scan workflow
python tests/integration_test.py
```

### Test Environment
All tests are conducted in an isolated virtual machine environment to ensure:
- No impact on production systems
- Safe vulnerability testing
- Controlled network conditions

## Ethical Considerations

### Important Guidelines
⚠️ **Always obtain proper authorization before scanning any systems**

This tool is designed for:
- Authorized security assessments
- Personal learning environments
- Controlled lab testing
- Organizational security auditing with permission

### Responsible Use
1. **Authorization**: Only scan systems you own or have explicit permission to test
2. **Scope Limitation**: Define clear boundaries for your scans
3. **Data Protection**: Treat vulnerability data as confidential
4. **Legal Compliance**: Ensure compliance with local laws and regulations
5. **Isolated Testing**: Use virtual machines and isolated networks for development

### Security Best Practices
- Store credentials securely (use environment variables or secret managers)
- Limit access to vulnerability data
- Use encrypted communication channels
- Regularly update scanning tools and dependencies
- Follow responsible disclosure practices

## Time Management

This project was completed over an 8-week period with the following time allocation:

- **Week 1-2**: Planning and environment setup (15 hours)
- **Week 3-4**: Scanner implementation (20 hours)
- **Week 5-6**: Parsing and alert system (18 hours)
- **Week 7-8**: Testing and documentation (17 hours)

**Total**: 70 hours

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style
- Follow PEP 8 for Python code
- Use meaningful variable and function names
- Include docstrings for all functions and classes
- Add comments for complex logic

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Course instructors and teaching assistants
- Open-source community for tools and libraries
- Research papers that informed the project methodology
- AI tools (ChatGPT, GitHub Copilot) for development assistance

## Contact

**Student Name**: [Your Name]
**Email**: [your-email@example.com]
**GitHub**: [@your-username](https://github.com/your-username)
**Project Link**: [https://github.com/your-username/vulnerability-scanner](https://github.com/your-username/vulnerability-scanner)

## References

- Ogundairo, O., & Brooklyn, Peter. (2024). Automated Vulnerability Assessment Using Machine Learning. *Journal of Cyber Security*.
- Vemula, S. R. (2024). Automating Security Testing: Strategies for Vulnerability Scanning, Penetration Testing, and Compliance Checks. *International Research Journal of Engineering Science Technology and Innovation*.
- Verma, A., Singh, A. K., Shukla, D., Sharma, R., & Sheetal Laroiya. (2025). XploitGuard: Automated Vulnerability Scanning Tool. *International Journal of Research in Engineering, Science and Management*.

---

**Last Updated**: December 2024
**Version**: 1.0.0
