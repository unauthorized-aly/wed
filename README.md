# Hana & Aly — Wedding Site

Two UI directions for the same wedding. Open `index.html` and pick one.

```bash
open /Users/alybarakat/Desktop/hana-aly-wedding/index.html
```

| File | What it is |
|---|---|
| `index.html` | Chooser page — links to all four variants |
| `romantic.html` | **A — Romantic Cairo, full.** Rustic orange, the H&A monogram, botanical leaves, foil-line arch |
| `romantic-short.html` | **A — Romantic, condensed.** Hero, invitation, countdown, 3-field RSVP |
| `luxe.html` | **B — Cinematic Dark Luxe, full.** Deep olive, the H&A monogram, gold dust, display capitals |
| `luxe-short.html` | **B — Dark Luxe, condensed.** Hero, invitation, countdown, 3-field RSVP |
| `garden-light.html` | **Light garden, full.** Watercolour pergola, palace toile, artwork instead of photos |
| `garden-light-short.html` | **Light garden, condensed.** Hero, invitation, countdown, 3-field RSVP |
| `garden-orange.html` | **Orange garden, full.** Palace arches, rust damask, artwork instead of photos |
| `garden-orange-short.html` | **Orange garden, condensed.** Hero, invitation, countdown, 3-field RSVP |
| `assets/` | Logos and artwork (`assets/art/`), plus older photos and plates |

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

## Theme

The visual language is the H&A logo sheet. The planner's PDF is a colour and pattern
reference only: no slide styling and no 3D renders appear on the site.

| Name | Hex | Used for |
|---|---|---|
| Rustic orange | `#8C3214` / band `#7A2A10` | Romantic background (the centre-right logo tile) |
| Deep olive | `#2D2A14` / `#23210F` | Dark Luxe background (the top-right logo tile) |
| Peach beige | `#E8BA98` | Ornament, labels |
| Bronze | `#A4632F` | Logo on cream, accents |
| Cream | `#F6EADB` / card `#F3E8DA` | Text on dark grounds, the RSVP card in Romantic |

Logo files: `assets/logo-on-rustic.svg`, `logo-on-olive.svg`, `logo-on-cream.svg`.
They are vector traces of the 1536px logo sheet, with a few small leaves redrawn by
hand. If the designer has the original vector, drop it in under the same names.

Type: Cormorant Garamond and Jost in Romantic, Italiana added in Dark Luxe. The corner
leaves are inline SVG drawn to match the monogram, and open as you scroll.

## Garden versions

`index.html` links only `garden-light-short.html` and `garden-orange-short.html`.
They run: hero, invitation with the dance floor, countdown, venue with a Google Maps
preview that opens the couple's Maps link, footer. RSVP is a bar fixed to the bottom of the screen (name, Attending /
Attending with +1) that appears once scrolling starts. Replies go to the Google Sheet "Hana & Aly RSVPs" on aly.m.barakat@gmail.com through an Apps Script web app (`RSVP_URL` in each page). A repeat reply under the same name updates that row.

The pages open on a closed-doors entrance: tapping parts the doors and starts the
music, because browsers block sound until a tap. If nobody taps, the doors open after
8 seconds without sound, and the music button (top right) still works.

Music: `assets/audio/aloula.m4a`, supplied by the couple (`aloula_EWxd4WxR.mp3`), with the silent ending trimmed and compressed to 128 kbps AAC for phones.

Phones: the orange frame is drawn to a canvas behind the closed doors, so only the plain middle of `o-arch-tall.webp` flexes, the arches, columns and flowers always fit, and it all appears at once. The doors wait for the art to decode, for up to 4 seconds. The dance floor turns from CSS (`animation-timeline`) where the browser supports it, otherwise from the scroll handler. Check phone changes in real Safari, since Chrome's phone emulation has no collapsing toolbar.

Languages: English by default; add `?lang=ar` to a link for Arabic. There is no language button. The Arabic is light Egyptian, not formal. It lives in the `AR` table in each page's script, matched to `data-i18n` attributes. Sheet labels stay in English in both languages.

Link preview: `assets/share-palace.jpg` (1200x630). The `og:` tags use full addresses for unauthorized-aly.github.io/wed/, so update them if the site moves.

All other pages remain in this folder but aren't linked from the landing page. The
artwork is in `assets/art/` (`l-` light, `o-` orange); `dancefloor.webp` comes from
the planner's PDF.

## Sections

**Full variants:** hero + live countdown → invitation → countdown → venue &
details → schedule → good-to-know → RSVP → footer.

**Short variants:** hero → invitation → countdown → RSVP → footer. The RSVP is
cut to three fields — name, optional phone, and Attending / Attending with +1.

> Note: the short form has no way to decline. Everyone who opens it is choosing
> between coming alone and coming with someone. If you want a "can't make it"
> option, say so and I'll add a third choice.

## Still to confirm

- **RSVP deadline has passed.** The pages still say 15 October 2026, a placeholder. Replace it.

These are placeholders — tell me the real values and I'll swap them in:

- **Schedule times.** 5:00 arrive / 6:00 Katb El-Kitab / 7:00 zaffa / 8:00 dinner / 10:00 dancing.
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

- `marble.webp`: your own photo of the pergola, used in the full variants' venue section.
- `invitation-share.jpg`: your painted invitation, still the link preview. It reads 2024
  and uses the old colours.

Nothing else in `assets/` apart from the logos is used by any page. That includes
`entrance.webp`, `garden.webp` and the old Wikimedia and Redouté files, which can be
deleted or brought back as you prefer.
