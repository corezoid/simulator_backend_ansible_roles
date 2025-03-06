# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-03-06

### Added
- Initial version of the ScyllaDB role
- Support for ScyllaDB versions 5.4 and 6.2
- Automatic installation from the official ScyllaDB repository
- Configuration of optimized database settings
- Ability to add and configure an additional disk for data
- Automatic data migration when setting up a new disk (AWS ec2 only)
- Installation and configuration of Java JRE for ScyllaDB operation
- Optimization of system parameters for ScyllaDB operation
- Configuration of automatic startup on system boot


### Configured
- Optimized ScyllaDB parameters for high performance
- Automatic detection of the first IP address for configuration
- Proper permissions and ownership for ScyllaDB files and directories
