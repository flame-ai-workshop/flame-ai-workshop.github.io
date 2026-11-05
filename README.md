# Stanford FLAME AI Workshop website

Source for <https://flame-ai-workshop.github.io/>. **Collaborators: see [EDITING.md](EDITING.md) for how to update content.** A Jekyll site built by GitHub Pages
directly from the `main` branch (legacy "deploy from branch" build, `github-pages` gem,
Jekyll 3.10, Cayman theme with local overrides). Pushing to `main` publishes.

## Layout

```
_config.yml            Site settings + per-edition header settings (`defaults`) + edition switcher (`editions`)
_layouts/default.html  Page shell: header (title, dates, buttons, banner), content, footer
_includes/team.html    Circular photo cards; used for speakers / organizers / office-hour hosts
_sass/                 Cayman theme overrides (colors in variables.scss, styles in cayman.scss)
assets/css/style.scss  Entry point compiled to /assets/css/style.css (shared by all editions)

index.md, organizers.md, assets/img/        Current edition (2027)   -> /
2024/index.md, 2024/organizers.md, 2024/assets/img/   Archive        -> /2024/
2023/index.md, 2023/organizers.md, 2023/assets/img/   Archive        -> /2023/

script/bootstrap       One-time local setup (gems into ./vendor/bundle)
script/server          Local preview with live reload
```

Each page's front matter holds its people lists (`speakers:`, `oh_hosts:`); the body is
Markdown and renders a list with `{% include team.html id="speakers" %}`.
Header fields (title, venue/dates, Register/Flyer URLs, banner image) come from
`defaults` in `_config.yml`, keyed by folder; a page's own front matter overrides them.
A blank `register_url` or `flyer_url` hides that button.

## Local preview

Requires Homebrew Ruby (`brew install ruby`); macOS system Ruby 2.6 is too old.

```sh
script/bootstrap        # first time only
script/server           # http://127.0.0.1:4000  (Ctrl-C to stop)
```

Pages, layouts, includes, Sass and images reload automatically.
`_config.yml` is read only at startup: restart `script/server` after editing it.

## Common edits

- **Add a speaker:** put the photo (square, ideally <300 KB) and optional flyer PDF in
  `assets/img/`, then add an entry to `speakers:` in `index.md`.
- **Set dates / registration / flyer:** edit the `path: ""` block under `defaults` in `_config.yml`.
- **Change the banner:** put the image in `assets/img/` and set `header_bg:` to its path. For a
  mostly-white image set `header_style: light` (dark text); for a dark image use `dark`.
  Values inherit from the root block, so archived blocks set `header_style: dark` explicitly.

## Archiving the current edition (e.g. when 2029 starts)

1. `mkdir -p 2027/assets/img` and `git mv index.md organizers.md 2027/`;
   `git mv` the edition's images/PDFs from `assets/img/` into `2027/assets/img/`.
2. In `2027/*.md`, rewrite `/assets/img/` to `/2027/assets/img/`.
3. In `_config.yml`: copy the `path: ""` defaults block to a new `path: "2027"` block
   (with `edition_url: /2027/`, asset paths under `/2027/`), then update the root block for
   the new year. Add the new year to the top of `editions:` and change 2027's `url` to `/2027/`.
4. Create the new root `index.md` / `organizers.md`.
