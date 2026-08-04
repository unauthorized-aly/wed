# Hana & Aly — Wedding Site

Two UI directions for the same wedding. Open `index.html` and pick one.

```bash
open /Users/alybarakat/Desktop/hana-aly-wedding/index.html
```

| File | What it is |
|---|---|
| `index.html` | Chooser page — links to all four variants |
| `romantic.html` | **A — Romantic Cairo, full.** Ivory paper, gold script, peonies, moorish ogee arch |
| `romantic-short.html` | **A — Romantic, condensed.** Hero, invitation, countdown, 3-field RSVP |
| `luxe.html` | **B — Cinematic Dark Luxe, full.** Night at the palace, gold dust, display capitals |
| `luxe-short.html` | **B — Dark Luxe, condensed.** Hero, invitation, countdown, 3-field RSVP |
| `assets/` | Photography and botanical plates |

No build step, no dependencies, no framework. Each variant is one self-contained
HTML file (CSS + JS inline). Drop the folder on Netlify, Vercel, GitHub Pages, or
any static host and it works. Fonts load from Google Fonts.

## Putting it online

> **Do not host this on Netlify.** Egyptian ISPs (WE, Vodafone, Orange, Etisalat)
> blocked Netlify around late June 2026. Every `*.netlify.app` site — and custom
> domains pointed straight at Netlify's IPs — times out in Egypt unless the visitor
> is on a VPN. Since essentially the whole guest list is in Cairo, this rules it out.
> Current deploy `lucent-tanuki-a0cc91.netlify.app` works fine everywhere else, so
> it's usable for showing people abroad, but not for the invitation itself.

The same risk applies to any free wildcard subdomain — `*.pages.dev` is blocked in
Türkiye and Russia, `*.vercel.app` in several countries. National filters blanket-ban
them because anyone can host anything there. **The durable fix is your own domain
served through Cloudflare**, whose IPs are too widely used to blanket-block.

### Recommended: custom domain on Cloudflare Pages

1. Buy a domain (`hanaandaly.com` or similar) — Cloudflare Registrar sells at cost,
   roughly $10/year, and keeps domain + DNS + hosting in one account.
2. Create a free Cloudflare account, go to **Workers & Pages → Create → Pages →
   Upload assets**, and drag in `hana-aly-wedding.zip`.
3. Under the project's **Custom domains**, add your domain. Cloudflare wires up DNS
   and TLS itself, and serves through its own proxied edge.

### Alternative: keep Netlify, put Cloudflare in front

If you'd rather not move the deploy: add your domain to Cloudflare, point a CNAME at
the Netlify site, and switch the record to **Proxied** (orange cloud). Visitors then
hit Cloudflare's IPs instead of Netlify's, which is the documented workaround for the
Egypt block. One more moving part, and it still depends on Netlify behind the scenes.

### Link previews

`og:` tags and a 1200×630 `assets/share.jpg` are in place, so pasting the link into
WhatsApp shows a photo card instead of a bare URL. **The URLs in those tags are
absolute and currently point at the Netlify domain** — search all three HTML files
for `lucent-tanuki-a0cc91.netlify.app` and replace it with the real domain when you
move, or the preview image will break.

## Sections

**Full variants:** hero + live countdown → invitation → countdown → venue &
details → schedule → good-to-know → RSVP → footer.

**Short variants:** hero → invitation → countdown → RSVP → footer. The RSVP is
cut to three fields — name, optional phone, and Attending / Attending with +1.

> Note: the short form has no way to decline. Everyone who opens it is choosing
> between coming alone and coming with someone. If you want a "can't make it"
> option, say so and I'll add a third choice.

## Still to confirm

These are placeholders — tell me the real values and I'll swap them in:

- **Schedule times.** 5:00 arrive / 6:00 Katb El-Kitab / 7:00 zaffa / 8:00 dinner / 10:00 dancing.
- **RSVP deadline** — currently 15 October 2026.
- **Dress code** — "Garden formal" (A) / "Black tie optional" (B).
- **The invitation artwork still reads "TWENTY TWENTY FOUR".** It is now the
  WhatsApp preview image on every page, so it is the first thing guests see.
- **Address** — 1 Al Saraya St, Al Manyal, Cairo.
- **Child-free line** — remove it if that's not your plan.

## RSVP

The form is **UI only**. It validates name and email, hides the guest/menu
questions when someone declines, and shows a thank-you card — but nothing is
saved anywhere yet. Wiring it up is the next step; options include Formspree or
Google Forms (zero backend), or a small API writing to a sheet or database if you
want an admin view of replies.

## Countdown

Targets `2026-11-21T17:00:00+02:00` (Cairo, UTC+2 in November). Change the
`TARGET` constant near the top of the script block in each file if the time moves.

## Notes

- Responsive from ~320px up; layouts switch to two columns at 60–64rem.
- Honours `prefers-reduced-motion` — all animation, parallax and the particle
  canvas switch off for anyone who's asked their OS for less motion.
- Keyboard accessible, with a skip link, visible focus rings, labelled fields and
  a live-region countdown.

## Image credits

All photographs are of the actual venue — Mohamed Ali (Manial) Palace, Cairo —
from [Wikimedia Commons](https://commons.wikimedia.org), used under their
respective Creative Commons licences:

- `arcade.jpg`, `mosque.jpg` — *Prince Muhammad Ali Palace Manial Cairo* series
- `garden-arcade.jpg`, `share.jpg` — *Jardins du Al-Manyal Palace Museum*
- `fountain.jpg` — *The colors fountain* (the marble fountain in the palace garden)
- `tilework.jpg` — *Mohamed Ali's Palace, Manial, Cairo Egypt*

Botanical plates are public domain, from Pierre-Joseph Redouté's
*Choix des plus belles fleurs* (1827):

- `peony-blush.jpg` — Plate 39, *Pivoine de la Chine*
- `peony-coral.jpg` — Plate 134, *Paeonia tenuifolia*
- `campanula.jpg` — Plate 106, *Campanule dentelée*

Before this goes public, check each file's licence page on Commons and add
attribution where the licence requires it (most are CC BY-SA and need credit).
The footer currently carries a general Wikimedia Commons credit.
