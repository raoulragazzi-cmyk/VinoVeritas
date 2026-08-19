## Cosa cambia

Descrivere la modifica in termini funzionali e tecnici.

## Perché

Issue / obiettivo collegato:

## Rischio

- [ ] Basso — copy / UI locale
- [ ] Medio — flussi / route / analytics / integrazioni
- [ ] Alto — auth / sessioni / Stripe / D1 / R2 / QR / e-label / domini / cancellazioni

## Dati e migrazioni

- [ ] Nessuna modifica dati/schema
- [ ] Migration D1 inclusa e testata su staging
- [ ] Modifica R2 / media
- [ ] Backup production richiesto prima del deploy

Dettagli:

## Test eseguiti

- [ ] CI automatica verde
- [ ] Smoke test interessati
- [ ] Staging acceptance
- [ ] Test manuale del percorso cliente

## Percorsi critici verificati

- [ ] login / sessione
- [ ] cantina / referenze
- [ ] e-label / pubblicazione
- [ ] URL pubblico / QR
- [ ] Marketing / Communication
- [ ] Sommelier
- [ ] Analytics
- [ ] Stripe / billing

## Rollback

Descrivere come tornare alla last-known-good release e, se necessario, come gestire dati/migrazioni.

## Impatto cliente

Descrivere cosa noterà una cantina o un utente finale dopo il deploy.

## Checklist sicurezza

- [ ] Nessun secret o dato cliente nel diff
- [ ] Nessun PR/test usa D1 production
- [ ] Nessun deploy automatico non intenzionale
- [ ] Compliance e-label preservata
