# tuyuMail — release distribution

This repository distributes **tuyuMail** release packages and update metadata. It contains no source code
development history, no customer data and no credentials. Development happens in a separate private repository.

## Layout

```
latest.json                     metadata of the newest stable release (read by installations over HTTPS)
releases/<version>/
    RELEASE_NOTES.md            what changed, upgrade notes
    tuyumail-<version>.zip      is NOT committed here: attached to the GitHub Release "v<version>"
    tuyumail-<version>.zip.sha256
```

## latest.json (schema 1)

| Field | Meaning |
|---|---|
| `schema` | metadata format version (integer) |
| `product`, `channel` | always `tuyuMail`, `stable` |
| `latest.version` | `MAJOR.MINOR.PATCH` |
| `latest.published` | `true` only after the package is uploaded and verified |
| `latest.release_date` | ISO date `YYYY-MM-DD` of publication |
| `latest.min_updater_version` | oldest installed updater able to install this release (`null` until an updater exists) |
| `latest.min_installed_version` | oldest installed version that may upgrade directly |
| `latest.package.url` | HTTPS download URL of the GitHub Release asset |
| `latest.package.sha256`, `size_bytes` | checksum and size of that exact file |
| `latest.release_notes_url` | HTTPS URL of `releases/<version>/RELEASE_NOTES.md` |
| `latest.requires` | minimum PHP version and required extensions |
| `latest.database` | whether the release adds migrations, and the newest migration file name |

Metadata is data only: it never contains commands or scripts. An installation that finds `null` in a required
field, `published: false`, an HTTP (not HTTPS) URL, or a checksum mismatch must refuse to install.

## Verifying a package

```
sha256sum -c tuyumail-<version>.zip.sha256          # Linux / Git Bash
certutil -hashfile tuyumail-<version>.zip SHA256     # Windows
```

Compare the result with `latest.package.sha256`. The package itself contains `tuyumail-<version>/release-manifest.json`
with the SHA-256 of every file.

## Installing

Fresh installation and upgrade instructions are in `README.md` inside the package. Each installation checks for
updates and upgrades independently, on an administrator's explicit action; nothing is pushed to installations.
