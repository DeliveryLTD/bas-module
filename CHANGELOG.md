# Changelog

All notable changes to this project are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [1.0.1] - 2026-05-31

### Changed
- Unified the processor file name everywhere to `DeliveryConnect-BAS.epf`
  (README, release, documentation, repository).

### Added
- `SECURITY.md` — security reporting policy.
- `SUPPORT.md` — support channels and scope.
- `CONTRIBUTING.md` — contribution guidelines.
- `NOTICE` — Apache 2.0 attribution notice.
- Issue templates (bug report, feature request).
- **Requirements** and **Limitations** sections in the README.
- Ukrainian user guide (`docs/`).

## [1.0.0] - 2026-05-31

### Added
- First public release.
- Support for regular and managed forms.
- Waybill search and registry.
- Waybill creation for 4 delivery schemes
  (Warehouse-Warehouse, Door-Door, Warehouse-Door, Door-Warehouse).
- Cost calculation before creating a waybill.
- PDF printing for waybills and stickers.
- Delivery hold and removal via SMS code.
- Courier pickup request.
- 1C / BAS document integration (waybill based on a sales / invoice document).
- Cash on delivery with bank account.
