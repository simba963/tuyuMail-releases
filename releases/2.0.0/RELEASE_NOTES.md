# tuyuMail 2.0.0

_Released 2026-09-30._

## Highlights

- **New sign-in page.** A two-column layout with a marketing panel (one of five illustrations at random) next to the
  sign-in form, with show/hide password, "Remember me" and "Forgot password?". Works on phones and tablets, and
  honours reduced-motion settings.
- **Protection against password guessing.**
  - From the third failed attempt, a security check (CAPTCHA) is required. It is a picture selection, a picture
    sequence or a sum, and there is a text alternative.
  - The sixth failed attempt starts a temporary cooldown of 15 minutes (longer on repeats, at most 60).
  - Accounts are never locked permanently.
- **Remember me.** Stay signed in on your own device for 30 days. Stolen or old sign-in cookies stop working.
- **Password recovery.** Request a reset link by email. The branded email is sent through your default email
  provider, and the link works once for 60 minutes. After a reset, you are signed out everywhere.
- **Included from 1.9.0 (never released on its own):**
  - browser and command-line installer;
  - startup configuration check;
  - online updates from the dashboard;
  - Nginx support;
  - hosting hardening.

## Requirements

- PHP 8.2+ with ctype, curl, dom, fileinfo, gd, json, mbstring, openssl, pdo_mysql and zip.
- **MariaDB 10.4+.** MySQL is not supported, and the installer refuses it.
- Apache 2.4 (`.htaccess`) or Nginx + PHP-FPM.
- **Cron for the worker (`php bin/worker.php`).** It sends campaigns *and* password-reset emails.

## Updating

- **From 1.9.0:** Dashboard → Software updates → Install 2.0.0. A backup and maintenance mode are included, and the
  database migration runs automatically.
- **From 1.8.3:** manual upgrade, because 1.8.3 has no updater:
  1. Back up the database, `.env`, `storage/` and `public/uploads/email/`.
  2. Upload the new files, keeping `.env`, `storage/` and `public/uploads/email/`.
  3. Run `php bin/migrate.php`.
  4. Check with `php bin/check-config.php --db`.
  
  With `APP_ENV=production`, `APP_URL` must be `https://` (except `localhost`).

After updating:
- Make sure an **active default email provider** is set, so reset emails can be sent.
- Make sure the worker cron runs.
- Everyone keeps their password; no sign-in data is lost.
