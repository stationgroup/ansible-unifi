# Change Log

## [1.6.0] - 2018-05-07
### Changed
- Add fqdn to /etc/hosts
- Open port 443 for Let's Encrypt TLS challenges (for renewals)
- Update unifi controller versions

## [1.5.0] - 2018-03-31
### Changed
- Disable chatty firewall logging

## [1.4.0] - 2018-03-31
### Changed
- Updated unifi controller on unifi-beta-01 to version 5.8.10

## [1.3.0] - 2018-03-25
### Changed
- Reverted public IPs of hosts in the field since they were incompatible with STUN.

## [1.2.0] - 2018-03-23
### Changed
- Updated DNS check to only run if we are generating initial certificate.
- Updated public IPs of hosts in the field.

## [1.1.0] - 2018-03-23
### Changed
- Reworked Let's Encrypt to use `deploy_hook` and built-in renewal functionality,
  rather than our own cronjob and full-fledged renewal script.

## [1.0.0] - 2018-03-22
### Added
- Initial commit to public github with encrypted secrets
