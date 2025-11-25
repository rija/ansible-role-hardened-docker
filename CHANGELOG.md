## [Unreleased]

### Added

- Docs #15: Add a CODE_OF_CONDUCT.md document from contributor covenant template 
- Fix #5: Use openssl-req instead of openssl-x509 to create CA cert to support RedHat
- Fix #9: Test the TLS based TCP connection to Docker
- Feat #8: The role will delete redundant intermediary files
- Feat #4: Add user documentation
- Fix #3: Remove formatting warnings from Yaml Lint
- Fix #6: Remove formatting warnings from Ansible Lint
- Feat #2: Add integration test using Ansible molecule
- Feat #1: Check that docker and systemd are present
- Generate certificates for client-certificate authenticated TCP connection to docker daemon
- (CI) Secret detection to project
- (CI) run yamllint and ansible-lint in Gitlab pipeline in a linting job
