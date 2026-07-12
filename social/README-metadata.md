# Social image metadata — graham-platner-the-record

Six social cards for the three record-site pages. Attribution metadata is embedded IN each PNG
(tEXt chunks: Title, Description, Author, Copyright with attribution URL) — verify with
`exiftool <file>` — and duplicated in a JSON sidecar named `<image filename>.json`.

All images: © 2026 Daniel Ismael Aguilar · https://grownfromconcrete.org

| Image | Page it belongs to | Title |
|---|---|---|
| og-1200x630.png | the-record.html (og:image) | The Platner Record — 156,084 → 31 days → 0 |
| og-1200x630-fifield.png | fifield-kavanaugh.html (og:image) | The Fifield–Kavanaugh File — archival specimen card |
| og-1200x630-questions.png | index.html — site front door (og:image) | Why is no one calling for an investigation? — editorial card |
| x-1600x900.png | any page, X/Twitter post | 156,084 — 31 days later: 0 |
| ig-1080x1080.png | Instagram square | Every box is unchecked |
| ig-1080x1350.png | Instagram portrait | Three waves — the timing record |

For fuller EXIF/XMP/IPTC embedding (per HANDOFF.md §5), run exiftool with the sidecar values, e.g.:
`exiftool -Artist="Daniel Ismael Aguilar" -Copyright="© 2026 Daniel Ismael Aguilar" -XMP-xmpRights:WebStatement="https://grownfromconcrete.org" -XMP-cc:AttributionURL="https://grownfromconcrete.org" <file>`

## Animated teasers (added 2026-07-12)

| Image | Motif | Sidecar |
|---|---|---|
| boxes-teaser-animated.gif | five unchecked boxes → “Every box is unchecked.” | boxes-teaser-animated.gif.json |
| mandate-teaser-animated.gif | counter to 156,084 → “31 days later: 0” | mandate-teaser-animated.gif.json |
| waves-teaser-animated.gif | three wave bands → the timing quote | waves-teaser-animated.gif.json |

Each GIF carries an embedded comment block: “(c) 2026 Daniel Ismael Aguilar - https://grownfromconcrete.org - The Platner Record”. 640×640, infinite loop.

## YouTube thumbnails (added 2026-07-12)

| Image | Argument | Sidecar |
|---|---|---|
| yt-thumb-demanded-1280x720.png | Q1 — withdrawal demanded, investigation never | yt-thumb-demanded-1280x720.png.json |
| yt-thumb-evidence-1280x720.png | Q2 — “reviewed the evidence” vs testing it | yt-thumb-evidence-1280x720.png.json |

## Revision 2026-07-12 (clarity pass)

- All “his” attributions now use Platner’s name; “verification boxes” language replaced with the explicit question “CHARGED? COURT FINDING? INDEPENDENTLY VERIFIED?”
- boxes-teaser-animated.gif rebuilt as a ledger (5 allegations, 2 named accusers) to prevent the “five accusers” misread.
- og-1200x630-fifield.png adds the method line (automated archive sweep, human-checked).
- NEW three-part series: questions-part1/2/3-1200x630.png + og-1200x630-questions.png as series cover. Part 3 cites 17-A M.R.S. §8(2-A) (20 years, clock to ~2041).

## Revision 2026-07-12b (marketing pass)

- NEW banner-site-1500x500 (site-promotion banner; also fits X/Twitter header).
- NEW the-money-1200x630 (contrast card linking the campaign-finance ledger).
- Vector masters: every card revised in this pass ships as .svg next to its .png — edit the SVG, not the PNG. Photo composites (yt-thumb-*) and GIFs are raster-only.
- boxes-teaser-animated.gif reworded — allegation specifics removed from marketing copy.
- questions-part3 + series cover: 2041 framing removed, replaced with the “then charge him” argument.
- og-1200x630-fifield: explicit 2018-vs-2026 contrast, “We have the receipts.”
- ig-1080x1080 closing line: “Allegations written as allegations. Denials written as denials.”

## Revision 2026-07-12c (final metadata pass)

- SVG masters now exist for EVERY still card (11 .svg files). yt-thumb-* are photo composites (raster-only); GIFs are raster by format.
- Every PNG carries embedded tEXt: Title, Description, Alt, Author, Copyright (+attribution URL), Keywords (SEO), Software.
- Every SVG carries <title>, <desc> (alt text), and an RDF/Dublin Core metadata block (creator, rights, subject keywords, date, source).
- Banner footer now reads “draw your own conclusions · our bias made clear”.
