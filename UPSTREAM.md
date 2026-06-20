# Upstream references — kiro-plasma-whitesur

Everything needed to refresh this theme from upstream in the future.

## Sources

| Component | Source | Notes |
|---------------------------|------------------------------------------|----------------------------|
| look-and-feel, desktoptheme, aurorae, color-schemes | **`install.sh` output** from `vinceliuice/WhiteSur-kde` | captured from the Plasma test box after running the official installer |
| Kvantum, SDDM | `https://github.com/vinceliuice/WhiteSur-kde` @ `1e4d960` | git (static dirs) |
| Cursors | `https://github.com/vinceliuice/WhiteSur-cursors` @ `e190baf` | bundled `dist/` |
| Icons | `https://github.com/vinceliuice/WhiteSur-icon-theme` | **fetched + built at every package build** (PKGBUILD `git+` source), installed as `kiro-whitesur*` |

- **Author:** vinceliuice · **License:** GPL-3.0 (upstream `LICENSE` carried in).
- **Plasma 6:** WhiteSur is P6-native (`metadata.json`, `X-Plasma-APIVersion 2`). SDDM
  uses the `WhiteSur-6.2` theme (`QtVersion=6`). **No P5→P6 conversion needed.**

## Why capture the installer output, not a raw git copy

WhiteSur is **not** in the KDE Store; it ships only via GitHub + `install.sh`. The Aurorae
decoration is **assembled at install time** from parts (`aurorae/main{,-sharp,-opaque}` +
`aurorae/common/assets{,-dark}` + per-scale variants), and the desktoptheme needs the
shared `desktoptheme/{icons,weather}` overlaid into each variant. A raw `cp` from git
produces a broken theme. So: run upstream `install.sh` (default = all 3 color variants,
round-blur window) on the Plasma test box, then capture the assembled result from
`~/.local/share/`.

## What was captured / copied (source → install path)

Captured from test-box `~/.local/share/` (installer output):
| Source | Installed to |
|------------------------------|----------------------------------------|
| `plasma/look-and-feel/com.github.vinceliuice.WhiteSur{,-dark,-alt}` | `usr/share/plasma/look-and-feel/` |
| `plasma/desktoptheme/WhiteSur{,-dark,-alt}` (icons+weather merged) | `usr/share/plasma/desktoptheme/` |
| `aurorae/themes/WhiteSur*` (light/dark + scales x1.25–x2.0) | `usr/share/aurorae/themes/` |
| `color-schemes/WhiteSur{,Alt,Dark}.colors` | `usr/share/color-schemes/` |

From `vinceliuice/WhiteSur-kde` git:
| Source | Installed to |
|------------------------------|----------------------------------------|
| `Kvantum/{WhiteSur,WhiteSur-opaque}` | `usr/share/Kvantum/` |
| `sddm/WhiteSur-6.2` | `usr/share/sddm/themes/WhiteSur` |

From `vinceliuice/WhiteSur-cursors`: `dist/` → `usr/share/icons/WhiteSur-cursors`.

## Refresh procedure
1. On the Plasma test box: `git clone …/WhiteSur-kde && cd WhiteSur-kde && ./install.sh`
   (default options) — let it assemble the aurorae/desktoptheme.
2. Capture `~/.local/share/{plasma/look-and-feel,plasma/desktoptheme,aurorae/themes,
   color-schemes}/WhiteSur*` back into `usr/share/`.
3. Re-copy `Kvantum/*`, `sddm/WhiteSur-6.2`→`sddm/themes/WhiteSur` from git, and cursors
   `dist/` from WhiteSur-cursors.
4. **Icons:** the 3 look-and-feel `defaults` reference `kiro-whitesur{,-light,-dark}` —
   the WhiteSur icon theme renamed at build time (PKGBUILD runs `install.sh -n kiro-whitesur`)
   to avoid the AUR `whitesur-icon-theme` file conflict. Keep that rename in sync if the
   defaults change. Cursors (`WhiteSur-cursors`) are bundled.

Kiro-only file (not upstream — leave as is on refresh):
- `etc/skel/.config/Kvantum/kvantum.kvconfig` → `[General] theme=WhiteSur`

## Intentionally NOT copied
- `sddm/WhiteSur-5.0`, `WhiteSur-6.0` — superseded by `6.2` for current Plasma 6.
- latte-dock, GTK/wallpapers from the repo — not part of this package.

## Verify on the Plasma test box
WhiteSur was installed there (the capture source); confirm all three variants appear and
apply in System Settings → Global Themes, with WhiteSur icons + cursors + Kvantum active.
