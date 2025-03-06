# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-03-06

### Added
- Initial version of the PostgreSQL role
- Support for Ubuntu 22.04 and 24.04 with compatible repository key handling
- Installation of PostgreSQL server with configurable version
- PostGIS 3 extension setup and configuration
- Custom data directory configuration with proper permissions
- Master-replica replication setup with automated initialization
- Secure repository key handling for modern Ubuntu versions
- Configuration customization for network access and security
- Complete documentation in README.md format (English and Russian)
- Tags for selective execution of master or replica tasks

### Changed
- Optimized installation process for better idempotence
- Consolidated PostgreSQL configuration tasks
- Improved directory structure with appropriate permissions

### Fixed
- Ubuntu 24.04 compatibility issues with APT repository signing keys
- Proper service management for database initialization
- Correct symlink creation for custom data directories