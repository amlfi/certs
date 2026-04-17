# TODO — Things Anthony Needs to Hunt For

> Items the Claude agent cannot find/decide alone. Blocks full polish until resolved.

**Live site**: https://certs.makes.events
**Generated**: 2026-04-17

---

## Priority 1 — Current certs missing images (visible, public-facing)

These are active/in-progress credentials. Most visible on the homepage.

- [ ] **Executive Leadership Programme** — Saïd Business School, University of Oxford (Mar 2026) `[business]`
- [ ] **High Risk Work Licence (7 classes)** — WorkSafe WA / DEMIRS (Feb 2024) (expires Feb 2029) `[licenses]`
- [ ] **Advanced First Aid (HLTAID014-016)** — St John Ambulance QLD (Aug 2024) `[safety]`
- [ ] **Licence to Operate Forklift** — Construction Industry Training Centre (Nov 2011) `[licenses]`
- [ ] **Construction Induction (White Card)** — Construction Industry Training Centre (Feb 2011) `[licenses]`

## Priority 2 — Complete certs missing images

Still visible in the catalog, but lower priority than current ones.

- [ ] **Discovering Cisco Computer Networks** — The Open University (Jul 2020) `[networking]`
- [ ] **HACCP Certification Level 1 & 2** — Nationwide Caterers Association (UK) (Jun 2020) `[safety]`
- [ ] **Food Hygiene Training Level 2** — Nationwide Caterers Association (UK) (Jun 2020) `[safety]`
- [ ] **Food Hygiene Training Level 1** — Nationwide Caterers Association (UK) (Jun 2016) `[safety]`
- [ ] **Web Development Career Path** — Codecademy (Jul 2020) `[webdev]`
- [ ] **Code Foundations Career Path** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn HTML** — Codecademy (May 2020) `[webdev]`
- [ ] **Learn CSS** — Codecademy (May 2020) `[webdev]`
- [ ] **Learn JavaScript** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn React** — Codecademy (Jul 2020) `[webdev]`
- [ ] **Learn Node.js** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn SQL** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn Git & GitHub** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn Express.js** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn Responsive Design** — Codecademy (Jun 2020) `[webdev]`
- [ ] **Learn the Command Line** — Codecademy (May 2020) `[webdev]`
- [ ] **Adobe Creative Cloud Design Suite** — Skillshare (May 2020) `[design]`

## Priority 3 — Missing issuer logos

- [ ] Logo for **Oxford** (used by: Executive Leadership Programme)
- [ ] Logo for **WorkSafe WA** (used by: High Risk Work Licence (7 classes))

## Priority 4 — Missing courseUrl (verification links)

- [ ] Public course URL for **Executive Leadership Programme** — Saïd Business School, University of Oxford
- [ ] Public course URL for **High Risk Work Licence (7 classes)** — WorkSafe WA / DEMIRS
- [ ] Public course URL for **Advanced First Aid (HLTAID014-016)** — St John Ambulance QLD
- [ ] Public course URL for **Safety for Managers** — National Compliance & Risk Qualifications
- [ ] Public course URL for **Discovering Cisco Computer Networks** — The Open University
- [ ] Public course URL for **HACCP Certification Level 1 & 2** — Nationwide Caterers Association (UK)
- [ ] Public course URL for **Food Hygiene Training Level 2** — Nationwide Caterers Association (UK)
- [ ] Public course URL for **Food Hygiene Training Level 1** — Nationwide Caterers Association (UK)
- [ ] Public course URL for **Certificate II Electrotechnology** — TAFE South Australia

---

## Brand (Makes.Events) — still open

- [ ] **Confirm primary brand colours** — logo variants (Sunrise/Sunset/Midday/Midnight) imply a palette; exact hex ideally from Steve Grant's source spec
- [ ] **Read Discovery Questionnaire** — `_Makes.Events/Brand/Sussudio & Makes Events __ Discovery Questionnaire.docx` (dated ~April 2019 — confirm still current)
- [ ] **Typography decision** — Sora + DM Sans is the working pair. Confirm this is the official Makes.Events typeface pairing
- [ ] **Tagline / positioning statement** — for hero + meta description

## Infrastructure decisions — resolved or pending

- [x] **Certs domain**: certs.makes.events (Phase 1) → makes.events/certs (Phase 2 when makes.events site rebuilt)
- [x] **Hosting**: Cloudflare Pages (migrated from GitHub Pages)
- [x] **Default branch**: main (renamed from master)
- [ ] **Airtable migration** — JS already stubbed for it; do when stable enough to move off JSON
- [ ] **Delete old amlfi.github.io/certs GitHub Pages site** — once CF site is confirmed stable
- [ ] **Image hosting strategy** — currently committing images to repo; move to Cloudflare R2 if repo gets large

## Future polish (non-blocking)

- [ ] Light/dark mode toggle (currently dark-only)
- [ ] Extract brand tokens from inline Tailwind config → `claude-kit/themes/brands/makes-events/brand.json`
- [ ] Cert expiry warning UI (e.g. '< 6 months to expiry' highlight)
- [ ] Verification URLs (Credly, LinkedIn Learning links) where available
- [ ] Short description / 'why it matters' per cert
