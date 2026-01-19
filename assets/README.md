# Assets Directory

This directory contains static assets for the FragIQ GitHub Pages site.

## Required Files

| File | Dimensions | Purpose |
|------|------------|---------|
| `icon-192.png` | 192x192 | Website favicon and header logo |
| `icon-512.png` | 512x512 | Hi-res icon for Play Store listing |
| `feature-graphic.png` | 1024x500 | Play Store feature graphic |

## Screenshots Directory

Place app screenshots in the `screenshots/` subdirectory:

| File | Dimensions | Description |
|------|------------|-------------|
| `frags-list.png` | 1080x1920 (9:16) | Main frags list screen |
| `frag-detail.png` | 1080x1920 (9:16) | Frag detail with photos |
| `add-frag.png` | 1080x1920 (9:16) | Add/edit frag form |
| `tanks.png` | 1080x1920 (9:16) | Tank management |
| `dashboard.png` | 1080x1920 (9:16) | Dashboard overview |

## How to Add Assets

### From Main Project

```powershell
# Copy and resize icon from main assets
Copy-Item "..\assets\icon.png" "icon-192.png"

# For 512x512, you may need to use an image editor or:
# magick convert "..\assets\icon.png" -resize 512x512 icon-512.png
```

### From Screenshot Pipeline

If you have automated screenshots from the CI/CD pipeline:

```powershell
Copy-Item "path\to\generated\screenshots\*.png" "screenshots\"
```

## Notes

- All images should be PNG or JPG format
- Icons should not have transparency for Play Store
- Screenshots should be actual app screens, not mockups (for production)
