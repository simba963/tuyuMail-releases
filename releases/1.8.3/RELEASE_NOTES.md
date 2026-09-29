# tuyuMail 1.8.3

_Released 2026-09-29._

First versioned release (baseline). Highlights: email campaigns with a background sending worker and provider
failover; SMTP, Brevo, Amazon SES, Mailtrap and custom JSON gateway providers; HTML and visual template editors;
Address Book with groups, subscriptions and CSV import; campaign cloning; live dashboard; `.xlsx` exports.

## Requirements
PHP 8.2 or newer with the extensions ctype, curl, json, mbstring, openssl, pdo_mysql and zip; MySQL/MariaDB;
Apache with mod_rewrite (document root → `public/`).

## Installation
See `README.md` in the package: create `.env` from `.env.example`, create the database and import
`database/schema.sql`, generate the encryption key (`php bin/generate-key.php`), run `php bin/migrate.php`, create the first administrator (`php bin/create-admin.php`)
and schedule the worker (`php bin/worker.php`).

## Upgrading
1.8.3 is the first release; there is no earlier version to upgrade from and no online updater yet.
