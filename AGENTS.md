# AGENTS.md — VinoVeritas

These instructions apply to any AI coding agent or automated contributor working in this repository.

## Mandatory project identity gate

Before any write, migration, Cloudflare change or deploy, read `PROJECT_FINGERPRINT.md` and verify that the repository, target Worker, target domain and production D1 ID all match VinoVeritas. If live infrastructure disagrees with the fingerprint, STOP and perform read-only verification first.

Never infer the project from UI appearance, filenames or nearby conversation context.

## Mandatory canonical filenames

Every user-facing VinoVeritas deployment file MUST be handed off with exactly one of these two names:

- **`VinoVeritas-Worker.txt`** → only for Cloudflare Worker **`vinoveritas-api`**
- **`index.html`** → only for Cloudflare Worker/assets **`vinoveritasstudioweb`**

Never give the owner alternative deployment filenames such as `final`, `fix`, `stable`, version numbers, `API_WORKER`, `frontend`, or other variants. Temporary internal filenames are allowed only during development; normalize them before handoff.

Before presenting a download link, verify the file type and target:
- `VinoVeritas-Worker.txt` must contain Worker JavaScript, not HTML;
- `index.html` must contain frontend HTML, not Worker source.

Never tell the owner to paste `index.html` into `vinoveritas-api`. Never tell the owner to upload `VinoVeritas-Worker.txt` to `vinoveritasstudioweb`.

## Current repository state

VinoVeritas is in controlled bootstrap. Cloudflare live remains authoritative until the exact deployed Worker/frontend are captured, hashed, compared and imported according to Issue #1.

Do not treat historical copies as deployable source.

## Non-negotiable protected area

### Regulatory e-label — FROZEN BY DEFAULT

Do not modify regulatory e-label behavior, schema, QR resolution, public route, ingredients/nutrition/compliance rendering or regulatory language behavior unless the product owner explicitly authorizes that specific change.

Never mix marketing, sales CTA, Sommelier content or promotional tracking into the regulatory e-label layer.

Bootstrap/import work must reproduce live e-label behavior exactly; bootstrap is not permission to refactor it.

## Bootstrap safety

- Do not add deployable production source while the repository is public.
- Do not add production secrets, `.env`, `.dev.vars`, database dumps or customer exports to Git.
- Do not create Cloudflare deploy automation until the verified production baseline is in Git and staging exists.
- Do not deploy historical `REFERENCE ONLY` files.
- Do not mutate production D1/R2 as part of bootstrap.

## Engineering workflow

For normal changes after bootstrap:
1. understand the product request and classify risk;
2. create/update an Issue when the change is not trivial;
3. work on a dedicated branch;
4. add/adjust regression tests;
5. open a PR with risk, data, rollback and customer impact;
6. pass CI;
7. validate on isolated staging with synthetic data;
8. repeat the Project Identity Gate immediately before production deploy;
9. deploy production only after the release gate;
10. run health/public-route acceptance and record rollback target.

## Release blockers

Stop rather than work around any of these:
- project fingerprint mismatch or ambiguity;
- cross-winery data access;
- regulatory QR/e-label route regression;
- compliance data loss or marketing injected into the regulatory layer;
- unverified payment unlock;
- staging bound to production customer data/resources by accident;
- secrets committed to Git;
- destructive D1/R2 action without explicit target, ownership check and recovery plan;
- VinoVeritas deployment file presented with a non-canonical filename or ambiguous target.

## Product invariants

Preserve the intended journey:
`winery/account -> wine/reference -> regulatory e-label -> Communication/Marketing -> Sommelier -> Analytics`

UI should converge on one canonical wine/reference concept and one obvious next action rather than duplicate CTAs.

For Communication Section 2, test each card end-to-end through its public page. `Eventi ed enoturismo` must validate the `PUBBLICA PAGINA EVENTO` route against the current live routing contract after baseline capture.

## Read first

Before changing protected or high-risk code, read:
- `PROJECT_FINGERPRINT.md`
- `docs/ENGINEERING_GOVERNANCE.md`
- `docs/PROTECTED_AREAS.md`
- `docs/ACCEPTANCE_MATRIX.md`
- `RELEASE_CHECKLIST.md`
- `SECURITY.md`

When these instructions conflict with an old chat/file/reference copy, the current repository governance and verified production baseline win.
