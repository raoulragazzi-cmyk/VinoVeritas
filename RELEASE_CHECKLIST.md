# VinoVeritas — Release Checklist

## 0. Bootstrap gate — mandatory before importing production source

- [ ] Cloudflare live Worker/frontend can be read and versioned.
- [ ] Current live source is captured byte-for-byte before any functional change.
- [ ] SHA-256 fingerprints are recorded and compared with historical candidates.
- [ ] Repository visibility is **private** before deployable production source is imported.
- [ ] No secret value, customer dump, D1 export, R2 object or credential is committed.
- [ ] `main` is the intended source-of-truth branch.
- [ ] Staging is isolated from production D1/R2 and domains.
- [ ] Deployment automation remains disabled until the verified baseline is reproducible.

## 1. Before implementation

- [ ] Requirement has observable acceptance criteria.
- [ ] Risk is classified: UI / auth / winery isolation / compliance / e-label / publishing / payment / AI / analytics / migration / destructive action.
- [ ] Regulatory e-label impact is explicitly declared.
- [ ] D1/R2/QR/public URL impact is explicitly declared.
- [ ] Rollback target is known.

## 2. Pull Request quality gate

- [ ] Work is on a dedicated branch.
- [ ] No secrets or production data are committed.
- [ ] Worker/frontend syntax and automated tests pass.
- [ ] Wrangler dry-run passes once deploy tooling is enabled.
- [ ] Migration reviewed if present.
- [ ] Mobile and desktop behavior checked for UI changes.
- [ ] PR states customer/compliance impact and rollback.

## 3. Staging acceptance

- [ ] Staging uses non-production D1/R2 resources.
- [ ] Registration/login/session works with test credentials.
- [ ] Winery ownership isolation is verified.
- [ ] Create/open/save reference flow works.
- [ ] Publish flow creates the expected stable public URL.
- [ ] Regulatory e-label route renders only approved regulatory information.
- [ ] Communication/marketing remains separated from the regulatory e-label layer.
- [ ] Sommelier uses approved wine data and does not invent regulated facts.
- [ ] Analytics records only intended test events.
- [ ] Destructive actions require confirmation and correct authorization.

## 4. Production promotion

- [ ] Last-known-good Git commit recorded.
- [ ] Current Cloudflare deployment/version recorded.
- [ ] D1 recovery point/export available for risky releases.
- [ ] R2 impact understood and backup/export strategy available where relevant.
- [ ] PR reviewed and merged from the approved baseline.
- [ ] Deploy originates from GitHub-controlled source, not an ad-hoc dashboard edit.

## 5. Post-deploy acceptance

- [ ] API health endpoint responds with the expected service/version.
- [ ] Studio login works.
- [ ] Existing winery/reference data remains visible to the correct account only.
- [ ] One existing published wine opens publicly.
- [ ] Existing QR still resolves to the same intended public route.
- [ ] Regulatory e-label content is unchanged unless the release explicitly approved a compliance change.
- [ ] Communication page works where affected.
- [ ] Sommelier works where affected.
- [ ] Analytics shows no obvious regression.
- [ ] Cloudflare logs show no new critical errors.
- [ ] Release/commit recorded as current production baseline.

## Rollback rule

Rollback to the last verified baseline instead of stacking hurried fixes if a release threatens winery isolation, authentication, data integrity, regulatory e-label correctness, existing QR/public URLs, payment state or production publishing.
