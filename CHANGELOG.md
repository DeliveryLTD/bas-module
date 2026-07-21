# Changelog

All notable changes to this project are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [1.0.3] - 2026-07-21

### Fixed
- Any HTTP 2xx status code (e.g. 203 behind transforming corporate proxies)
  is now treated as success — previously only 200 was accepted
  (object module request engine + inline cookie-login checks on managed forms).

### Added
- **"Діагностика конфігурації"** button on both settings forms: scans the
  configuration metadata (candidate documents with attributes and tabular
  sections, counterparty catalogs) and produces a report for support —
  speeds up adding official support for new configurations (e.g. BAS KUP).

## [1.0.2] - 2026-06-01

### Added
- In-processor version display — an **"Про програму"** window (version, copyright,
  support email, license) on both regular and managed forms.
- `ВерсияОбработки()` / `ТекстПроПрограмму()` in the object module — single source
  of truth for the version (kept in sync with the GitHub release).
- `.github/ISSUE_TEMPLATE/config.yml` — disables blank issues, links to SECURITY / SUPPORT.
- Latest-release badge in README.

### Changed
- README: fixed the platform badge (removed empty link), absolute links to releases.
- SUPPORT.md: Scope rendered as a list instead of a table.
- User guide: added a "do not publish secrets" warning next to Issues.

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
