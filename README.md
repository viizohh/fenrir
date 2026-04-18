# Fenrir - Network Traffic Analyzer

A network security scanner with AI-powered threat analysis that monitors and analyzes network traffic in real-time.

## Features

- **Live Traffic Capture**: Monitor network traffic in real-time on any interface
- **PCAP Analysis**: Analyze saved packet capture files
- **AI-Powered Security Analysis**: Intelligent threat detection using Claude API
- **Sensitive Data Detection**: Detect passwords, credit cards, API keys, and other sensitive data in cleartext
- **Protocol Parsing**: Extract information from DNS, HTTP/HTTPS, and TCP packets
- **Device Tracking**: Monitor all devices on your network
- **Connection Tracking**: Track TCP connections and data transfer
- **Behavior Detection**:
  - Beaconing detection (periodic automated communication)
  - Tracking detection (third-party tracking cookies)
  - Anomaly detection (DGA domains, port scanning, etc.)
- **Session Tracking**: Track website browsing sessions with context
- **Organized Analysis Output**: JSON data, Markdown reports, and text summaries

## Installation

```bash
cd fenrir
pip install -e .
```

Or using a virtual environment (recommended):

```bash
cd fenrir
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pip install -e .
```

## Usage

Start the interactive shell:

```bash
sudo fenrir
```

### Available Commands

Once in the Fenrir shell, use these commands:

**Sniff live traffic with AI analysis:**
```bash
fenrir> sniff live --iface en0 --ai --count 200
```

**Analyze PCAP file with AI:**
```bash
fenrir> sniff pcap capture.pcap --ai
```

**Monitor all traffic:**
```bash
fenrir> sniff live --iface en0 --show-all
```

**Filter for specific device:**
```bash
fenrir> sniff live --iface en0 --device 10.0.0.89
```

### Options

- `--iface TEXT`: Network interface (required for live capture)
- `--device TEXT`: Filter for specific device IP
- `--count NUMBER`: Capture N packets then stop (e.g., --count 200)
- `--show-all`: Show ALL traffic (like Wireshark)
- `--alerts-only`: Only show warnings and alerts
- `--verbose`: Show detailed information
- `--ai`: Enable AI analysis (requires ANTHROPIC_API_KEY)

### AI Analysis

To use AI-powered threat analysis, set your Anthropic API key:

```bash
export ANTHROPIC_API_KEY='your-api-key-here'
```

Then run Fenrir with the `--ai` flag:

```bash
sudo fenrir
fenrir> sniff live --iface en0 --ai --count 200
```

Results are saved to `./analysis/`:
- `raw_data/` - JSON scan data
- `reports/` - Full Markdown analysis reports
- `summaries/` - Quick text summaries

See [ANALYSIS_FOLDER_GUIDE.md](ANALYSIS_FOLDER_GUIDE.md) for details.

## Requirements

- Python 3.8+
- scapy >= 2.5.0
- click >= 8.1.0
- colorama >= 0.4.6
- tabulate >= 0.9.0
- python-dateutil >= 2.8.2
- anthropic >= 0.18.0

## Permissions

Network packet capture requires elevated privileges:

- **macOS**: Run with `sudo`
- **Linux**: Run with `sudo` or grant capabilities to Python
- **Windows**: Run as Administrator

## Example

```bash
$ sudo fenrir
     ___           ___           ___           ___                       ___
    /\__\         /\__\         /\  \         /\  \                     /\  \
   /:/ _/_       /:/ _/_        \:\  \       /::\  \       ___         /::\  \
  /:/ /\__\     /:/ /\__\        \:\  \     /:/\:\__\     /\__\       /:/\:\__\
 /:/ /:/  /    /:/ /:/ _/_   _____\:\  \   /:/ /:/  /    /:/__/      /:/ /:/  /
/:/_/:/  /    /:/_/:/ /\__\ /::::::::\__\ /:/_/:/__/___ /::\  \     /:/_/:/__/___
\:\/:/  /     \:\/:/ /:/  / \:\~~\~~\/__/ \:\/:::::/  / \/\:\  \__  \:\/:::::/  /
 \::/__/       \::/_/:/  /   \:\  \        \::/~~/~~~~   ~~\:\/\__\  \::/~~/~~~~
  \:\  \        \:\/:/  /     \:\  \        \:\~~\          \::/  /   \:\~~\
   \:\__\        \::/  /       \:\__\        \:\__\         /:/  /     \:\__\
    \/__/         \/__/         \/__/         \/__/         \/__/       \/__/

Welcome to Fenrir - Network Security Scanner
Type 'help' to see available commands

fenrir> sniff live --iface en0 --ai --count 200
# Start monitoring and analyzing network traffic...
```

## License

See LICENSE file for details.
