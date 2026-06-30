# Software Trust Manager (STM) Dashboard — Project Context

This file gives Claude Code the background needed to continue this design/build
work without re-explaining it each session. Claude Code reads this file
automatically when this folder is opened.

## What this is

A dashboard redesign for **Software Trust Manager (STM)**, a code-signing and
certificate lifecycle management product within the **DigiCert ONE** platform.
Scope covers code signing, key management, certificate lifecycle, release
security, and software supply-chain risk governance.

Owner: Sourabh, UX/product designer at DigiCert.

## Tech stack & constraints

- **Charting**: AG Charts (`ag-charts-community`), loaded via CDN — mandated
  for all dashboard visualizations. No build framework required; this is a
  static HTML/CSS/JS project.
- **AG Charts gotcha**: charts must be lazily initialized — only init a chart
  when its panel/tab actually becomes visible, or it sizes incorrectly. Set
  locale to `en-US` explicitly to avoid a sandbox-specific "No data to
  display" crash during headless rendering (does not affect real browsers,
  but matters for any automated/Playwright validation).
- **Typography**: Plus Jakarta Sans.
- **Visual identity**: navy sidebar, brand blue `#0E76BC`.

## Established design decisions

### 1. "Set Up Signing" flow (formerly "Get Started")

- This is a **permanent, repeatable utility**, not one-time onboarding —
  naming and placement must reflect that.
- Renamed from "Get Started" to **"Set up signing."**
- Lives as its **nav item**, not embedded inside the Dashboard.
- **First-run routing model** (agreed):
  - New/unsigned users land on Set Up Signing by default, with the full nav
    visible (not a stripped-down onboarding shell).
  - A one-time **"Skip for now"** banner is the escape hatch.
  - A **persistent per-user checkbox** controls where subsequent sessions
    land (Dashboard vs. Set Up Signing).

### 2. Dashboard IA & metrics

- All metric cards must be **actionable** — deep-link to the corresponding
  filtered view, not just display a number.
- **Pending Approvals** is earmarked to graduate from a dashboard card into a
  top-level **"Action Center"** nav item (concept still being refined).
- Dashboard redesign has gone through a full iteration with six sections:
  Certificate lifecycle management, Signing & Licensing, Release monitoring, Vulnerability governance and the sidebar nav.

## Tools previously used for this project

- AG Charts (CDN)
- Python / PIL (Pillow) — competitor screenshot analysis (cropping,
  upscaling, gamma correction for dark UIs, dark-pixel-fraction boundary
  detection)
- openpyxl — competitive analysis Excel output
- Playwright — HTML prototype rendering/validation
