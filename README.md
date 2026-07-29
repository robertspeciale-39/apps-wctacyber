# apps.wctacyber.org — WCTA Cyber Tool Library

Cold-boot themed tool library for West CTA Cybersecurity. Single-file, no build
step, no dependencies beyond Google Fonts.

```
index.html    the page (design system + boot sequence + grid). Rarely edit.
links.json    ALL your content. This is the file you edit.
CNAME         custom domain for GitHub Pages.
```

---

## Adding or changing a tool

Edit `links.json` only. Never touch `index.html` for content changes.

```json
{ "category": "Network+", "name": "My New Tool", "url": "https://my-tool.vercel.app/", "description": "One short line students will read on the card." }
```

Add the object to the `tools` array, bump `updated`, commit. Done.

Everything downstream regenerates automatically from that array:

- category grouping and headings
- per-category colour coding
- filter buttons
- tool counts (`8 tools`, `1 tool` — plural handled)
- boot-log mount lines (`Mounting /network [ro] · 8 modules`)
- search index

## Adding a category

Just use a new `category` value on any tool. That's it — a new group, colour,
and filter button appear on their own.

- Display order = order the category first appears in the array.
- Colours are assigned automatically in this order: `u1`, `u3`, `u4`, `u5`, `u2`.
  That order is deliberate — `u1` and `u2` are both greens in the Matrix theme,
  so `u2` is held back to keep adjacent categories distinct in all five themes.
- Past 5 categories, colours start repeating.

If only ONE category exists, the filter bar hides itself automatically.

## Removing a tool

Delete its object. Nothing else to clean up.

---

## Notes

- **Multi-category tools.** Currently handled with a literal `"Both"` category.
  If you'd rather a tool appear under *each* of its categories instead, that's a
  small code change — ask.
- **Category names** are shown verbatim. `"Security+"` renders as `Security+`.
- **`updated`** is displayed in the topbar and in the boot log.

## Local preview

`fetch()` is blocked on `file://`, so opening `index.html` by double-clicking
shows a "Library unavailable" notice. Serve it instead:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy (GitHub Pages)

Commit all four files to the repo root, keep Pages pointed at the branch root.
`CNAME` keeps `apps.wctacyber.org` attached.

---

## Behaviour worth knowing

- **Boot sequence** runs ~6s on first visit each session, then is skipped
  (`sessionStorage`). "Replay boot sequence" link re-runs it on demand.
- **Reduced motion** (`prefers-reduced-motion`) skips the animation entirely and
  goes straight to the grid.
- **Sound** is off by default and only unlocks after a click — browsers block
  autoplay audio. Toggle sits next to Skip intro / Replay.
- **Themes** — Matrix (default), Arctic, Crimson Ops, Tokyo, Galaxy. The choice
  persists across every CyberSpesh app on the same origin via `cs_theme`.
