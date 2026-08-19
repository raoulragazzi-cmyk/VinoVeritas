# VinoVeritas — End-to-End Acceptance Matrix

This matrix is the minimum acceptance suite for the verified production baseline and all future releases.

## A. Account and winery

| Flow | Expected result | Risk |
|---|---|---|
| Register / login | Session created only for valid account | High |
| Logout / session expiry | Protected data no longer accessible | High |
| Load winery profile | Correct winery only | High |
| Cross-winery URL/API attempt | Denied server-side | Release blocker |

## B. Wine/reference lifecycle

| Flow | Expected result | Risk |
|---|---|---|
| Create wine/reference | One canonical reference is created | High |
| Reopen reference | Same data and identity are loaded | Medium |
| Edit allowed fields | Persist once, no duplicate reference | High |
| Publish | Stable public URLs generated | High |
| Repeat publish | No accidental duplicate or route drift | High |

Terminology in UI should converge on one canonical concept. The customer should see one obvious next action instead of duplicate CTAs.

## C. Regulatory e-label — protected regression suite

The regulatory e-label is frozen by default. Bootstrap must reproduce live behavior exactly.

Required checks:
1. existing representative QR resolves successfully;
2. route remains regulatory/compliance-only;
3. ingredients/nutrition/compliance data render correctly;
4. language switching preserves regulatory data;
5. no marketing CTA, sales block or Sommelier content is injected;
6. QR/public URL remains stable;
7. unauthorized winery cannot read/write another winery's e-label data.

Any failure in this section is a **release blocker**.

## D. Communication / Marketing — Section 2

Each card must be tested individually from open -> edit/configure -> publish -> public page -> return/navigation.

Minimum card assertions:
- selected card/section is visually obvious;
- only one primary next action is presented;
- no dead buttons or duplicate actions;
- persisted content reappears after reload;
- generated public URL opens successfully;
- invalid/incomplete state produces a clear recoverable message;
- mobile and desktop behavior remain usable.

### Eventi ed enoturismo

Specific regression:
- CTA is named `PUBBLICA PAGINA EVENTO`;
- publishing creates/returns the intended event URL;
- opening the returned URL results in the correct event page, not a blank page/404/unrelated route;
- route parameters winery/marketing/wine/language resolve consistently.

The historical example route shape to verify after live capture is:
`/evento/{cantina}/marketing/{vino}/{lingua}/`

Do not hard-code this shape as authoritative until the current Cloudflare live implementation has been captured and compared.

## E. Sommelier

| Flow | Expected result | Risk |
|---|---|---|
| Text question | Relevant answer grounded in the selected wine/winery context | High |
| Language change | Same wine context retained | Medium |
| Voice path, where enabled | Same permissions/context as text | High |
| Unknown information | Model should not invent winery facts | High |
| Cross-winery context attempt | No leakage | Release blocker |

## F. Analytics

Required checks:
- dashboard values come from persisted production/staging events, not demo constants;
- winery filtering is enforced;
- public-page/QR/marketing/Sommelier events have defined semantics;
- empty state is truthful;
- date/period filters do not silently mix periods;
- analytics route/API failure is visible and diagnosable.

## G. Billing and unlock

Required checks when billing is enabled:
1. Stripe test-mode checkout/payment link starts correctly;
2. cancelled/failed payment leaves account locked;
3. browser return alone does not unlock paid state;
4. verified webhook/server state unlocks exactly once;
5. duplicate webhook is idempotent;
6. paid state survives reload/new session;
7. production and test Stripe configuration are separated.

## H. Destructive actions

For delete/archive actions:
- explicit target and confirmation;
- server-side ownership check;
- predictable result on repeat request;
- no unrelated R2/D1 records are removed;
- rollback/recovery path documented when deletion is not reversible.

## I. Release acceptance

A release is accepted only when:
- automated CI is green;
- staging tests pass with synthetic data;
- protected-area tests pass;
- D1 backup/restore point is recorded for risky changes;
- post-deploy health and representative public URLs pass;
- rollback target is known;
- production acceptance is recorded in the PR/release notes.
