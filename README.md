# Public Assets Directory

This directory contains static assets that are served directly.

## Using Assets in Your Code

**Always use the `assetPath` utility** to ensure assets work correctly in both development and production (especially with GitHub Pages basePath):

```tsx
import { assetPath } from '@/lib/assetPath'

// Images
<img src={assetPath('/logo.png')} alt="Logo" />

// Downloadable files
<a href={assetPath('/downloads/slides.pdf')} download>Download Slides</a>

// Any public asset
<link rel="stylesheet" href={assetPath('/custom.css')} />
```

## Directory Structure

```
public/
├── README.md                              # This file
├── Dawson_En_Logo_Full_Color_RGB.png     # Institutional logo
├── PIM_banniere.png                       # PIM grant logo
├── IRV-logo-small.png                     # I.R.V. credit logo
├── downloads/                             # (Create as needed)
│   ├── slide-decks/                       # Workshop slide decks
│   ├── handouts/                          # Printable handouts
│   └── templates/                         # Downloadable templates
└── ...other assets
```

## Adding New Files

1. **For Images**: Just add the file to `public/` or a subdirectory
2. **For Downloads** (PDFs, slide decks, etc.):
   - Create logical subdirectories (e.g., `public/downloads/slide-decks/`)
   - Add your files
   - Link using `assetPath('/downloads/slide-decks/your-file.pdf')`

3. **In MDX Content**:
   ```mdx
   import { assetPath } from '../src/lib/assetPath'
   
   [Download Workshop Slides]({assetPath('/downloads/slides.pdf')})
   ```

## Why Use assetPath?

When deploying to GitHub Pages with a basePath (e.g., `/genai-sandbox-dawson`), regular paths like `/logo.png` won't work. The `assetPath` utility automatically prefixes paths with the basePath:

- Development: `/logo.png` → `/logo.png`
- Production: `/logo.png` → `/genai-sandbox-dawson/logo.png`

This ensures all assets load correctly regardless of deployment environment.

## Important Notes

- **Never import images/PDFs in code** - Use `assetPath()` instead
- Assets in this directory are **not processed** by Next.js
- Files are copied as-is to the build output
- Keep filenames lowercase with hyphens (e.g., `workshop-slides.pdf`)
- Avoid spaces in filenames
