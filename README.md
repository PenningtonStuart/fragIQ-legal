# FragIQ GitHub Pages Site

This folder contains the static website for FragIQ, designed to be deployed via GitHub Pages. It provides publicly accessible legal documents (Privacy Policy, Terms of Service) required for Google Play Store submission.

## 📁 Structure

```
GithubPages/
├── _config.yml          # Jekyll configuration
├── index.html           # Landing page
├── privacy.html         # Privacy Policy (required for Google Play)
├── terms.html           # Terms of Service
├── css/
│   └── style.css        # Shared styles
├── assets/
│   ├── icon-192.png     # App icon (copy from main assets)
│   ├── icon-512.png     # Hi-res icon for store
│   ├── feature-graphic.png  # Feature graphic (1024x500)
│   └── screenshots/     # App screenshots
└── README.md            # This file
```

## 🚀 Deployment

### Option 1: Deploy from this subfolder

1. Go to your repository Settings → Pages
2. Under "Source", select "Deploy from a branch"
3. Select the branch and folder `/GithubPages`
4. Click Save

### Option 2: Deploy to root (recommended for custom domain)

1. Copy all contents of `GithubPages/` to the repository root or a `docs/` folder
2. Configure GitHub Pages to deploy from that location

### Option 3: Separate repository

1. Create a new repository named `<username>.github.io` or `fragiq-site`
2. Copy all contents of this folder to that repository
3. Enable GitHub Pages in that repository

## 🔗 URLs After Deployment

Once deployed, your pages will be accessible at:

- **Landing Page**: `https://penningtonstuart.github.io/fragIQ-legal/`
- **Privacy Policy**: `https://penningtonstuart.github.io/fragIQ-legal/privacy.html`
- **Terms of Service**: `https://penningtonstuart.github.io/fragIQ-legal/terms.html`

> **Note**: Update the URLs in `_config.yml` and throughout the HTML files if using a custom domain.

## ✅ Google Play Store Requirements

This site satisfies the following Google Play requirements:

| Requirement | File | Status |
|-------------|------|--------|
| Privacy Policy URL | `privacy.html` | ✅ Ready |
| Terms of Service URL | `terms.html` | ✅ Ready |
| Developer Website | `index.html` | ✅ Ready |

## 📦 Required Assets

Before deployment, copy these assets from the main project:

1. **App Icon (192x192)**: Copy from `assets/icon.png` → `GithubPages/assets/icon-192.png`
2. **App Icon (512x512)**: Export or copy → `GithubPages/assets/icon-512.png`
3. **Feature Graphic (1024x500)**: Create or generate → `GithubPages/assets/feature-graphic.png`
4. **Screenshots**: Copy from screenshot generation pipeline → `GithubPages/assets/screenshots/`

### Quick Copy Commands (PowerShell)

```powershell
# Create assets directory
New-Item -ItemType Directory -Path "GithubPages/assets/screenshots" -Force

# Copy icon (you may need to resize to 192x192)
Copy-Item "assets/icon.png" "GithubPages/assets/icon-192.png"

# Copy screenshots (if generated)
# Copy-Item "path/to/screenshots/*.png" "GithubPages/assets/screenshots/"
```

## 🎨 Customization

### Colors

The site uses a dark theme matching the app. Colors are defined as CSS variables in `css/style.css`:

```css
:root {
  --bg-primary: #0B1426;
  --accent-primary: #0EA5E9;
  /* ... */
}
```

### Content Updates

- **Privacy Policy**: Edit `privacy.html` (keep in sync with `src/screens/settings/PrivacyPolicyScreen.tsx`)
- **Terms of Service**: Edit `terms.html` (keep in sync with `src/screens/settings/TermsOfServiceScreen.tsx`)
- **Landing Page**: Edit `index.html` for marketing content

## 🔄 Keeping Documents in Sync

The Privacy Policy and Terms of Service exist in two places:
1. **In-app**: `src/screens/settings/PrivacyPolicyScreen.tsx` and `TermsOfServiceScreen.tsx`
2. **Website**: `GithubPages/privacy.html` and `GithubPages/terms.html`

**Important**: When updating either version, update both to keep them synchronized.

## 📋 Checklist Before Going Live

- [ ] Copy app icon to `assets/icon-192.png`
- [ ] Create/copy 512x512 icon to `assets/icon-512.png`
- [ ] Create feature graphic (1024x500) at `assets/feature-graphic.png`
- [ ] Add app screenshots to `assets/screenshots/`
- [ ] Update URLs in `_config.yml` if using custom domain
- [ ] Test all pages locally
- [ ] Enable GitHub Pages in repository settings
- [ ] Verify all URLs are accessible
- [ ] Add URLs to Google Play Console store listing
- [ ] Add Privacy Policy URL to `app.json` for Play Store

## 🔗 Linking in App Configuration

After deployment, add the Privacy Policy URL to your `app.json`:

```json
{
  "expo": {
    "android": {
      "privacyUrl": "https://penningtonstuart.github.io/fragIQ-legal/privacy.html"
    }
  }
}
```

## 📞 Support

For questions about the website or legal documents:
- Email: fragg3d.reef.innovation@gmail.com
