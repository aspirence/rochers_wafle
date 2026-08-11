# Images

| File         | Used in                                        |
| ------------ | ---------------------------------------------- |
| `main.webp`  | **Why We Made This** (second section) + social share card |
| `front.webp` | **What's Inside** — left pack photo, and the sticky buy-bar thumbnail |
| `back.webp`  | **What's Inside** — right pack photo (ingredients / allergen side) |
| `4.webp`     | **Ready to Crunch** — the closing section        |

All four are in place. Any slot whose file is missing renders a labelled panel
describing the shot instead of a broken image, so nothing ever looks broken.

---

## Optional: turn the break-apart scroll into a real photo

The hero's signature effect — the waffle that cracks into six pieces as you
scroll — currently draws a **vector waffle**, because it needs a very specific
kind of file:

**`hero-chips.png` — square, chips only, background fully removed (transparent PNG).**

Drop that in and the six shards use the real photo automatically. No code change.

It cannot use `main.webp` or any other lifestyle shot: those have a table, a
wall and a plant in them, so each shard would fly off carrying a rectangle of
background with it.

## Optional: lifestyle gallery

The lifestyle gallery section was removed because no such photos exist (six
empty boxes is worse than no section). If these get shot, say so and it goes
back in:

| File           | Shot                                            | Size      |
| -------------- | ----------------------------------------------- | --------- |
| `crunch.webp`  | Macro — a chip snapping in half, crumbs mid-air | 1400×1000 |
| `life-1.webp`  | Chips served with chai                          | 1000×1250 |
| `life-2.webp`  | Snacking on the go                              | 1000×1250 |
| `life-3.webp`  | Sharing with friends                            | 1000×1250 |
| `life-4.webp`  | Chips spilling out of an open pack              | 1000×1250 |
| `life-5.webp`  | Chocolate drizzle, close up                     | 1000×1250 |
| `life-6.webp`  | Pack styled as a gift                           | 1000×1250 |
