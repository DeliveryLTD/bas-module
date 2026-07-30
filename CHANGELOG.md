# Changelog

All notable changes to this project are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [1.1.1] - 2026-07-31

### Added
- **Payer selection** ("Платник") on both create-waybill forms: sender or recipient.
  Previously the sender was always the payer with no way to change it. When the
  recipient pays, `payerType` is set to 1 and the payer id is omitted so the API
  resolves it from the recipient data. Defaults to sender, so existing behaviour
  is unchanged.

## [1.1.0] - 2026-07-30

### Added
- **Tariff type selection ("Тип тарифу") per cargo unit** on both create-waybill
  forms — regular cargo plus four pallet types (Euro pallet, Americana-1,
  Americana-2, half-pallet). Pallets are sent with `mainCategoryId: 75` as required
  by the Delivery API; regular cargo keeps the previous payload unchanged.
- **Weight limit validation for special tariffs.** Limits are fetched live from the
  API (`GetTariffCategory`) and fall back to a built-in table when the API is
  unreachable, so new limits are picked up automatically without updating the
  processor. The user gets a clear message instead of the backend silently
  substituting the weight — e.g. *"Для тарифу «Європалета» вага має бути не менше
  60 кг (вказано 11)"*. Applied both when creating and when calculating the price.
- **Date validation** on both create-waybill forms: the pickup date cannot be later
  than the dispatch date, and neither date can be in the past (same day is allowed).
  Checked both on submit and right after the date is entered, so the user is warned
  immediately.
- Cargo valuation field ("Оцінка вантажу") on the **regular** create-waybill form
  (previously only on the managed one). It now feeds `InsuranceValue` both when
  creating a waybill and when calculating the price, and is combined with the
  cash-on-delivery amount (the larger of the two is sent).

### Changed
- Error messages now include a hint when the API rejects the recipient: check the
  recipient's full name for typos and use the local phone format `0XXXXXXXXX`.

## [1.0.4] - 2026-07-23

### Added
- **Cargo valuation field** ("Оцінка вантажу") on the managed create-waybill form.
  It sets `InsuranceValue`, so insurance is now calculated correctly — previously
  the declared value was always sent as 0. Placed in a dedicated "Страхування"
  section, visually separated from the cash-on-delivery "Сума" field to avoid confusion.

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
