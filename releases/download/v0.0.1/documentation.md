# NFGuard Documentation

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [System Requirements](#system-requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [CLI Usage](#cli-usage)
- [WebGUI Usage](#webgui-usage)
- [Geo-blocking](#geo-blocking)
- [API Reference](#api-reference)
- [Security](#security)
- [Troubleshooting](#troubleshooting)
- [Development](#development)
- [License](#license)

## Overview

NFGuard is an advanced firewall management tool that provides both Command Line Interface (CLI) and Web Graphical User Interface (WebGUI) for managing NFTables rules on Linux systems. It offers comprehensive firewall management with geo-blocking capabilities using MaxMind GeoLite2 database.

**Repository**: https://github.com/nfguard/nfguard
**Version**: v0.0.1
**Developer**: Lucas Catão de Moraes
**Website**: https://nfguard.org
**Company**: https://dolutech.com

## Features

### Core Features
- **Dual Interface**: Both CLI and WebGUI management
- **NFTables Integration**: Direct NFTables rule management
- **Real-time Monitoring**: Live logs and statistics
- **Rule Synchronization**: CLI and WebGUI stay in sync
- **Export/Import**: Configuration backup and restore

### Security Features
- **HTTPS Only**: Secure web interface (port 8443)
- **JWT Authentication**: Secure token-based authentication
- **Role-based Access**: Admin and viewer roles
- **Audit Logging**: Complete action tracking
- **bcrypt Password Hashing**: Secure password storage

### Geo-blocking Features
- **MaxMind GeoLite2**: Professional IP geolocation database
- **240+ Countries**: Comprehensive country coverage
- **Intelligent Caching**: Performance optimized lookups
- **Real-time IP Checking**: Instant country identification
- **Fallback Ranges**: Reliable operation even without database

### Management Features
- **Multi-user Support**: Multiple user accounts
- **Service Management**: systemd/OpenRC integration
- **Universal Installer**: Works on all major Linux distributions
- **Auto SSL Certificates**: Self-signed certificate generation
- **Log Rotation**: Automatic log management

## System Requirements

### Operating System
- Linux with NFTables support
- Supported distributions:
  - Ubuntu 18.04+
  - Debian 9+
  - CentOS/RHEL 7+
  - Fedora 28+
  - Arch Linux
  - OpenSUSE 15+
  - Alpine Linux 3.10+

### Hardware Requirements
- **CPU**: 1 core minimum, 2 cores recommended
- **RAM**: 512MB minimum, 1GB recommended
- **Storage**: 50MB for application, 500MB for logs
- **Network**: Port 8443 for WebGUI, Port 22 for SSH

### Software Dependencies (Auto-installed)
- NFTables
- Node.js 14+
- OpenSSL
- systemd or OpenRC

## Installation

### Quick Installation

1. **Download and Extract**:
```bash
wget https://github.com/nfguard/nfguard/raw/refs/heads/main/releases/download/v0.0.1/nfguard-0.0.1.tar.gz
tar -xzf nfguard-0.0.1.tar.gz
cd nfguard-0.0.1
```

2. **Run Installer**:
```bash
sudo bash install.sh
```

3. **Start Service**:
```bash
sudo systemctl start nfguard
sudo systemctl enable nfguard
```

4. **Access WebGUI**:
- URL: `https://your-server-ip:8443`
- Default credentials: `nfguard` / `nfguard`

### Manual Installation Steps

The installer performs these steps automatically:

1. **Detect Distribution**: Identifies your Linux distribution
2. **Install Dependencies**: Installs NFTables, Node.js, npm, OpenSSL
3. **Copy Files**: Installs to `/opt/nfguard`
4. **Install Node Modules**: Installs required npm packages
5. **Create Directories**: Sets up `/etc/nfguard`, `/var/log/nfguard`
6. **Setup Service**: Creates systemd/OpenRC service
7. **Configure Firewall**: Initializes basic NFTables rules
8. **Generate SSL**: Creates self-signed certificates
9. **Create CLI Link**: Links CLI to `/usr/local/bin/nfguard`

## Configuration

### File Locations

```
/opt/nfguard/                 # Application directory
├── src/                      # Source code
├── web/                      # WebGUI files
├── node_modules/             # Node.js dependencies
└── package.json              # Package information

/etc/nfguard/                 # Configuration directory
├── users.json                # User accounts
├── rules.json                # Firewall rules backup
├── geo-blocks.json           # Geo-blocking rules
├── nftables.conf             # NFTables configuration
├── .secret                   # JWT secret key
└── ssl/                      # SSL certificates
    ├── cert.pem
    └── key.pem

/var/log/nfguard/             # Log directory
├── app.log                   # Application logs
├── audit.log                 # Audit trail
├── service.log               # Service output
└── error.log                 # Error logs
```

### Default Credentials

- **Username**: `nfguard`
- **Password**: `nfguard`
- **Role**: `admin`

⚠️ **Important**: Change the default password immediately after installation!

### Service Configuration

```bash
# Service management
systemctl start nfguard       # Start service
systemctl stop nfguard        # Stop service
systemctl restart nfguard     # Restart service
systemctl status nfguard      # Check status
systemctl enable nfguard      # Enable auto-start
systemctl disable nfguard     # Disable auto-start

# View logs
journalctl -u nfguard -f      # Follow service logs
tail -f /var/log/nfguard/app.log  # Follow application logs
```

## CLI Usage

### Basic Commands

```bash
# Get help
nfguard --help
nfguard [command] --help

# Initialize NFTables
nfguard init

# View current rules
nfguard list
```

### Port Management

```bash
# Allow port (TCP by default)
nfguard allow -p 80
nfguard allow -p 443

# Allow UDP port
nfguard allow -p 53 -P udp

# Allow port from specific source
nfguard allow -p 22 -s 192.168.1.100

# Block port
nfguard block -p 8080
```

### IP/Network Management

```bash
# Block single IP
nfguard block -s 192.168.1.100

# Block network range
nfguard block -s 192.168.1.0/24

# Allow IP
nfguard allow -s 10.0.0.0/8

# Block destination
nfguard block -d 172.16.0.1
```

### Geo-blocking

```bash
# Block country
nfguard geo-block CN          # China
nfguard geo-block RU          # Russia
nfguard geo-block KP          # North Korea

# Unblock country
nfguard geo-unblock CN

# List blocked countries
nfguard geo-list

# Check IP location
nfguard check-ip 8.8.8.8
nfguard check-ip 1.1.1.1
```

### Configuration Management

```bash
# Export rules
nfguard export /backup/firewall.conf

# Import rules
nfguard import /backup/firewall.conf

# View statistics
nfguard stats

# Delete specific rule
nfguard delete RULE_ID

# Flush all rules (DANGEROUS!)
nfguard flush
```

## WebGUI Usage

### Accessing WebGUI

1. Open browser and navigate to: `https://your-server-ip:8443`
2. Accept the self-signed certificate warning
3. Login with credentials: `nfguard` / `nfguard`
4. Change default password in Settings

### Dashboard

The dashboard provides:
- **Real-time Statistics**: Active rules, blocked connections
- **Recent Activity**: Latest firewall actions
- **System Status**: Service health and uptime
- **Quick Actions**: Common firewall operations

### Rules Management

**Adding Rules**:
1. Click "Add Rule" button
2. Select rule type (Port, IP, Network)
3. Configure parameters
4. Set action (Allow/Block)
5. Click "Create Rule"

**Managing Rules**:
- **View**: All active rules displayed in table
- **Edit**: Click rule to modify parameters
- **Delete**: Remove unwanted rules
- **Export**: Download rules as configuration file

### Geo-blocking Interface

**Block Countries**:
1. Navigate to "Geo-blocking" tab
2. Select country from dropdown
3. Click "Block Country"
4. View blocked countries in table

**IP Lookup**:
1. Enter IP address in lookup field
2. View country, region, and block status
3. Optional: Block entire country

### User Management (Admin only)

**Add Users**:
1. Go to "Users" tab
2. Click "Add User"
3. Set username, password, role
4. Click "Create User"

**Manage Users**:
- **View**: List all users with roles
- **Edit**: Modify user permissions
- **Delete**: Remove user accounts
- **Reset**: Reset user passwords

### Logs and Monitoring

**Application Logs**:
- Real-time log viewer
- Filter by severity level
- Search functionality
- Export logs

**Audit Trail**:
- Track all user actions
- View timestamps and users
- Compliance reporting
- Security monitoring

## Geo-blocking

### MaxMind GeoLite2 Integration

NFGuard uses the MaxMind GeoLite2 Country database for accurate IP geolocation:

**Features**:
- **240+ Countries**: Comprehensive coverage
- **High Accuracy**: Professional-grade database
- **Regular Updates**: Database refreshed weekly
- **Local Lookup**: No external API calls required

**Supported Countries** (Examples):
- `CN` - China
- `RU` - Russia
- `US` - United States
- `BR` - Brazil
- `DE` - Germany
- `GB` - United Kingdom
- `FR` - France
- `JP` - Japan
- `IN` - India
- `KP` - North Korea
- `IR` - Iran

### How Geo-blocking Works

1. **IP Range Generation**:
   - System scans MaxMind database for country IP ranges
   - Generates CIDR blocks for entire countries
   - Caches results for 24 hours

2. **Rule Application**:
   - Each IP range becomes an NFTables rule
   - Rules are applied directly to kernel
   - Traffic matching ranges is dropped

3. **Fallback System**:
   - If MaxMind database unavailable, uses static ranges
   - Covers major countries with known IP blocks
   - Ensures continued operation

### IP Range Caching

- **Cache Location**: `/etc/nfguard/ip-lists/`
- **Cache Duration**: 24 hours
- **Cache Format**: JSON with metadata
- **Performance**: Sub-millisecond lookups

## API Reference

### Authentication Endpoints

```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "nfguard",
  "password": "nfguard"
}
```

Response:
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": "1",
    "username": "nfguard",
    "role": "admin"
  }
}
```

### Rule Management Endpoints

```http
# Get all rules
GET /api/rules
Authorization: Bearer <token>

# Add rule
POST /api/rules
Authorization: Bearer <token>
Content-Type: application/json

{
  "type": "port",
  "direction": "input",
  "protocol": "tcp",
  "port": "80",
  "action": "accept"
}

# Delete rule
DELETE /api/rules/:ruleId
Authorization: Bearer <token>
```

### Geo-blocking Endpoints

```http
# Block country
POST /api/geo/block
Authorization: Bearer <token>
Content-Type: application/json

{
  "countryCode": "CN"
}

# Unblock country
DELETE /api/geo/block/:countryCode
Authorization: Bearer <token>

# List blocked countries
GET /api/geo/blocked
Authorization: Bearer <token>

# Check IP
GET /api/geo/check/:ip
Authorization: Bearer <token>
```

### Monitoring Endpoints

```http
# Get statistics
GET /api/stats
Authorization: Bearer <token>

# Get logs
GET /api/logs?lines=100
Authorization: Bearer <token>

# Get audit logs
GET /api/logs/audit?lines=50
Authorization: Bearer <token>

# Health check
GET /api/health
```

## Security

### Authentication Security

- **JWT Tokens**: 24-hour expiration
- **bcrypt Hashing**: 10 rounds salt
- **Secure Sessions**: HTTPS-only cookies
- **Role-based Access**: Admin/viewer permissions

### File Security

- **Configuration Files**: 0600 permissions (root only)
- **SSL Certificates**: Properly secured
- **Log Files**: Protected access
- **Secret Keys**: Randomly generated

### Network Security

- **HTTPS Only**: No plain HTTP access
- **Self-signed Certificates**: Auto-generated
- **Firewall Protection**: NFTables integration
- **Audit Logging**: Complete action tracking

### Best Practices

1. **Change Default Password**: Immediately after installation
2. **Use Strong Passwords**: Minimum 12 characters
3. **Regular Backups**: Export configurations regularly
4. **Monitor Logs**: Review audit trails
5. **Update Regularly**: Keep system updated
6. **Limit Access**: Use geo-blocking for high-risk countries
7. **Network Segmentation**: Isolate management interface

## Troubleshooting

### Common Issues

**Service Won't Start**:
```bash
# Check service status
systemctl status nfguard

# Check logs
journalctl -u nfguard -n 50

# Check NFTables
nft list ruleset
```

**WebGUI Not Accessible**:
```bash
# Check if service is running
systemctl status nfguard

# Check if port is open
nft list ruleset | grep 8443

# Check SSL certificates
ls -la /etc/nfguard/ssl/
```

**CLI Commands Fail**:
```bash
# Check if nfguard is in PATH
which nfguard

# Check permissions
ls -la /usr/local/bin/nfguard

# Reinstall CLI link
sudo ln -sf /opt/nfguard/src/cli/index.js /usr/local/bin/nfguard
```

**Geo-blocking Not Working**:
```bash
# Check GeoLite database
ls -la /opt/nfguard/src/GeoLite/

# Test IP lookup
nfguard check-ip 8.8.8.8

# Check generated rules
nft list ruleset | grep GeoBlock
```

### Log Analysis

**Application Logs**:
```bash
tail -f /var/log/nfguard/app.log
```

**Audit Logs**:
```bash
tail -f /var/log/nfguard/audit.log
```

**Service Logs**:
```bash
journalctl -u nfguard -f
```

### Performance Tuning

**Memory Usage**:
- Normal usage: ~50MB RAM
- High traffic: ~100MB RAM
- Geo-blocking: Additional ~20MB for database

**CPU Usage**:
- Idle: <1% CPU
- Active: 2-5% CPU during rule changes
- Geo-blocking: Brief spikes during country blocks

## Development

### Building from Source

```bash
# Clone repository
git clone https://github.com/nfguard/nfguard.git
cd nfguard

# Install dependencies
npm install

# Run in development mode
npm run dev

# Build production package
./build.sh
```

### Project Structure

```
nfguard/
├── src/
│   ├── core/                 # Core functionality
│   │   ├── nftables-manager.js
│   │   ├── geo-blocker.js
│   │   └── logger.js
│   ├── auth/                 # Authentication
│   │   └── auth-manager.js
│   ├── cli/                  # Command line interface
│   │   └── index.js
│   ├── GeoLite/              # MaxMind database
│   │   └── GeoLite2-Country.mmdb
│   └── index.js              # Main server
├── web/                      # WebGUI files
│   ├── index.html
│   ├── app.js
│   └── styles.css
├── install.sh                # Installation script
├── build.sh                  # Build script
├── package.json              # Dependencies
└── Documentation.md          # This file
```

### Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Add tests
5. Submit pull request

### Testing

```bash
# Install development dependencies
npm install --dev

# Run tests
npm test

# Run linting
npm run lint

# Check code coverage
npm run coverage
```

## License

NFGuard is released under the MIT License.

```
MIT License

Copyright (c) 2025 Lucas Catão de Moraes

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

**Developed by**: Lucas Catão de Moraes
**Website**: https://nfguard.org
**Company**: https://dolutech.com
**Repository**: https://github.com/nfguard/nfguard
**Version**: v0.0.1

For support, bug reports, and feature requests, please visit our GitHub repository.
