# VinoVeritas — Protected Areas

This file defines production areas that require elevated review and explicit release gates.

## 1. Regulatory e-label — FROZEN BY DEFAULT

The regulatory e-label is a compliance surface, not a marketing surface.

Rules:
- do not change its functional behavior, data model, public route, QR resolution or regulatory content unless the product owner explicitly authorizes that change;
- do not add marketing, sales, tracking, promotional CTA or Sommelier content inside the regulatory e-label;
- marketing/Communication experiences must remain logically and visibly separate;
- any authorized e-label change requires before/after regression evidence on existing public routes and representative wines/languages;
- a bootstrap/import operation must preserve the exact live behavior. Bootstrap is not permission to refactor the e-label.

Release blocker examples:
- an existing regulatory QR resolves to a different page or error;
- ingredients/nutrition/compliance content disappears or changes unexpectedly;
- a marketing CTA is introduced into the regulatory layer;
- a wine from winery A can expose or mutate winery B data.

## 2. Authentication, sessions and winery isolation

Protected because a failure can expose customer data.

Required invariants:
- authenticated user resolves to the intended winery/account;
- wine/reference mutations are authorized against winery ownership server-side;
- session expiration/logout works consistently;
- no client-side identifier alone is trusted for authorization;
- staging never uses production customer sessions or production data by default.

## 3. Publish and public URL generation

Protected because QR codes and external links can live for years.

Required invariants:
- publishing is idempotent where applicable;
- generated slugs/routes remain stable unless a migration is explicitly planned;
- public page, marketing page and regulatory e-label routes remain distinct;
- 404/authorization failures are explicit, never silent redirects to unrelated content.

## 4. Payments and account unlock

Protected because payment state controls paid capabilities.

Required invariants:
- browser return URLs are never the sole source of truth for payment success;
- webhook/server verification controls durable unlock state;
- test and production Stripe credentials/resources remain separated;
- a failed/abandoned payment cannot unlock paid features;
- retries/webhook duplication are safe.

## 5. Analytics

Protected where analytics drive commercial decisions.

Required invariants:
- production dashboards use real persisted events/aggregates, not demo values;
- tenant/winery filtering is enforced server-side;
- event definitions are versioned when meaning changes;
- regulatory e-label analytics must respect the compliance/privacy design.

## 6. R2/media and destructive actions

Protected because deletion can be irreversible.

Rules:
- delete actions require authorization and explicit target ownership;
- destructive operations should be idempotent and auditable where practical;
- staging uses isolated/synthetic media storage when write tests are needed;
- no bootstrap task deletes or rewrites production media.

## Review principle

A UI-only change may use a lighter path. Any change touching a protected area must include risk, test evidence, rollback instructions and explicit confirmation that the protected invariants still hold.
