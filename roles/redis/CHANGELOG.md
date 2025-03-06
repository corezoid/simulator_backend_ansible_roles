# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-03-06

### Added
- Initial version of the Redis role
- Support for both Ubuntu 22.04 (Jammy) and Ubuntu 24.04 (Noble)
- Automatic detection of Ubuntu version and package selection
- Installation of Redis from official Redis repository
- Configuration file generation based on template
- Setup of automatic service startup with systemd
- Addition of monitoring through Monit
- Complete documentation in README.md format
- Support for Redis version 7.4.2
- Fallback mechanism for installation if specific version fails

### Changed
- Consolidated repository management tasks for better maintainability
- Optimized GPG key handling

### Fixed
- Reliable service auto-start configuration with systemd
- Proper handling of package version suffixes for different Ubuntu releases