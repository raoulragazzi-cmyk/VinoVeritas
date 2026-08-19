# Security policy — VinoVeritas

## Compliance data

Ingredienti, allergeni, valori nutrizionali, annata, denominazione, lotto e altri dati regolamentati devono provenire dalla cantina o da fonti approvate. L'AI non deve inventare o sostituire dati obbligatori.

## Winery isolation

Auth, sessioni, ownership cantina/referenza e autorizzazioni di pubblicazione sono aree ad alto rischio. Una cantina non deve poter leggere, modificare, pubblicare o cancellare referenze appartenenti a un'altra cantina.

## Production data

Non copiare dati reali di cantine, utenti, vini, scansioni, ordini, media o payload production in issue, PR, fixture o staging per default. Utilizzare dati sintetici.

## Secrets

Non committare API key, Stripe secrets, webhook secrets, OpenAI keys, Resend keys, session secrets, Cloudflare credentials, `.dev.vars` o `.env`. Nel repository si documentano solo i nomi delle variabili.

## D1 / R2

Le modifiche D1 devono essere versionate e provate su staging separato. Le modifiche R2 o alle pipeline media devono evitare cancellazioni/sovrascritture irreversibili. Le modifiche ad alto rischio richiedono backup e rollback.

## E-label / QR

Qualunque cambiamento a pubblicazione, slug, URL pubblici, QR, route e-label o separazione tra contenuto normativo e marketing richiede test mirati e verifica post-deploy. Gli URL stampati su etichetta sono asset persistenti e non vanno cambiati accidentalmente.

## Pagamenti e integrazioni

Stripe, webhook, email, Sommelier AI e servizi esterni richiedono staging, gestione degli errori, idempotenza quando applicabile e osservabilità.

## Reporting

Segnalare vulnerabilità e incidenti al repository owner in privato. Non pubblicare segreti, dati personali o dettagli sfruttabili in issue pubbliche.
