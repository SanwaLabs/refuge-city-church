# Refuge City Church

Website for Refuge City Church in Palmdale, California.

Live site: https://refugecitychurchav.org/

Plain static HTML and CSS. No build step, no dependencies.

## Run Locally

From the repo root:

```sh
npx live-server
```

This opens the site in your browser and reloads the page automatically whenever
you save `index.html` or `styles.css`. It needs Node installed, but adds nothing
to the repo.

Without Node, Python serves the same files with no auto-reload, so refresh the
browser yourself after each save:

```sh
python3 -m http.server 8000
```

Either way, use the served URL instead of opening `index.html` as a file, so
paths and the internal TODO page at `/todo/` behave the way they do in
production.

## Files

```text
index.html      Homepage (all sections live here)
styles.css      All styles
public/         Images (web-ready .jpg / .webp)
public/slides/  Optimized slideshow images (WebP + JPEG fallbacks)
public/original Untouched camera originals (.HEIC), not used by the site
preview/        Temporary before/after snapshots (noindex; delete after review)
todo/           Internal TODO list, excluded from search engines
robots.txt      Search engine rules
CNAME           Custom domain for GitHub Pages
DEPLOYMENT.md   Hosting, DNS, and GitHub Pages setup
```

## Editing Content

The homepage is one file. Each part of the page is a `<section>` with an `id`
that the nav links to: `#about`, `#beliefs`, `#pastors`, `#services`, `#location`.
The photo slideshow lives in the hero card beside the main headline.

The Statement of Belief lives in a native `<dialog>` modal opened from the
`#beliefs` section. No libraries are involved; open/close logic is a short
inline script in `index.html`. The slideshow uses the same pattern: a second
inline script, no dependencies.

Service times appear in three places, so update all of them together:

- the `#services` cards
- the hero card ("Join Us Sunday")
- the footer tagline

The `data-hf-id` attributes are leftovers from a visual editor export. They are
unused and safe to leave alone.

After changing `styles.css`, bump the version in the stylesheet link in
`index.html` (and `preview/before.html` if it still exists) so returning
visitors do not get a cached copy:

```html
<link rel="stylesheet" href="styles.css?v=1.0.7">
```

### Regenerating slideshow images

From the repo root, with ImageMagick installed (`magick`):

```sh
mkdir -p public/slides
magick public/IMG_0957.JPEG -auto-orient -strip -resize 560x -quality 74 public/slides/01-worship-560.webp
magick public/IMG_0957.JPEG -auto-orient -strip -resize 1000x -quality 74 public/slides/01-worship-1000.webp
magick public/IMG_0957.JPEG -auto-orient -strip -resize 800x -quality 80 public/slides/01-worship-800.jpg
# Repeat for 02-embrace (add -rotate 90), 03-prayer, 04-praise, 05-fellowship
```

Blur placeholders are 24px WebP files base64-inlined into `styles.css`, so they
are not kept as separate files in `public/slides/`.

## Search indexing

Every page currently includes:

```html
<meta name="robots" content="noindex, nofollow">
```

Remove that tag from each page when the site is ready to appear in search
results (see the Launch item on `/todo/`).

## TODO List

`todo/index.html` tracks pending site work. It is a normal page at
https://refugecitychurchav.org/todo/ but is kept out of search results with
`robots.txt` and a `noindex` meta tag, and nothing on the site links to it.
It is not private; the repo is public.

## Deploying

Push to `main` and GitHub Pages publishes automatically. See
[DEPLOYMENT.md](DEPLOYMENT.md) for details.
