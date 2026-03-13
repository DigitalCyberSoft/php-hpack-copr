# PHP-HPACK COPR Build Repository

Automated COPR build configuration for [php-hpack](https://github.com/DigitalCyberSoft/php-hpack) - PHP extension for HPACK header compression (RFC 7541).

## Overview

This repository contains the COPR build configuration to automatically build RPM packages for the PHP HPACK extension from GitHub releases.

## Features

- **Automated Builds**: Builds directly from php-hpack GitHub releases
- **PHP Version Support**: Builds for the system PHP version (8.0+)
- **NTS and ZTS Support**: Builds both non-thread-safe and thread-safe variants
- **Test Suite**: Runs upstream test suite during build

## COPR Repository

The built packages are available in COPR at:
```
https://copr.fedorainfracloud.org/coprs/reversejames/php-hpack/
```

### Installation

```bash
# Enable the COPR repository
sudo dnf copr enable reversejames/php-hpack

# Install php-hpack
sudo dnf install php-hpack

# For development headers
sudo dnf install php-hpack-devel

# Restart PHP-FPM if using it
sudo systemctl restart php-fpm
```

## Configuration

The extension is configured via `/etc/php.d/40-hpack.ini`:
```ini
; Enable hpack extension module
extension = hpack.so
```

## Verification

```bash
php -m | grep hpack
php -i | grep hpack
```

## Build Process

1. Downloads the php-hpack source from GitHub release tag
2. Validates version against `php_hpack.h`
3. Generates RPM spec file dynamically
4. Builds SRPM for COPR

## Local Testing

```bash
cd .copr
make srpm
```

## Dependencies

- **Build**: gcc, make, php-devel (>= 8.0), libnghttp2-devel
- **Runtime**: php, libnghttp2

## Extension Features

- HPACK header compression/decompression (RFC 7541)
- HPackContext class with dynamic table management
- Standalone Huffman encode/decode functions
- Automatic sensitive header protection (authorization, cookie, etc.)

## License

The build configuration is provided as-is. php-hpack is licensed under the MIT License.

## Upstream

- php-hpack GitHub: https://github.com/DigitalCyberSoft/php-hpack
- RFC 7541 (HPACK): https://www.rfc-editor.org/rfc/rfc7541
- libnghttp2: https://nghttp2.org/
