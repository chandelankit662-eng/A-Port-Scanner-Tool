# Port Scanner Tool

A fast, multi-threaded TCP port scanner written in Python. Scans a target host over a given port range (or list), reports which ports are open, identifies common services, and can optionally grab service banners.

> ⚠️ **Only scan hosts you own or have explicit permission to test.** Unauthorized port scanning may violate laws or terms of service in your jurisdiction.

## Features
- Multi-threaded scanning (configurable thread count) for speed
- Accepts single ports, ranges, or comma-separated lists (`22,80,443` or `1-1024`)
- Resolves hostnames to IPs automatically
- Identifies well-known services by port number
- Optional banner grabbing on open ports
- JSON export of results
- Progress indicator during scan

## Requirements
- Python 3.7+
- No external dependencies (uses only the standard library)

## Usage

```bash
# Scan the default range (1-1024) on a host
python port_scanner.py -t example.com

# Scan a specific range
python port_scanner.py -t 192.168.1.1 -p 1-65535

# Scan specific ports
python port_scanner.py -t example.com -p 22,80,443,8080

# Increase thread count for faster scans
python port_scanner.py -t example.com -p 1-65535 --threads 300

# Grab service banners on open ports
python port_scanner.py -t example.com -p 1-1024 --banner

# Save results to a JSON file
python port_scanner.py -t example.com -p 1-1024 -o results.json
```

## Arguments

| Flag             | Description                                      | Default   |
|------------------|---------------------------------------------------|-----------|
| `-t, --target`   | Target hostname or IP address (required)         | —         |
| `-p, --ports`    | Ports to scan: single, range, or comma list       | `1-1024`  |
| `--threads`      | Number of concurrent threads                      | `100`     |
| `--timeout`      | Socket timeout in seconds                          | `1.0`     |
| `--banner`       | Attempt banner grabbing on open ports             | off       |
| `-o, --output`   | Path to save results as JSON                       | none      |

## Example Output

```
[*] Target       : example.com (93.184.216.34)
[*] Ports        : 1024 port(s) [1-1024]
[*] Threads      : 100
[*] Banner grab  : off
[*] Started at   : 2026-07-14 10:23:36
--------------------------------------------------
[+] Found 2 open port(s):

PORT    SERVICE        BANNER
80      HTTP           -
443     HTTPS          -

[*] Scan completed in 3.42 seconds
```

## Possible Extensions (good first issues!)
- UDP port scanning
- OS fingerprinting
- Export results to CSV/HTML report
- Add a `--stealth` mode using SYN scans (requires raw sockets / root)
- GUI or web dashboard front-end
- Integration with CVE lookups based on detected service/version

## Contributing
See the main repo README for the fork → branch → PR workflow used across CyberSecurity-IIITA projects.
