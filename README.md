# HMC CIS/ARCS Campus Service Finder — prototype

This is a **local-only, static prototype** for faculty and staff. It was not deployed to Pathify, Vercel, or an existing HMC site.

## Try it

Open `index.html` in a browser. Search by service name or task (for example, `record lecture`, `accessible PDF`, `AI tools`), use a category chip, and open an official HMC service page. All searches and filters execute in the browser. No build command, account, API key, AI service, tracking, or backend is required.

To test it with a local web server, from this folder run `python3 -m http.server 8000` and open `http://localhost:8000/`.

## Content and sources

- Official A–Z directory: https://www.hmc.edu/cis/services/
- Official category directory: https://www.hmc.edu/cis/services/cis-services-by-category/
- The curated prototype contains **24** individually linked services, selected for faculty/staff use.
- The service titles and destination pages were cross-checked against the official directory on **November 18, 2026**; descriptions are intentionally short editorial summaries. Category groupings were adapted for the widget, not presented as the college's exact taxonomy.
- Two destination pages (Duo and Google Drive) live directly under `/cis/` rather than `/cis/services/` and are linked accordingly.
- This is a snapshot: update entries when CIS changes service pages. There is no background scraping or live sync.

## Pathify embedding guidance

1. **Confirm supported extension type with your Pathify administrator.** If an iframe/web content card is allowed, host this static HTML on an HMC-approved HTTPS endpoint and embed that URL. Do **not** paste the complete HTML into a widget that sanitizes scripts.
2. **Set a sensible widget size.** Start with a full-width card and ~550–700 px height, or link from a compact Pathify card to a larger service finder page. The layout adapts to narrower widths (one column under 520 px).
3. **Security configuration.** On the eventual hosting origin, set `Content-Security-Policy: frame-ancestors https://<approved-pathify-host>` to the *actual* approved Pathify domain(s), after verifying the embedding method. Pathify's own frame policy may also need to permit the hosted origin. Never use unrestricted `*` frame ancestors. Do not guess hostnames.
4. **Accessibility.** The UI supports keyboard controls, labeled search input, visible focus, responsive cards, reduced-motion preference, a live result count, and explanatory link labels. Complete a human keyboard/screen-reader test before production.
5. **Governance.** Assign a CIS/ARCS content owner and establish a review schedule (for example, quarterly) to detect broken links, renamed services, and changed descriptions. This avoids quietly serving stale service information.
6. **Privacy.** Search text remains in the user's browser; the prototype makes no API requests. Clicking a service opens an official HMC website, where that site's own policies apply. Avoid storing or submitting free-text queries in production unless deliberately reviewed and approved.

## Edit services

In `index.html`, find `const services`. Each row contains:

`[name, category, description, search keywords, official URL path, icon]`

Use one of the existing values in the `categories` array. For official links, paths are resolved relative to `https://www.hmc.edu/cis/services/`; `../` can point to an official page in `/cis/`. Verify every new URL in the browser before publishing.

Keyword matching is local and deterministic (all query terms must match, with a few manually curated synonyms). It is **not** a generative or full semantic search engine. Add common faculty/staff vocabulary and synonyms when you learn how people search.

## Recommended production acceptance checklist

- [ ] CIS/ARCS verifies descriptions, categories, and the intended service scope.
- [ ] All official service links are rechecked.
- [ ] Pathify supports the selected embed approach and its mobile rendering.
- [ ] HMC security/accessibility reviewers approve production hosting and CSP.
- [ ] Keyboard and screen-reader testing is completed.
- [ ] The approved host and editor/maintenance process are documented.

**No deployment was performed.**
