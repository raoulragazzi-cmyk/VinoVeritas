# PROJECT FINGERPRINT — VinoVeritas

> Read this file before any write, migration or deploy. If live infrastructure disagrees with this file, STOP and re-verify read-only.

## Identity
- Project: **VinoVeritas**
- Repository: `raoulragazzi-cmyk/VinoVeritas`
- Governance branch: `governance/bootstrap`
- Intended canonical branch: `main`
- Current historical default branch: `splendoria.vip`
- Repository visibility: public — production source import remains gated pending privacy decision

## Canonical deployment filenames — NON-NEGOTIABLE
For every VinoVeritas delivery, hotfix, recovery file or upload package, use these exact filenames only:
- Backend/API Worker `vinoveritas-api` → **`VinoVeritas-Worker.txt`**
- Frontend/assets Worker `vinoveritasstudioweb` → **`index.html`**

Do not create user-facing VinoVeritas deploy files with alternative names such as `finale`, `fix`, version numbers, `API_WORKER`, `frontend`, `stable`, or similar suffixes/prefixes. Internal working copies may have temporary names, but before handoff they MUST be normalized to the two canonical filenames above.

Before telling the owner which file to upload, explicitly verify:
- `VinoVeritas-Worker.txt` is JavaScript Worker source and targets only `vinoveritas-api`;
- `index.html` is HTML frontend source and targets only `vinoveritasstudioweb`.

Never instruct the owner to paste `index.html` into `vinoveritas-api` or `VinoVeritas-Worker.txt` into `vinoveritasstudioweb`.

## Cloudflare production fingerprint
- Account ID: `9ea664e4c34f649045f64024e0db52e1`
- API Worker: `vinoveritas-api`
- Frontend/assets Worker: `vinoveritasstudioweb`
- API domain: `api.vinoveritas.studio`
- Studio domain: `studio.vinoveritas.studio`
- D1 production: `vinoveritas-db`
- D1 production ID: `144b8f51-40d4-4dee-b0b7-665476439f71`
- R2: live name must be re-verified. Historical docs say `vinoveritas-media`; a later inventory reported `vinoveritas-clienti`. Never choose one by assumption.
- Health: historical endpoint `/health`; live re-verification required.

## Protected areas
### FROZEN BY DEFAULT
- regulatory e-label;
- compliance data and regulatory presentation;
- stable public regulatory QR/URL behavior.

Compliance and marketing must remain separate. Do not insert promotional content into the regulatory e-label.

## Auth incident — 2026-08-19
A production login regression was reported after the Worker used PBKDF2 with 310000 iterations while the serving runtime accepted at most 100000. The login path attempted the unsupported derivation before its legacy fallback, so the fallback was unreachable. A minimal hotfix restoring the supported 100000-iteration behavior was manually uploaded by the owner and the owner reported that login worked again.

Follow-up requirements:
- capture the exact current live Worker before the next production deployment;
- turn this incident into an automated auth regression test;
- do not redesign password storage during an incident hotfix;
- plan any future password-hardening migration separately and version it explicitly.

## Deploy gate
Do NOT deploy production unless all are true:
1. repository = VinoVeritas;
2. target Worker = `vinoveritas-api` or explicitly named VinoVeritas frontend worker;
3. target domain is a VinoVeritas domain;
4. target D1 ID matches `144b8f51-40d4-4dee-b0b7-665476439f71` for production DB operations;
5. exact live source/bindings were captured and compared with the proposed source;
6. e-label protected area is untouched unless explicitly authorized;
7. rollback target is known;
8. applicable tests are green;
9. handoff filenames comply with the canonical naming rule (`VinoVeritas-Worker.txt` / `index.html`).

If any fingerprint is ambiguous, STOP rather than deploy.
