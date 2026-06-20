# Changelog

## 2026.06.20 — initial package

### What Changed
- New repo: **kiro-plasma-whitesur**, the **WhiteSur** (macOS-style) Plasma global theme
  for the Kiro Plasma edition — KDE Store #2 most-downloaded global theme. Ships **WhiteSur**
  (light), **WhiteSur Dark**, and **WhiteSur Alt** as full Global Themes.
- Combined the layers: 3 desktopthemes + 3 look-and-feel + Aurorae (light/dark + HiDPI
  scales x1.25–x2.0) + 3 color schemes + Kvantum (WhiteSur, WhiteSur-opaque) + SDDM (Qt6)
  + bundled WhiteSur cursors.
- **Captured from the upstream `install.sh` output** on the Plasma test box: WhiteSur is
  not in the KDE Store (GitHub-only), and its Aurorae is *assembled at install time* from
  parts + the desktoptheme needs an icons/weather overlay — so a raw git copy breaks. The
  installer output is the correct, working result.
- **No Plasma-6 metadata conversion** — WhiteSur is already P6-native (`metadata.json`,
  `X-Plasma-APIVersion 2`; SDDM `WhiteSur-6.2`, `QtVersion=6`). Kvantum/SDDM/cursors from git.
- **Icons:** uses the WhiteSur icon set → depends on `whitesur-icon-theme` (no defaults edit).
- **Default Kvantum selection** via `/etc/skel/.config/Kvantum/kvantum.kvconfig` (`theme=WhiteSur`).

### Technical Details
- Sources: Plasma-test-box `install.sh` output (look-and-feel/desktoptheme/aurorae/
  color-schemes), [vinceliuice/WhiteSur-kde](https://github.com/vinceliuice/WhiteSur-kde)
  `1e4d960` (Kvantum, SDDM 6.2), [vinceliuice/WhiteSur-cursors](https://github.com/vinceliuice/WhiteSur-cursors)
  `e190baf`. Full mapping in [UPSTREAM.md](./UPSTREAM.md).
- License: GPL-3.0.
- Recipe depends on `whitesur-icon-theme`, `kvantum`, `sddm`; copies `usr/` + `etc/`.

### Files Modified
- usr/share/plasma/look-and-feel/com.github.vinceliuice.WhiteSur{,-dark,-alt} (new)
- usr/share/plasma/desktoptheme/WhiteSur{,-dark,-alt} (new)
- usr/share/aurorae/themes/WhiteSur* (light/dark + scales) (new)
- usr/share/color-schemes/WhiteSur{,Alt,Dark}.colors (new)
- usr/share/Kvantum/{WhiteSur,WhiteSur-opaque}, sddm/themes/WhiteSur (new)
- usr/share/icons/WhiteSur-cursors (new)
- etc/skel/.config/Kvantum/kvantum.kvconfig (new)
- README.md, CHANGELOG.md, CLAUDE.md, UPSTREAM.md, LICENSE, up.sh, setup.sh, kiro.jpg, .gitignore (new)
