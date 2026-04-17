# Cert Image Drop Zone

Drop source cert images here. Any format (JPG, PNG, PDF scan). Any size — larger is better, the optimizer handles sizing.

## Naming convention

Use the `id` from `data/certificates.json` as the filename:

```
<id>.<ext>
```

e.g. `oxford_elp.jpg`, `wa_hrwl.png`, `stjohn_advfa.pdf`.

Any extension you have is fine. JPG preferred for photos/scans. PNG for anything with transparency. PDF works (converted during optimize step).

## What happens after you drop files

I run:

```
optimize_images({ dir: 'assets/img-source/', preset: 'cert' })
```

Generates for each source:
- `<id>-600.jpg` (card display)
- `<id>-1600.jpg` (modal zoom)
- `<id>-600.webp`
- `<id>-1600.webp`

Outputs land in `assets/img/certs/`. Then I update `data/certificates.json` with the paths and commit. CF Pages auto-deploys.

## Priority 1 — Current certs missing images (5)

| id | Cert | Issuer |
|---|---|---|
| `oxford_elp` | Executive Leadership Programme | Saïd Business School, Oxford |
| `wa_hrwl` | High Risk Work Licence (7 classes) | WorkSafe WA / DEMIRS |
| `stjohn_advfa` | Advanced First Aid (HLTAID014-016) | St John Ambulance QLD |
| `citc_fl` | Licence to Operate Forklift | Construction Industry Training Centre |
| `citc_wc` | Construction Induction (White Card) | Construction Industry Training Centre |

## Priority 2 — Complete certs missing images (17)

| id | Cert | Issuer |
|---|---|---|
| `tou_compnet` | Discovering Cisco Computer Networks | The Open University |
| `ncass_haccp` | HACCP Certification Level 1 & 2 | NCASS (UK) |
| `ncass_fh2` | Food Hygiene Training Level 2 | NCASS (UK) |
| `ncass_fh1` | Food Hygiene Training Level 1 | NCASS (UK) |
| `cc_webdev` | Web Development Career Path | Codecademy |
| `cc_foundations` | Code Foundations Career Path | Codecademy |
| `cc_html` | Learn HTML | Codecademy |
| `cc_css` | Learn CSS | Codecademy |
| `cc_js` | Learn JavaScript | Codecademy |
| `cc_react` | Learn React | Codecademy |
| `cc_node` | Learn Node.js | Codecademy |
| `cc_sql` | Learn SQL | Codecademy |
| `cc_git` | Learn Git & GitHub | Codecademy |
| `cc_express` | Learn Express.js | Codecademy |
| `cc_responsive` | Learn Responsive Design | Codecademy |
| `cc_commandline` | Learn the Command Line | Codecademy |
| `ss_adobe` | Adobe Creative Cloud Design Suite | Skillshare |

## Priority 3 — Issuer logos (2)

These go in `assets/img-source/` too, but use `logo-` prefix:

| filename | For |
|---|---|
| `logo-oxford.svg` (or `.png`) | Oxford / Saïd Business School |
| `logo-worksafe-wa.svg` (or `.png`) | WorkSafe WA |

Source hints: issuer website favicons, Credly badges, or a screenshot of the logo from the issuer's homepage. SVG preferred if you find it.

## Don't worry about

- Cropping — tool preserves aspect ratio
- File size — as long as under ~20MB each, no issues
- Quality — start with the biggest/sharpest version you have
- Where in the repo they end up — tool handles that

## Where to source images

- **Oxford ELP** — Credly badge if you have one, or programme page on Oxford Saïd website
- **WA HRWL** — photo of the physical licence card (both sides if combined)
- **St John First Aid** — certificate PDF from St John's student portal
- **Forklift / White Card** — photo of the physical card(s)
- **Codecademy** — screenshot of the certificate from Codecademy's "My Profile → Certificates"
- **Open University** — OpenLearn transcript/badge
- **NCASS HACCP / Food Hygiene** — PDF from NCASS dashboard
- **Skillshare Adobe CC** — screenshot of the completion certificate

Some issuers email the cert PDF on completion — search your inbox for "certificate", "certification", "successfully completed" from the issuer domain.

## Batch approach

You don't need all at once. Any batch of 2+ I can process. Drop files + tell me when ready. Partial progress is better than waiting for a perfect batch.
