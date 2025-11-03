# Zeus Web Scanner

A comprehensive web vulnerability scanner that combines Google dorking, web spidering, and multiple security scanning capabilities into one powerful tool.

## Overview

Zeus (Web_Scanner) is an advanced security reconnaissance tool designed to discover and assess web vulnerabilities. It automates the process of finding potential security weaknesses through Google dorking, URL enumeration, and various attack vectors including SQL injection, XSS, port scanning, and more.

## Features

###  Discovery Methods
- **Google Dorking**: Search using custom or predefined dorks
- **Web Spidering**: Crawl websites to discover all available URLs
- **Batch Scanning**: Process multiple dorks or URLs from files
- **Multiple Search Engines**: Support for Google, DuckDuckGo, Bing, and AOL

###  Security Scans
- **SQL Injection (SQLi)**: Integration with SQLmap for automated SQLi detection
- **Cross-Site Scripting (XSS)**: XSS vulnerability scanning with payload tampering
- **Port Scanning**: Nmap integration for network reconnaissance  
- **Admin Panel Finder**: Automated admin panel discovery
- **Clickjacking Detection**: Tests for clickjacking vulnerabilities
- **WHOIS Lookup**: Domain registration information gathering
- **PGP Key Lookup**: Search for public PGP keys
- **WAF/IDS/IPS Detection**: Identify protective mechanisms
- **Plugin Detection**: Discover installed web plugins

###  Anonymity & Stealth
- **Proxy Support**: Single proxy or random proxy from file
- **Tor Integration**: Route traffic through Tor network
- **Custom User-Agents**: Random or custom user-agent strings
- **X-Forwarded-For Headers**: Add randomized forwarding headers

## Installation

### Prerequisites
- Python 2.7+ or Python 3.x
- Firefox browser
- GeckoDriver
- Nmap
- SQLmap

### Using Docker (Recommended)

```bash
docker build -t zeus-scanner .
docker run -it zeus-scanner python zeus.py --help
```

### Manual Installation

```bash
# Clone repository
git clone <repository-url>
cd Web_Scanner

# Install dependencies
pip install -r requirements.txt

# Install system dependencies
sudo apt-get update
sudo apt-get install -y nmap sqlmap firefox geckodriver xvfb
```

## Usage

### Basic Syntax
```bash
python zeus.py -d|r|l|f|b DORK|FILE|URL [ATTACKS] [--OPTS]
```

### Examples

#### 1. Single Dork with SQLi Scan
```bash
python zeus.py -d "inurl:admin.php" -s --batch
```

#### 2. Random Dork with Multiple Attacks
```bash
python zeus.py -r -s -x -p --verbose
```

#### 3. Spider Website and Run All Scans
```bash
python zeus.py -b https://example.com -s -x -p -a -w
```

#### 4. Batch Scan from Dork File
```bash
python zeus.py -l /path/to/dorks.txt -s -x --batch
```

#### 5. URL File with Proxy and Random Agent
```bash
python zeus.py -f urls.txt -s --proxy socks5://127.0.0.1:9050 --random-agent
```

#### 6. Multi-page Google Search
```bash
python zeus.py -d "inurl:login" -M -L 100 -s -x
```

#### 7. Using Tor with Verbose Output
```bash
python zeus.py -r -s -x --tor --verbose
```

## Command Reference

### Mandatory Options (Choose One)
| Option | Description |
|--------|-------------|
| `-d DORK` | Single Google dork query |
| `-l FILE` | File containing multiple dorks |
| `-r` | Use random dork from etc/dorks.txt |
| `-b URL` | Spider a single webpage |
| `-f FILE` | File containing URLs to scan |

### Attack Options
| Option | Description |
|--------|-------------|
| `-s, --sqli` | SQL injection scan (SQLmap) |
| `-p, --port-scan` | Port scan (Nmap) |
| `-a, --admin-panel` | Admin panel finder |
| `-x, --xss-scan` | XSS vulnerability scan |
| `-w, --whois-lookup` | WHOIS domain lookup |
| `-c, --clickjacking` | Clickjacking vulnerability test |
| `-P, --pgp` | PGP public key lookup |

### Advanced Attack Arguments
| Option | Description |
|--------|-------------|
| `--sqlmap-args` | Custom SQLmap arguments (comma-separated) |
| `--sqlmap-conf` | SQLmap configuration file |
| `--nmap-args` | Custom Nmap arguments (pipe-separated) |
| `--tamper` | XSS payload tampering script |
| `--auto` | Auto-start SQLmap API |
| `--show-possibles` | Show all admin panel connections |

