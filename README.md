# Burak Kanber Personal Blog

Personal technical blog built with [Hexo](https://hexo.io/) and the [NexT](https://theme-next.js.org/) theme, deployed on Cloudflare Pages.

## Topics

- **Software Architecture** — Cloud platforms, API design, deployment strategies
- **SAP** — Transaction codes, ERP automation patterns
- **Accounting & IFRS** — Financial reporting standards for tech professionals
- **IoT & AI** — Sensor integration, computer vision, production ML
- **PlantUML** — System architecture diagrams as code
- **Book** — *Just Build It: From Consuming to Producing Technology*

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Static Site Generator | Hexo 8.x |
| Theme | NexT v8 (Gemini scheme) |
| Styling | Stylus + CSS custom properties (dark mode) |
| Hosting | Cloudflare Pages |
| Source Control | GitHub |

## Local Development

```bash
# Install dependencies
npm install

# Start dev server (http://localhost:4000)
npx hexo server

# Generate static files
npx hexo generate

# Create a new post
npx hexo new post "Post Title"
```

## Project Structure

```
├── _config.yml            # Hexo configuration
├── _config.next.yml       # NexT theme configuration
├── source/
│   ├── _posts/            # Blog posts (Markdown)
│   ├── _data/
│   │   ├── styles.styl    # Custom styles
│   │   ├── variables.styl # Theme variable overrides
│   │   ├── footer.njk     # Custom footer
│   │   └── head.njk       # Custom head injection
│   ├── about/             # About page
│   ├── images/            # Static images
│   └── ...                # Tags, categories, archives pages
├── scaffolds/             # Post templates
└── themes/                # Theme directory
```

## Deployment

Cloudflare Pages builds and deploys automatically on every push to `main`.

| Setting | Value |
|---------|-------|
| Build command | `npx hexo generate` |
| Output directory | `public` |
| Node version | `20` |

## Author

**Burak Kanber** — Digital Transformation Specialist

- [LinkedIn](https://www.linkedin.com/in/burak2kanber/)
- [GitHub](https://github.com/datkanber)
- [Kaggle](https://www.kaggle.com/kanberburak)
- [ORCID](https://orcid.org/0009-0006-5688-5372)

## License

Blog content © 2026 Burak Kanber. All rights reserved.
