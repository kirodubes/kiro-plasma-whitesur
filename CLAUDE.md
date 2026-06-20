# kiro-plasma-whitesur — Project Claude Instructions

## Overview
The **WhiteSur** (macOS-style) Plasma global theme for the Kiro Plasma edition. Ships
WhiteSur (light), WhiteSur Dark, WhiteSur Alt as Global Themes. Sibling to
[[kiro-plasma-sweet]], [[kiro-plasma-nord]], [[kiro-plasma-layan]].

## Current state
- Source repo: `~/KIRO/kiro-plasma-whitesur` (payload under `usr/`, Kvantum default `etc/skel`).
- Build recipe: `~/KIRO-PKG-BUILD-APPS/kiro-plasma-whitesur`.
- Sources: test-box `install.sh` output (look-and-feel/desktoptheme/aurorae/color-schemes)
  + vinceliuice/WhiteSur-kde git (Kvantum, SDDM) + WhiteSur-cursors. See [UPSTREAM.md](./UPSTREAM.md).

## Patterns / things to know
- **Plasma 6 native** — no metadata conversion (like Layan, unlike Nord).
- **NOT in the KDE Store — GitHub `install.sh` only.** The Aurorae is *assembled at install
  time* from parts and the desktoptheme needs an icons/weather overlay, so a raw git copy
  breaks. Refresh by running upstream `install.sh` on the test box, then capturing
  `~/.local/share/...` (see UPSTREAM.md). Do NOT hand-copy aurorae/desktoptheme from git.
- **Icons are the WhiteSur set** (the macOS pairing). Recipe depends on `whitesur-icon-theme`.
  Defaults reference `WhiteSur`; do NOT repoint to neo-candy.
- **No defaults edits** — `WhiteSur` icons (dep) and `WhiteSur-cursors` (bundled) satisfied.
- Aurorae ships HiDPI scale variants (x1.25–x2.0) — keep them; KWin picks by DPI.
- SDDM from `WhiteSur-6.2` (Qt6) installed as `sddm/themes/WhiteSur`; 5.0/6.0 excluded.
- Kvantum default for new users: `etc/skel/.config/Kvantum/kvantum.kvconfig` → `theme=WhiteSur`.
- Mixed delivery: payload → `/usr/share`, Kvantum selection → `/etc/skel`. PKGBUILD copies both.
- **Test on the Plasma test box** — it was the capture source; confirm all 3 variants apply.
