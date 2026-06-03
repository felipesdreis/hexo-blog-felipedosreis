# hexo-blog-felipedosreis

Hexo 5.x static blog in Portuguese (pt-br). Theme: cactus. Deployed via Vercel.

## Commands

- `npx hexo server` — local dev server (default port 4000)
- `npx hexo generate` — build to `public/`
- `npx hexo new "titulo-do-post"` — scaffold a new post in `source/_posts/`

## Posts

- Location: `source/_posts/<filename>.md`
- Front matter: `title`, `date`, `tags` (list)
- Filenames use kebab-case in Portuguese (e.g. `review-kz-edx-pro.md`)
- Content written in Portuguese

## Notes

- Use npm, not yarn (yarn removed)
- No test suite — verify changes by running `npx hexo generate` and checking output