### Search Options
| Option | Description |
|--------|-------------|
| `-M, --multi` | Search multiple Google pages |
| `-L NUM` | Number of links to search |
| `-E, --exclude-none` | Include URLs without GET parameters |
| `-W, --webcache` | Parse webcache redirect URLs |
| `--x-forward` | Add X-Forwarded-For header |
| `--time-sec` | Control timeout durations |
| `--identify-waf` | Detect WAF/IDS/IPS |
| `--identify-plugins` | Detect installed plugins |

### Anonymity Options
| Option | Description |
|--------|-------------|
| `--proxy` | Single proxy (e.g., socks5://127.0.0.1:9050) |
| `--proxy-file` | File with multiple proxies (random selection) |
| `--random-agent` | Random user-agent from etc/agents.txt |
| `--agent` | Custom user-agent string |
| `--tor` | Use Tor network |

### Search Engine Options
| Option | Description |
|--------|-------------|
| `-D, --search-engine-ddg` | Use DuckDuckGo |
| `-B, --search-engine-bing` | Use Bing |
| `-A, --search-engine-aol` | Use AOL |

### Miscellaneous
| Option | Description |
|--------|-------------|
| `--verbose` | Verbose output mode |
| `--batch` | Skip prompts (batch mode) |
| `--hide` | Hide banner |
| `--version` | Show version |
| `--show-success` | Calculate dork success rate |

## Project Structure

```
Web_Scanner/
├── zeus.py                 # Main entry point
├── requirements.txt        # Python dependencies
├── Dockerfile             # Docker configuration
├── bin/                   # Utility scripts
├── lib/                   # Core libraries
│   ├── attacks/          # Attack modules (SQLi, XSS, Nmap, etc.)
│   ├── core/             # Core functionality
│   ├── plugins/          # Plugin detection modules
│   └── header_check.py   # HTTP header analysis
├── var/                   # Variable data
│   ├── blackwidow/       # Web spider
│   ├── search/           # Search engine integration
│   └── auto_issue/       # Issue reporting
└── etc/                   # Configuration files
    ├── dorks.txt         # Predefined dorks
    ├── agents.txt        # User-agent strings
    ├── scripts/          # Helper scripts
    └── text_files/       # Additional resources
```

## Dependencies

See `requirements.txt` for complete list:
- beautifulsoup4 - HTML parsing
- selenium - Browser automation
- requests - HTTP library
- python-nmap - Nmap integration
- lxml - XML/HTML processing
- colorama - Colored terminal output
- And more...

## Output

Zeus saves all results to log files:
- **URL logs**: `var/logs/url-log/`
- **Spider logs**: `var/logs/spider-log/`
- **Current session**: `var/logs/zeus-current-log.log`

## Legal Disclaimer

 **WARNING**: This tool is for educational and authorized penetration testing purposes only.

- Only use on systems you own or have explicit permission to test
- Unauthorized scanning is illegal in most jurisdictions
- The authors assume no liability for misuse or damage
- Always comply with applicable laws and regulations

## Security Notice

- Use strong proxies/VPNs when scanning
- Rate-limit your requests to avoid detection
- Respect robots.txt and website policies
- Be aware that scanning can be detected and logged

## Troubleshooting

### Common Issues

**GeckoDriver version mismatch:**
```bash
# Update GeckoDriver to match Firefox version
# Check compatibility: https://github.com/mozilla/geckodriver/releases
```

**Max retries exceeded:**
```bash
# Use proxy and change user-agent
python zeus.py -r -s --proxy http://proxy:port --random-agent
```

**Permission denied:**
```bash
# Run with sudo if needed
sudo python zeus.py -r -s
```

**Tor connection issues:**
```bash
# Ensure Tor is running
sudo service tor start
# Verify SOCKS proxy on 127.0.0.1:9050
```

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

Please refer to the LICENSE file in the repository.

## Credits

Zeus is a fork/continuation of zeus-scanner by ekultek. This tool integrates multiple open-source security tools including SQLmap and Nmap.

## Support

For issues, bugs, or feature requests, please use the built-in issue creation feature or submit through the repository's issue tracker.

---

**Remember**: With great power comes great responsibility. Use Zeus ethically and legally.

Real Tool Link -: https://github.com/Ekultek/Zeus-Scanner.git
Credit To -: Ekultek
