<p align="center">
  <img src="kiro.jpg" alt="Kiro" width="220" />
</p>

# kiro-plasma-whitesur

Kiro's **WhiteSur** Plasma global theme — the polished macOS look (KDE Store #2 by
downloads), packaged as ready-to-pick Global Themes for the Kiro Plasma edition.

## What it ships

Global Themes you select in **System Settings → Appearance → Global Themes**:
**WhiteSur** (light), **WhiteSur Dark**, and **WhiteSur Alt**, each with its full set of
layers:

| Layer | Path | Notes |
|---------------------|------------------------------------------|------------------------------|
| Plasma desktop theme | `/usr/share/plasma/desktoptheme/WhiteSur{,-dark,-alt}` | panels, widgets, popups |
| Global themes (look-and-feel) | `/usr/share/plasma/look-and-feel/com.github.vinceliuice.WhiteSur{,-dark,-alt}` | the three variants |
| Window decorations | `/usr/share/aurorae/themes/WhiteSur*` | light + dark, incl. HiDPI scales (x1.25–x2.0) |
| Color schemes | `/usr/share/color-schemes/WhiteSur{,Alt,Dark}.colors` | application colours |
| Kvantum themes | `/usr/share/Kvantum/WhiteSur{,-opaque}` | Qt app styling |
| Kvantum default selection | `/etc/skel/.config/Kvantum/kvantum.kvconfig` | new users get `WhiteSur` |
| SDDM login theme | `/usr/share/sddm/themes/WhiteSur` | Plasma 6 (Qt6) |
| Cursors | `/usr/share/icons/WhiteSur-cursors` | bundled WhiteSur cursors |

**Icons:** the WhiteSur icon set is **bundled** (built fresh from upstream at every
package build) and installed as **`kiro-whitesur`** (`/usr/share/icons/kiro-whitesur{,-light,-dark}`)
so it never conflicts with the AUR `whitesur-icon-theme` package — no external icon
dependency. WhiteSur is Plasma-6 native — no metadata conversion needed.

## Install

```bash
sudo pacman -S kiro-plasma-whitesur
```

Then open **System Settings → Appearance → Global Themes** and apply **WhiteSur**,
**WhiteSur Dark**, or **WhiteSur Alt**. New users get the WhiteSur Kvantum theme for Qt
apps automatically; existing users can pick it in **Kvantum Manager**.

## Heritage

Based on [vinceliuice/WhiteSur-kde](https://github.com/vinceliuice/WhiteSur-kde) and
[vinceliuice/WhiteSur-cursors](https://github.com/vinceliuice/WhiteSur-cursors), GPL-3.0.
The look-and-feel / desktoptheme / Aurorae are captured from the upstream `install.sh`
output (which assembles the Aurorae from parts), with Kvantum / SDDM / cursors taken from
git. See [UPSTREAM.md](./UPSTREAM.md) for exact sources and refresh notes.
