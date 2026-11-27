# Changelog — Curve Speed Potential Assessment Tool

All notable public changes and bug fixes to this project after the initial public release (`v2.7.2`) will be documented in this file.

## [Unreleased]

- Future public bug fixes and feature updates following the `2026-11-27` initial public release will be recorded here.

## [2.7.2] - 2026-11-27

### Initial Public Release (Windows Portable)

- **Public Distribution Package:** Initial public Windows x64 portable release (`IR-CSP_v2.7.2_Windows_Portable.zip`) developed independently by Basudev Kunwar (`ToolsNp` — `basudevkunwar.com.np`).
- **Startup Experience & Branding:** Immediate startup splash screen displaying live integrity verification and module loading progress, embedded application icon, and independent/unofficial software notices (`DISCLAIMER.txt`, `APPLICATION_LICENSE.txt`).
- **Engineering & Reporting Capabilities:** Curve speed potential assessment (circular and transition constraints under configurable IRPWM/IRSOD baselines), scenario comparison (`S1`–`S4`) with `Ca Rate (mm/s)` and `Cd Rate (mm/s)` register columns, batch CSV/XLSX import/export, KML export, Calculation PDF, and Remediation Dossier export.
- **Integrity & Open-Source Licensing:** Ed25519-signed release manifest (`RELEASE_INTEGRITY_MANIFEST.json`) and updater metadata (`releases/latest.json`), excluding dynamically linked LGPLv3 Qt/PySide6/Shiboken6 libraries with full third-party license notices (`compliance_notices/`) and corresponding source archives hosted in GitHub Releases.
