# Editing the FLAME AI website

Live site: <https://flame-ai-workshop.github.io/> · Repo: `flame-ai-workshop/flame-ai-workshop.github.io`

**Anything pushed to `main` goes live in about a minute.** Preview locally first (§1), and
use a branch + pull request unless you're making a trivial fix.

---

## 1. Set up and preview (once)

macOS with Homebrew:

```sh
brew install ruby                      # macOS's built-in Ruby is too old
git clone git@github.com:flame-ai-workshop/flame-ai-workshop.github.io.git
cd flame-ai-workshop.github.io
script/bootstrap                       # installs Jekyll locally (first time only)
script/server                          # open http://127.0.0.1:4000 ; Ctrl-C to stop
```

The page reloads in the browser when you save a file. **Exception:** changes to `_config.yml`
need a server restart (Ctrl-C, then `script/server` again).

No local setup? You can edit files in the GitHub web UI. Use "Create a new branch" when
committing, open a PR, and ask a maintainer to preview it.

---

## 2. Where things are

| What you want to change | File |
|---|---|
| Title, dates/venue, Register link, Flyer link, banner (header) | `_config.yml` → `defaults` → block with `path: ""` |
| Mission, Agenda, Prize, Topics, any body text | `index.md` (below the second `---`) |
| Invited speakers | `index.md` → `speakers:` list at the top |
| Organizing committee / office-hour hosts | `organizers.md` → `speakers:` / `oh_hosts:` |
| Images and PDFs (photos, flyers, banner, topics) | `assets/img/` |
| Header buttons / page shell (rarely needed) | `_layouts/default.html` |
| Colors, fonts | `_sass/variables.scss`, `_sass/cayman.scss` |
| Archived years (normally leave alone) | `2024/…`, `2023/…` |

---

## 3. Common tasks

### 3.1 Set dates, registration, flyer, banner

In `_config.yml`, under `defaults`, edit the **first** block (`path: ""` = 2027):

```yaml
      venue: "Dates: Feb. 1 to Feb. 26 2027 | Venue: Virtual"
      register_url: https://events.humanitix.com/...   # blank = no Register button
      flyer_url: /assets/img/flyer.pdf                 # blank = no Flyer button
      header_bg: /assets/img/flameflowthing.png
      header_style: light    # light = dark text (mostly-white banner); dark = white text
```

Restart `script/server` to see the changes.

### 3.2 Add a speaker

1. Add the photo to `assets/img/` (see §4 for the photo format), e.g. `assets/img/doe.png`.
   Optionally add the flyer `assets/img/speaker_flyer_doe.pdf`.
2. In `index.md`, add an entry under `speakers:`. Cards appear in list order. Copy this template:

```yaml
speakers:
  - name: Jane Doe
    url: /assets/img/speaker_flyer_doe.pdf      # name links here (flyer, homepage, …); optional
    aff: Associate Professor <br /> Stanford University
    interest: '"Title of the Talk"'              # optional italic line; delete if unused
    image: /assets/img/doe.png
```

If `speakers: []` is still there, replace it with `speakers:` followed by your entries.

### 3.3 Add an organizer or office-hour host

The format is the same as for speakers, in `organizers.md`. Use the `speakers:` list for the
Organizing Committee and `oh_hosts:` for Office Hour Hosts. That section only appears once
`oh_hosts` has at least one entry.

```yaml
  - name: John Smith
    url: https://www.linkedin.com/in/...
    aff: Stanford University
    image: /assets/img/smith.png
```

The 2027 committee uses a fixed 2-column grid: `{% include team.html id="speakers" columns=2 %}`.
Change the number, or delete `columns=2` to go back to normal wrapping. Phones always wrap.

### 3.4 Edit page text

The body of `index.md` is plain Markdown:

- `# Heading`
- `**bold**`
- `1.` for numbered lists; indent with `-` for sub-bullets
- `[link text](https://…)`
- Image: `![topics](/assets/img/topics.png)`

To show the speaker cards anywhere in the body, keep this line:
`{% include team.html id="speakers" %}`

### 3.5 Add a new page (e.g. Schedule, Challenge)

1. Create `schedule.md`:
   ```markdown
   ---
   layout: default
   ---
   # Schedule
   ...
   ```
   It is served at `/schedule.html`.
2. For a header button, add this line next to the other buttons in `_layouts/default.html`:
   `<a href="{{ '/schedule.html' | relative_url }}" class="btn">Schedule</a>`
   (Note: the button then appears on the 2024/2023 pages too. Ask a maintainer if that's unwanted.)

---

## 4. Rules that prevent most breakage

**YAML (the part between the two `---` lines and `_config.yml`)**
- Indent with **2 spaces**, never tabs. Every entry starts with `  - name:`, and its other fields line up under `name`.
- Put text containing `:` or `#`, or starting with `"`, in quotes: `interest: '"AI: The Next Step"'`.
- Use `<br />` for a line break inside `aff`. Anything after ` #` is a comment and is ignored.

**Files and paths**
- File names: lowercase, no spaces (`doe.png`, not `Jane Doe.PNG`).
- Paths start with `/assets/img/…` (leading slash).
- **Case matters on the live site but not on your Mac.** `Doe.png` vs `doe.png` works locally and breaks online.

**Photos**
- Use a square PNG, about 900×900, with a transparent background. The photo must already be cropped to a circle with a ring (gray for regular speakers, red for keynotes), because the site doesn't round it.
- The easiest way: copy an existing photo in `2024/assets/img/` as a reference for the style.
- Keep each file under about 500 KB, and banners under about 1 MB. Compress at <https://tinypng.com>.

**Don't touch:** `2024/`, `2023/`, `vendor/`, `_site/`, `Gemfile*`, unless you mean to.

---

## 5. Publishing checklist

- [ ] `script/server` shows no errors, and the page looks right at <http://127.0.0.1:4000>
- [ ] New images and links load (check the 2024/2023 tabs still work too)
- [ ] `git status`: only the files you meant to change, plus new images
- [ ] Commit on a branch → push → open a PR → merge to `main`
- [ ] After merging: the repo's **Actions** tab shows "pages build and deployment" ✅, and the live site updates (hard-refresh: ⌘⇧R)

## 6. Troubleshooting

| Symptom | Likely cause |
|---|---|
| Page blank or missing cards, or the server prints `YAML Exception` | Bad indentation, a tab, or an unquoted `:` in the front matter |
| Image shows locally but not online | Filename case mismatch, or the file wasn't committed (`git add`) |
| `_config.yml` change has no effect | Server not restarted |
| Live site not updated | Build failed (red ❌ in the Actions tab; the error names the file and line), or browser cache |
| `script/bootstrap` fails | Homebrew Ruby missing: run `brew install ruby` and open a new terminal |

---

## 7. 2027 fill-in list

Current placeholders on the 2027 page:

- [x] Dates and venue: 1–26 Feb 2027, Virtual: `_config.yml` → `venue`
- [x] Registration link (Humanitix): `_config.yml` → `register_url`
- [ ] Flyer PDF: `assets/img/flyer.pdf`, then `_config.yml` → `flyer_url`
- [x] 2027 banner: `assets/img/flameflowthing.png` (`header_bg`, with `header_style: light`)
- [ ] Agenda, challenge description, prize: `index.md`
- [ ] Topics graphic (optional): `assets/img/topics.png` plus `![topics](/assets/img/topics.png)` in `index.md`
- [ ] Invited speakers: `index.md` → `speakers:`
- [x] Organizing committee: `organizers.md`
- [ ] Office-hour hosts: `organizers.md` → `oh_hosts:`

Questions: flame.ai.workshop@gmail.com
