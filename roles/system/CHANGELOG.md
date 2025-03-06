# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-03-06

### Added
- Initial version of the System role
- System information display functionality
- Hostname configuration capability
- Firewall management for iptables
- Kernel parameter optimization for high-performance servers
- Root user shell customization (PS1, grep colors)
- System limits configuration for open files and processes
- Essential administrative tools installation
- Detailed inline documentation for each task
- Comprehensive README with usage instructions
- Tagging system for selective task execution

### Changed
- Optimized task organization for better readability
- Improved variable handling with proper conditionals
- Enhanced apt package installation with comprehensive tool selection

### Fixed
- Proper permission management for root's .bashrc modifications
- Correct handling of system limits by removing default configuration files
- Graceful handling of iptables commands on systems where it might not be installed