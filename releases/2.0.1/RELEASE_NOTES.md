# tuyuMail 2.0.1

_Released 2026-09-30._

Patch release. No database changes.

## Fixed

- **"The release server did not answer in time."** The dashboard update check (and the package download) could time
  out when one of GitHub's server addresses was unreachable from your host, because only the first address was tried.
  Now every checked address is available, and the next one is used if a connection cannot be opened.
- The same improvement applies to email providers that use an HTTPS API (Brevo, Amazon SES, Mailtrap, custom
  gateway).
- Security is unchanged: HTTPS certificate checks, fixed host names, public-address checks, time and size limits and
  the no-redirect rule all stay in place, and a message is never sent twice.

## Requirements

Unchanged from 2.0.0: PHP 8.2+ with ctype, curl, dom, fileinfo, gd, json, mbstring, openssl, pdo_mysql and zip;
MariaDB 10.4+; Apache 2.4 or Nginx + PHP-FPM; a cron job for the worker (`php bin/worker.php`).

## Updating

- **From 2.0.0 or 1.9.0:** Dashboard → Software updates → Install 2.0.1. A backup and maintenance mode are included.
  From 1.9.0 the database migration of 2.0.0 runs automatically; see the
  [2.0.0 notes](../2.0.0/RELEASE_NOTES.md) for what changes (new sign-in page, reset emails through the worker).
- If the dashboard of a 1.9.0 or 2.0.0 installation shows "did not answer in time", open it again after a minute:
  the older updater tries one address per check, so a retry usually succeeds.
- **From 1.8.3:** manual upgrade as described in the [2.0.0 notes](../2.0.0/RELEASE_NOTES.md).
