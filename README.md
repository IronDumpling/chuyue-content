# chuyue-content

Blog posts, portfolio projects and their images for the Chuyue site. The site repository builds and deploys this content; this repository has no build of its own.

## Layout

- `blog/{category}/{slug}.mdx`
- `portfolio/{category}/{slug}.mdx`
- `images/blog/...`, `images/portfolio/...` (referenced from MDX as `/images/blog/...`, `/images/portfolio/...`; they mirror the content folders, e.g. `images/blog/films/`)

The folder a file sits in **is** its category, and the category is part of its URL (`/blog/films/her-review/`). Do not write `category:` or `type:` in frontmatter; the folder decides.

Every folder must be a category the site knows. The site build fails on an unknown folder, so a typo cannot silently drop posts. The category list lives in the site repository, in `lib/taxonomy.ts`:

| Section | Group | Categories (folder names) |
|---|---|---|
| blog | Moments | `moments` |
| blog | Reviews | `films`, `shows`, `music`, `video-games`, `books` |
| portfolio | Computing | `applications`, `games`, `systems`, `ai` |
| portfolio | Art | `photography`, `illustration` |

Groups only shape the filter menu. They never appear in a folder name or a URL, so moving a category to another group needs no file changes.

## Where does a project go?

Pick the category by **what the thing is**, not by the technology it uses.

- The AI is a feature of something people use → `applications` (a travel assistant is an application; tag it `AI Agent`).
- The AI is the subject of the work (a model, an algorithm, an experiment, an agent framework) → `ai`.
- Systems software (kernels, databases, distributed storage, networking, compilers) → `systems`.
- Games, and rendering / graphics work → `games`.
- If it fits two categories, pick the closer one and use `tags` for the other side. Do not create a category for a single project.

Where it was made is not a category. Use the optional `context` field instead: `course`, `research`, `work` or `personal`. It shows as a small badge on the project card.

## Link fields (portfolio)

`github`, `demo` and `website` are always a **list**, even for a single link:

```yaml
github:
  - url: "https://github.com/you/repo"
    label: "Frontend"        # optional; falls back to "View on GitHub" (one link)
                              # or "GitHub Repo 1", "GitHub Repo 2", … (several links)
demo:
  - url: "https://example.com"
website:
  - url: "https://example.com"
    label: "View More"
```

Leave the field out entirely (not `github: ""`) when a project has none. `demo` falls back to "View Demo", `website` to "Visit Website" when `label` is omitted.

## Bilingual posts

`her-review.en.mdx` is the English text. Add `her-review.zh.mdx` next to it for a Chinese version (same slug, so the same URL). A post missing one language is shown in the other with a notice. Every content file carries its language as a suffix — there is no un-suffixed form anymore.

## Editing from a phone

The site serves an editor at `<site>/admin/` (Sveltia CMS). Sign in with a GitHub fine-grained token scoped to this repository only, with Contents: read and write — never a token with access to the site repository. The editor's fields for each Blog and Portfolio category are generated from the site's `lib/taxonomy.ts`, so they always match this layout.

Every push to `main` triggers a rebuild of the site.
