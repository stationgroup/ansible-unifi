# Change Log

## [2.0.0] - 2018-06-30
### Changed
- Reorganized to more closely follow Ansible conventions
- Update beta and prod controllers to 5.8.24
- Put controllers behind nginx

## [1.8.0] - 2018-05-28
### Changed
- Update unifi controller on unifi-beta-01 to version 5.8.19
- Update unifi controller on unifi-prod-01 to version 5.7.28

## [1.7.0] - 2018-05-11
### Changed
- Update unifi controller on unifi-beta-01 to version 5.8.16

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
