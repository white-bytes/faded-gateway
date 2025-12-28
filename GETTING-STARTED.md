# Getting Started with Faded Gateway

This guide will help you get started with developing Faded Gateway.

## Prerequisites

- **Node.js**: v18.17.0 or higher
- **Yarn**: v1.22.22 (specified in package.json)
- **Git**: For version control

## Installation

1. **Clone the repository** (if you haven't already):
   ```bash
   git clone https://github.com/white-bytes/faded-gateway.git
   cd faded-gateway
   ```

2. **Install dependencies**:
   ```bash
   yarn install
   ```

3. **Start the development server**:
   ```bash
   yarn dev
   ```
   
   Your site will be available at `http://localhost:4321`

## Available Commands

| Command | Description |
|---------|-------------|
| `yarn dev` | Starts development server at `localhost:4321` |
| `yarn build` | Builds production site to `./dist/` |
| `yarn preview` | Previews the production build locally |
| `yarn start` | Alias for `yarn dev` |

## Project Structure

```
faded-gateway/
├── public/              # Static assets
├── src/
│   ├── assets/         # Images, logos, media files
│   ├── components/
│   │   ├── override-components/  # Enhanced Starlight components
│   │   └── user-components/      # Custom DocKit components
│   ├── config/         # Configuration files
│   │   ├── config.json      # Site settings
│   │   ├── theme.json       # Theme customization
│   │   ├── sidebar.json     # Navigation structure
│   │   └── social.json      # Social media links
│   ├── content/
│   │   └── docs/       # Documentation markdown files
│   └── styles/         # Custom CSS
├── docs/               # Project documentation
├── astro.config.mjs    # Astro configuration
├── package.json
└── README.md
```

## Quick Customization

### 1. Update Site Branding

Edit `src/config/config.json`:
```json
{
  "site": {
    "title": "Your Site Name",
    "logo": "/src/assets/your-logo-light.svg",
    "logo_darkmode": "/src/assets/your-logo-dark.svg"
  }
}
```

### 2. Customize Theme Colors

Edit `src/config/theme.json`:
```json
{
  "theme": {
    "primary_color": "#your-color-hex"
  }
}
```

### 3. Update Navigation

Edit `src/config/sidebar.json` to customize the sidebar navigation structure.

### 4. Add Documentation Pages

Create new markdown files in `src/content/docs/`:
```bash
touch src/content/docs/your-page.md
```

Add frontmatter and content:
```markdown
---
title: Your Page Title
description: Page description
---

# Your Page Title

Your content here...
```

## Next Steps

1. **Read the Roadmap**: Check [ROADMAP.md](./ROADMAP.md) for the full development plan
2. **Review DocKit Features**: See [docs/dockit-readme.md](./docs/dockit-readme.md) for component documentation
3. **Define Your Vision**: Clarify what Faded Gateway will become
4. **Start Building**: Begin with Phase 1 from the roadmap

## Need Help?

- **DocKit Documentation**: [docs/dockit-readme.md](./docs/dockit-readme.md)
- **Astro Docs**: https://docs.astro.build
- **Starlight Docs**: https://starlight.astro.build
- **Cloudflare AI Gateway**: https://developers.cloudflare.com/ai-gateway/

## Development Tips

- **Hot Reload**: The dev server automatically reloads on file changes
- **Type Safety**: Uses TypeScript for better development experience
- **Component Library**: Check `src/components/user-components/` for pre-built components
- **Styling**: Uses Tailwind CSS v4 for styling

---

**Ready to start?** Run `yarn dev` and open `http://localhost:4321` in your browser!
