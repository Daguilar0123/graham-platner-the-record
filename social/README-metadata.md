# Social image metadata — graham-platner-the-record

Six social cards for the three record-site pages. Attribution metadata is embedded IN each PNG
(tEXt chunks: Title, Description, Author, Copyright with attribution URL) — verify with
`exiftool <file>` — and duplicated in a JSON sidecar named `<image filename>.json`.

All images: © 2026 Daniel Ismael Aguilar · https://grownfromconcrete.org

| Image | Page it belongs to | Title |
|---|---|---|
| og-1200x630.png | index.html (og:image) | The Platner Record — 156,084 → 31 days → 0 |
| og-1200x630-fifield.png | fifield-kavanaugh.html (og:image) | The Fifield–Kavanaugh File — archival specimen card |
| og-1200x630-questions.png | the-questions.html (og:image) | Why is no one calling for an investigation? — editorial card |
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
