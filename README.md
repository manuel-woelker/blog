# Manuel Woelker's Blog

A modern, professional blog built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, deployed to GitHub Pages.

**Live at**: [https://manuel-woelker.github.io/blog/](https://manuel-woelker.github.io/blog/)

## Tech Stack

- **Static Site Generator**: Hugo (Extended v0.140.2+)
- **Theme**: PaperMod - clean, fast, and feature-rich
- **Hosting**: GitHub Pages
- **CI/CD**: GitHub Actions
- **Content**: Markdown
- **Features**: Search, dark/light theme, syntax highlighting, reading time, TOC, social sharing

## Local Development Setup

### Prerequisites

- Hugo Extended v0.140.2 or later ([installation guide](https://gohugo.io/installation/))
- Git

### Getting Started

1. Clone the repository with submodules:
```bash
git clone --recurse-submodules git@github.com:manuel-woelker/blog.git
cd blog
```

2. Start the development server:
```bash
hugo server -D
```

3. Visit `http://localhost:1313/blog/` in your browser

The `-D` flag includes draft posts during development. Remove it to preview published content only.

## Creating New Blog Posts

### Quick Command

```bash
hugo new posts/my-post-title.md
```

This creates a new post using the archetype template with all necessary frontmatter.

### Manual Creation

1. Create a new file in `content/posts/`:
```bash
touch content/posts/my-post-title.md
```

2. Add frontmatter (see template below)

3. Write your content in Markdown

4. Set `draft: false` when ready to publish

### Frontmatter Template

```yaml
---
title: "Your Post Title"
date: 2026-02-05
draft: false
tags: ["tag1", "tag2"]
categories: ["Category Name"]
description: "Brief description for search results"
author: "Manuel Woelker"
showToc: true
---
```

### Frontmatter Options

- **title**: Post title (required)
- **date**: Publication date in YYYY-MM-DD format
- **draft**: Set to `true` to hide from published site
- **tags**: Array of tags for categorization
- **categories**: Array of categories
- **description**: Short excerpt for search results and meta tags
- **author**: Post author
- **showToc**: Show table of contents (true/false)

## Content Structure

```
content/
├── posts/          # Blog posts (Markdown files)
│   ├── hello-world.md
│   └── my-post.md
├── about.md        # About page
└── search.md       # Search page

static/
└── images/         # Static images (referenced as /blog/images/filename.png)
```

## Configuration

The blog is configured in `hugo.yaml`:

- **baseURL**: Set to `https://manuel-woelker.github.io/blog/` (project site URL)
- **theme**: PaperMod
- **menu**: Navigation menu (Posts, Tags, About, Search)
- **params**: Theme and site parameters
- **markup**: Code highlighting settings

### Important Notes

- All URLs and asset paths must include `/blog/` since this is a project site
- The `baseURL` must include the trailing slash
- Static assets should be placed in `static/` and referenced with `/blog/` prefix

## Deployment

Deployment is automated via GitHub Actions. When you push to the `master` branch:

1. GitHub Actions triggers the workflow (`.github/workflows/hugo.yaml`)
2. Hugo builds the site
3. The compiled site is deployed to GitHub Pages
4. Your changes are live at `https://manuel-woelker.github.io/blog/`

### Manual Deployment Check

To verify the workflow is configured correctly:

1. Go to your repository settings
2. Navigate to **Pages** section
3. Ensure **Source** is set to "GitHub Actions"
4. Check workflow runs at **Actions** tab

## Writing Tips

### Markdown Features Supported

- Standard Markdown syntax
- Code blocks with syntax highlighting
- Tables
- Footnotes
- Blockquotes
- Lists (ordered and unordered)

### Example Post

```markdown
---
title: "Understanding Go Interfaces"
date: 2026-02-05
draft: false
tags: ["golang", "programming"]
categories: ["Software Development"]
description: "A comprehensive guide to Go interfaces"
author: "Manuel Woelker"
showToc: true
---

## Introduction

Go interfaces are a powerful feature...

## Basic Usage

\`\`\`go
type Reader interface {
    Read(p []byte) (n int, err error)
}
\`\`\`

## Conclusion

Interfaces are fundamental to Go design...
```

## File Structure

```
blog/
├── .github/
│   └── workflows/
│       └── hugo.yaml          # GitHub Actions workflow
├── archetypes/
│   └── default.md              # Post template
├── content/
│   ├── posts/
│   │   └── hello-world.md
│   ├── about.md
│   └── search.md
├── static/
│   └── images/                 # Site images
├── themes/
│   └── PaperMod/               # Theme (git submodule)
├── .gitignore
├── .gitmodules
├── hugo.yaml                   # Main configuration
└── README.md
```

## Useful Commands

### Development
```bash
# Start server with drafts
hugo server -D

# Start server (published posts only)
hugo server

# Build the site
hugo
```

### Content Management
```bash
# Create new post
hugo new posts/post-title.md

# Create new draft (with draft: true)
hugo new -k post posts/draft-title.md
```

## Troubleshooting

### Links returning 404

Ensure `baseURL` in `hugo.yaml` includes the `/blog/` suffix:
```yaml
baseURL: 'https://manuel-woelker.github.io/blog/'
```

### Theme not loading

Update submodules:
```bash
git submodule update --init --recursive
```

### GitHub Actions deployment fails

1. Verify Pages source is set to "GitHub Actions" in repository settings
2. Check workflow logs in the **Actions** tab
3. Ensure `.gitmodules` is committed

### Local server not accessible

Make sure port 1313 is available or specify a different port:
```bash
hugo server -D -p 8080
```

## Performance

PaperMod is optimized for speed:
- Minimal dependencies
- Fast CSS/JS loading
- Optimized images
- Code splitting where applicable

The blog also uses Hugo's minification features to reduce file sizes.

## RSS Feed

An RSS feed is automatically generated at `/blog/index.xml`

Subscribe to stay updated on new posts!

## Future Enhancements

Potential improvements for the blog:

- [ ] Add Google Analytics or privacy-friendly alternative
- [ ] Enable comments via Giscus (GitHub Discussions)
- [ ] Custom domain setup
- [ ] OpenGraph images for social sharing
- [ ] Content organization by year/month
- [ ] Related posts suggestions
- [ ] Search analytics

## Contributing

This is a personal blog, but feedback and suggestions are welcome! Feel free to open issues for:
- Broken links or typos
- Content suggestions
- Technical improvements
- Design feedback

## License

The blog content is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The PaperMod theme is licensed under [MIT](https://github.com/adityatelange/hugo-PaperMod/blob/master/LICENSE).

## Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Theme Docs](https://github.com/adityatelange/hugo-PaperMod/wiki)
- [GitHub Pages Guide](https://docs.github.com/en/pages)
- [Markdown Syntax](https://www.markdownguide.org/)

## Contact

- **GitHub**: [manuel-woelker](https://github.com/manuel-woelker)
- **Twitter**: [@manuel_woelker](https://twitter.com/manuel_woelker)
- **LinkedIn**: [manuel-woelker](https://linkedin.com/in/manuel-woelker)

---

Built with ❤️ using Hugo and PaperMod
