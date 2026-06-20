# Changelog

## 2026.06.20 — Kvantum default via install scriptlet (no packaged kvconfig)

### What Changed
- Stopped shipping a packaged `kvantum.kvconfig`. The Kvantum selection is now written by a
  pacman **install scriptlet** to `/etc/skel/.config/Kvantum/kvantum.kvconfig` (`theme=Kiro-WhiteSur`)
  on install/upgrade. This removes the shared-file clash on that path (with `kiro-kvantum` and
  the other kiro-plasma themes) — they all coexist now; last-installed theme wins, falling back
  to `kiro-kvantum`'s `ArcDark` baseline.

### Technical Details
- Removed the `etc/` payload entirely (it held only the Kvantum selection); the PKGBUILD no
  longer copies `etc/`. Added `install=kiro-plasma-whitesur.install` (`post_install`/`post_upgrade`)
  and `depends+=('kiro-kvantum')` so the overwritten baseline stays package-owned and the
  override is deterministic. Dropped `conflicts=('kiro-kvantum')` (no longer needed).

### Files Modified
- Removed `etc/skel/.config/Kvantum/kvantum.kvconfig` (+ empty `etc/`)
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-whitesur/PKGBUILD` — drop `cp etc`, add `install=` + `kiro-kvantum` dep, drop conflicts
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-whitesur/kiro-plasma-whitesur.install` — new scriptlet

## 2026.06.20 — rename theme identity to Kiro namespace (coexist with upstream WhiteSur)

### What Changed
- Renamed every shipped theme identity from the upstream `WhiteSur` name into a `Kiro-`
  namespace so the package **coexists with the upstream WhiteSur theme** — a user can
  install `whitesur-kde-theme-git` alongside this without any pacman file conflict — and so
  System Settings shows honest **Kiro WhiteSur** / **Kiro WhiteSur Dark** / **Kiro WhiteSur
  Alt** labels.

### Technical Details
- Look-and-feel `com.github.vinceliuice.WhiteSur{,-dark,-alt}` → `com.kiroproject.WhiteSur*`
  (both `metadata.json` and legacy `metadata.desktop`). Desktoptheme (×3), aurorae (×10 incl.
  all HiDPI `_x*` variants, each with its `*rc`), Kvantum (×2 incl. inner `*Dark` configs/svgs),
  SDDM, the 3 color schemes, and the cursor theme all prefixed `Kiro-`.
- SDDM `Main.qml` absolute self-paths repointed to the renamed dir.
- Cross-references repointed: the 3 look-and-feel `defaults` (`cursorTheme`/`ColorScheme`/
  `__aurorae__svg__`/`plasmarc name`) and `etc/skel` Kvantum `theme=Kiro-WhiteSur`. The
  bundled icon theme (`kiro-whitesur{,-light,-dark}`) was already Kiro-named — unchanged.
  Logout-screen QML references an external WhiteSur *wallpaper* package (not shipped here) —
  left as-is.
- PKGBUILD: dropped `conflicts=(whitesur-kde-theme-git)` and bumped `pkgrel`. The
  `install.sh -n kiro-whitesur` icon-build step is unchanged.

### Files Modified
- Renamed all theme dirs/files under `usr/share/{plasma,aurorae,color-schemes,Kvantum,sddm,icons}` to `Kiro-WhiteSur*`
- The 3 look-and-feel `contents/defaults`, SDDM `Main.qml`, `etc/skel/.config/Kvantum/kvantum.kvconfig` — repointed
- `README.md`, `CLAUDE.md` — Kiro WhiteSur naming + coexistence note
- `../KIRO-PKG-BUILD-APPS/kiro-plasma-whitesur/PKGBUILD` — drop upstream conflicts, bump pkgrel

## 2026.06.20 — bundle WhiteSur icons (renamed, no external dep)

### What Changed
- **Bundled the WhiteSur icon theme into the package** instead of depending on
  `whitesur-icon-theme` (which is AUR-only — not in the official/nemesis repos, so the
  build couldn't resolve it as a dependency).
- The icons are **re-fetched fresh from `vinceliuice/WhiteSur-icon-theme` on every build**
  (a second `git+` source in the PKGBUILD) and installed via upstream `install.sh -n
  kiro-whitesur`, so they land as **`kiro-whitesur{,-light,-dark}`** — renamed to avoid the
  `/usr/share/icons/WhiteSur` file conflict with the AUR `whitesur-icon-theme` package.
- Repointed the three look-and-feel `defaults` icon themes to `kiro-whitesur`,
  `kiro-whitesur-dark`, `kiro-whitesur-light` to match.
- Recipe: dropped `whitesur-icon-theme` from `depends` (now `kvantum`, `sddm`); added
  `gtk-update-icon-cache` to `makedepends`.

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
