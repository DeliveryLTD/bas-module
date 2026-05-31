# Security Policy

## Reporting a vulnerability

For security-related reports, contact: **bas-module@delivery-auto.com.ua**

Please **do not** open public GitHub Issues for security problems — report them privately by email.

## Do not publish sensitive data

When reporting any problem (security or otherwise), never include:

- API keys or secret keys
- Passwords or logins
- Waybill (ТТН) numbers
- Phone numbers or addresses
- Personal data of recipients / senders
- Screenshots containing credentials
- Production logs

## If your credentials were compromised

If you suspect that your Delivery Auto API credentials were exposed:

1. Revoke the old credentials in your Delivery Auto account.
2. Generate new API and secret keys.
3. Update them in the module settings (**Налаштування**).

## How secrets are stored

This module stores API keys, the secret key and the cabinet password in
`ХранилищеОбщихНастроек` — a **shared database storage**. Any user with the
right to run external data processors can read them. See the **Security**
section of the [README](README.md) for the threat model and how to harden it.
