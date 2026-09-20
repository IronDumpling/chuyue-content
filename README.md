# chuyue-content

Blog posts, portfolio projects and their images for the Chuyue site. The site repository builds and deploys this content; this repository has no build of its own.

## Layout

- `blog/{category}/{type}/{slug}.mdx`
- `portfolio/{category}/{slug}.mdx`
- `images/blog/...`, `images/portfolio/...` (referenced from MDX as `/images/blog/...`, `/images/portfolio/...`)

Every push to `main` triggers a rebuild of the site.
