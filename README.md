# Delivery Connect for BAS

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Platform: BAF / 1C 8.3](https://img.shields.io/badge/Platform-BAF%20%7C%201C%208.3-yellow.svg)]()
[![Delivery Auto API](https://img.shields.io/badge/API-Delivery%20Auto%20v4-black.svg)](https://delivery-auto.com.ua)

> Інтеграція облікових систем **BAS / BAF / 1С:Підприємство** з API служби доставки **Delivery Auto** — оформлення, розрахунок і відстеження доставок прямо з вашої облікової системи.
>
> Integration of **BAS / BAF / 1C:Enterprise** accounting systems with the **Delivery Auto** shipping API — create, calculate and track shipments right from your accounting software.

**🇺🇦 [Українська](#-українська)** | **🇬🇧 [English](#-english)**

---

## 🇺🇦 Українська

### Що це

Зовнішня обробка (`.epf`) для конфігурацій на платформі BAF / 1С:Підприємство 8.3, яка підключає вашу облікову систему до API служби доставки [Delivery Auto](https://delivery-auto.com.ua). Оформлюйте квитанції, рахуйте вартість, друкуйте документи, викликайте кур'єра — без переходу в особистий кабінет.

### Можливості

| | Функція |
|---|---|
| 🔍 | **Пошук квитанції** за номером з деталями |
| 📋 | **Реєстр квитанцій** — завантаження з API, деталі по подвійному кліку |
| 📦 | **Створення квитанції** — усі 4 схеми доставки (Склад-Склад, Двері-Двері, Склад-Двері, Двері-Склад) |
| 🧮 | **Розрахунок вартості** перед оформленням |
| 🖨 | **Друк** квитанції та стікерів (PDF) |
| 🔒 | **Заборона видачі** + зняття через SMS-код |
| 🚚 | **Виклик кур'єра** — заявка на забір вантажу |
| 🔗 | **Інтеграція з документами 1С** — оформлення квитанції на підставі реалізації / рахунку |
| ⚙️ | **Налаштування** з перевіркою з'єднання |
| 🚛 | **Накладений платіж** (розрахунковий рахунок) |

### Підтримувані конфігурації

- **БАС Управління торговим підприємством 1.2** — звичайні форми (режим звичайного застосунку)
- **БАС Бухгалтерія 2.1** — керовані форми (режим керованого застосунку)
- Адаптивна архітектура: імена документів-підстав налаштовуються під різні конфігурації
- **Платформи:** BAF 8.3.19+, 1С:Підприємство 8.3.x

> Універсальна `.epf` містить **обидва набори форм** — платформа автоматично обирає потрібні залежно від режиму застосунку.

### Технічні особливості

- **HMAC-SHA1** авторизація — чиста реалізація мовою 1С, **без зовнішніх компонент (.dll/.so)**
- **Cookie-авторизація** (`.ASPXAUTH`) для методів особистого кабінету
- Робота через `ЗащищенноеСоединениеOpenSSL` (HTTPS)
- Жовто-чорний корпоративний стиль Delivery

### Вимоги

- **Платформа:** BAF 8.3.19+ або 1С:Підприємство 8.3.x
- **З'єднання:** доступ до інтернету через HTTPS (OpenSSL)
- **Доступ:** право запуску зовнішніх обробок у вашій базі
- **Обліковий запис Delivery Auto:** логін/пароль кабінету + API-ключ і секретний ключ

### Встановлення

1. Завантажте `DeliveryConnect-BAS.epf` з [релізів](../../releases) або репозиторію
2. У вашій БАС/1С: **Файл → Відкрити** → оберіть `DeliveryConnect-BAS.epf`
3. Натисніть **Налаштування** → введіть **API-ключ** і **секретний ключ** (отримати в [особистому кабінеті Delivery Auto](https://delivery-auto.com.ua)), а також логін/пароль кабінету
4. **Перевірити з'єднання** — має показати ваше ім'я та ID клієнта
5. Готово — оформлюйте квитанції 🚚

📖 **Детальна інструкція користувача:** [docs/Інструкція_користувача.md](docs/Інструкція_користувача.md)

### Обмеження

- Протестовано на вказаних конфігураціях (БАС УТП 1.2, БАС Бухгалтерія 2.1). Для **суттєво доопрацьованих** баз може знадобитися адаптація імен документів-підстав.
- Накладений платіж — лише тип «розрахунковий рахунок».

### ⚠️ Безпека

API-ключі, секретний ключ і пароль зберігаються в `ХранилищеОбщихНастроек` — **спільному сховищі бази даних**. Будь-який користувач із правом запуску зовнішніх обробок може їх прочитати.

**Це прийнятно** за умови спільних ключів компанії та довірених співробітників. Для **суворих середовищ**:
- обмежте доступ до обробки ролями, **АБО**
- замініть `ХранилищеОбщихНастроек` на `ХранилищеНастроекПользователя` у функції `ПрочитатьНастройки()` модуля об'єкта (єдина точка зміни) та в `СохранитьНастройки()`.

> 📋 Політика безпеки та звітування про вразливості — [SECURITY.md](SECURITY.md).

### Підтримка

Офіційні релізи супроводжує IT-команда Delivery Auto. Канали зв'язку та межі підтримки (зокрема best-effort для форків) — у [SUPPORT.md](SUPPORT.md).

### Кастомізація

Код повністю відкритий — `.epf` відкривається в конфігураторі, дивіться/правте будь-який модуль. Офіційну версію підтримує Delivery Auto; ваші форки — на ваш розсуд (ліцензія Apache 2.0 дозволяє).

### Ліцензія

[Apache License 2.0](LICENSE) — вільне використання, модифікація та розповсюдження.

---

## 🇬🇧 English

### What is this

An external data processor (`.epf`) for the BAF / 1C:Enterprise 8.3 platform that connects your accounting system to the [Delivery Auto](https://delivery-auto.com.ua) shipping API. Create waybills, calculate costs, print documents, and call a courier — without switching to the web cabinet.

### Features

| | Feature |
|---|---|
| 🔍 | **Search waybill** by number with details |
| 📋 | **Waybill registry** — load from API, details on double-click |
| 📦 | **Create waybill** — all 4 delivery schemes (Warehouse-Warehouse, Door-Door, Warehouse-Door, Door-Warehouse) |
| 🧮 | **Cost calculation** before creating |
| 🖨 | **Printing** of waybills and stickers (PDF) |
| 🔒 | **Delivery hold** + removal via SMS code |
| 🚚 | **Call a courier** — cargo pickup request |
| 🔗 | **1C document integration** — create a waybill based on a sales/invoice document |
| ⚙️ | **Settings** with connection check |
| 🚛 | **Cash on delivery** (bank account) |

### Supported configurations

- **BAS Trade Management 1.2** — regular forms (ordinary application mode)
- **BAS Accounting 2.1** — managed forms (managed application mode)
- Adaptive architecture: source-document names are configurable for different setups
- **Platforms:** BAF 8.3.19+, 1C:Enterprise 8.3.x

> The universal `.epf` contains **both form sets** — the platform automatically picks the right one based on application mode.

### Technical highlights

- **HMAC-SHA1** authentication — pure 1C implementation, **no external components (.dll/.so)**
- **Cookie authentication** (`.ASPXAUTH`) for personal-cabinet methods
- Works over `OpenSSL secure connection` (HTTPS)
- Delivery yellow-and-black corporate styling

### Requirements

- **Platform:** BAF 8.3.19+ or 1C:Enterprise 8.3.x
- **Connection:** internet access over HTTPS (OpenSSL)
- **Access:** the right to run external data processors in your database
- **Delivery Auto account:** cabinet login/password + API key and secret key

### Installation

1. Download `DeliveryConnect-BAS.epf` from [releases](../../releases) or the repository
2. In your BAS/1C: **File → Open** → select `DeliveryConnect-BAS.epf`
3. Click **Settings** → enter your **API key** and **secret key** (get them in the [Delivery Auto cabinet](https://delivery-auto.com.ua)), plus cabinet login/password
4. **Check connection** — it should show your name and client ID
5. Done — start creating waybills 🚚

### Limitations

- Tested on the listed configurations (BAS Trade Management 1.2, BAS Accounting 2.1). **Heavily customized** databases may require adapting the source-document names.
- Cash on delivery — bank-account type only.

### ⚠️ Security

API keys, secret key and password are stored in `CommonSettingsStorage` — a **shared database storage**. Any user with the right to run external processors can read them.

**This is acceptable** with shared company keys and trusted employees. For **strict environments**:
- restrict access to the processor via roles, **OR**
- replace `CommonSettingsStorage` with `UserSettingsStorage` in the `ПрочитатьНастройки()` (ReadSettings) function of the object module (single point of change) and in `СохранитьНастройки()` (SaveSettings).

> 📋 Security & vulnerability-reporting policy — [SECURITY.md](SECURITY.md).

### Support

Official releases are maintained by the Delivery Auto IT team. Support channels and scope (including best-effort for forks) — see [SUPPORT.md](SUPPORT.md).

### Customization

The code is fully open — the `.epf` opens in the Designer, view/edit any module. The official version is maintained by Delivery Auto; your forks are up to you (Apache 2.0 permits it).

### License

[Apache License 2.0](LICENSE) — free to use, modify and distribute.

---

<p align="center">
  Made with 💛🖤 for <a href="https://delivery-auto.com.ua">Delivery Auto</a> logistics partners
</p>
