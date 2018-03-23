# Change Log

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
