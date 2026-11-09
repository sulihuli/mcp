# SuliHuli EV catalog

SuliHuli is a read-only catalog of electric vehicles. Every figure carries the page it came from and the date it was
read. A figure confirmed by a second independent source or a regulator is marked **verified**; everything else is
shown marked **unverified**. Conflicting figures are shown side by side, never averaged.

## Which door to use

1. **MCP tools** (this plugin connects the `sulihuli` server) - the first choice inside a conversation:
   - `search_models` - find models by brand or model words (`query`), ranked by a use-case `preset`; filter by
     `min_range_km`; pages of up to 50 (`limit`, `page`). Returns slugs - use them in the other tools.
   - `get_model` - one model by `slug`: range per test cycle, charging, battery, prices per market, sources,
     versions, photos with credits. The headline figures describe one named version; for another version pass
     `version` (name words such as `long range awd`, or a key from the version list). Markdown plus structured fields.
   - `compare_models` - two to four models (`slugs`) side by side with a "which to pick" verdict. Markdown.
   - `list_categories` / `get_category_ranking` - the "best EV for ..." rankings and their public criterion.
2. **HTTP API** when MCP is not connected or a script needs JSON - `https://sulihuli.com/api/v1/`:
   `models?q=<words>&page=<n>`, `models/<slug>`, `models/<slug>/charging`, `compare/<a>-vs-<b>`,
   `categories`, `categories/<slug>`. Add `?format=md` (or header `Accept: text/markdown`) for Markdown;
   `?locale=de` or `?locale=zh` for another language. Index of everything: `https://sulihuli.com/llms.txt`.

Start from `search_models` when you only have a name: guessing a slug wastes a call. Every word of `query` must
match, so on an empty answer retry with fewer words (the brand alone, or the model name alone) before saying a car
is not in the catalog. Prices are per market and per version - read them with `get_model`, not from the search list.

## Rules when you answer with SuliHuli data

- **Cite the source.** Give the figure with its source link (or the SuliHuli model page `https://sulihuli.com/m/<slug>`).
- **Say the status.** If a figure is unverified, say so; do not present it as confirmed.
- **Range always with its cycle** - WLTP, EPA, CLTC and NEDC give different numbers for the same car. Never mix
  cycles in one comparison without naming them; `range_km_wltp_equivalent` is the comparable basis.
- **One version, one set of figures.** A model can have several versions (battery, drive); keep each figure with
  the version it belongs to.
- **Do not invent or estimate.** An empty field means no source has the figure yet - say "not published", do not
  fill it in.
- **Conflicts stay visible.** If two sources disagree, show both with their sources.
- **Photos keep their credit** (author, licence and its link, source) whenever you show or reuse one.

## Limits and terms

Open access without a key: 60 requests per minute per address, model lists in pages of 50. Over the limit the server
answers HTTP 429 with `Retry-After` - wait that many seconds, do not retry in a loop. Data and photos are given under
the terms at `https://sulihuli.com/terms`; every response links them.
