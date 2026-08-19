# Engineering governance — VinoVeritas

## 1. Obiettivo

Trasformare VinoVeritas da progetto gestito tramite copie locali / deploy manuali a prodotto con source-of-truth GitHub, staging isolato, test automatici, backup e promozione controllata verso Cloudflare production.

## 2. Ambienti

### Production

- Worker API: `vinoveritas-api`
- Area Cantina / frontend: da verificare sul live Cloudflare
- D1 production: `vinoveritas-db`
- R2 production: `vinoveritas-media`
- domini e route: devono essere catturati dal live prima di essere codificati nel repository

### Staging

Da creare solo dopo la cattura della baseline production:

- Worker API staging separato;
- frontend staging separato;
- D1 staging dedicato;
- R2 staging o namespace media isolato se necessario;
- segreti separati;
- dati sintetici, non clienti reali per default.

## 3. Source of truth

Durante il bootstrap la produzione Cloudflare è autorevole.

Dopo il bootstrap:

1. `main` contiene l'ultima baseline approvata;
2. ogni modifica nasce da un branch;
3. ogni modifica passa da Pull Request;
4. CI e staging devono essere verdi;
5. solo una release approvata può arrivare a production.

Sono vietati deploy manuali di file non presenti in GitHub, salvo emergenza documentata e immediatamente riconciliata nel repository.

## 4. Classi di rischio

### Basso
Copy, microcopy, spaziature, CSS locale, correzioni visive senza modifica di flussi o dati.

### Medio
Nuove card, CTA, route, analytics, logica marketing, Sommelier, integrazioni non distruttive.

### Alto
Auth, sessioni, Stripe, webhook, D1 schema, cancellazioni, pubblicazione e-label, ownership cantina/referenza, QR, domini, R2, compliance.

Le modifiche ad alto rischio richiedono sempre backup pre-change, staging e rollback documentato.

## 5. Flussi invarianti da proteggere

### Core vino
`login -> sessione -> cantina -> referenza -> pubblicazione -> URL pubblico -> QR -> analytics`

### Percorso prodotto
`creazione cantina -> creazione e-label -> Marketing/Communication -> Sommelier -> Analytics`

### Compliance
I dati regolamentati non devono essere inventati dall'AI. La cantina resta responsabile dei dati dichiarati e della loro approvazione. La componente commerciale/narrativa deve restare separata dalla e-label normativa quando richiesto dalla normativa e dal disegno di prodotto.

## 6. Release gate

Prima della production:

- PR completa;
- test automatici verdi;
- staging acceptance verde;
- nessun segreto nel diff;
- eventuale migrazione D1 verificata su staging;
- backup production recente per modifiche ad alto rischio;
- rollback definito;
- health check noto;
- verifica dei flussi critici interessati.

## 7. Database

- nessuna modifica manuale allo schema production senza migration tracciata;
- migration additive quando possibile;
- evitare DROP/rename distruttivi senza piano a fasi;
- backup prima di migration ad alto rischio;
- staging deve usare D1 separato;
- i test PR non devono mai usare il D1 production.

## 8. Segreti

Nel repository possono essere documentati esclusivamente i **nomi** dei secret / environment variables. I valori non devono essere committati.

## 9. Rollback

Il rollback applicativo e il rollback dati sono due operazioni diverse.

- codice: ripristino della last-known-good release;
- D1: Time Travel / restore o procedura equivalente, solo se realmente necessario;
- R2: non sovrascrivere o cancellare media production senza una strategia di recupero.

Il restore D1 non viene automatizzato come effetto collaterale del deploy.

## 10. Definizione di Done

Una modifica è Done solo quando:

1. è versionata;
2. ha test proporzionati al rischio;
3. è stata verificata in staging quando necessario;
4. è stata promossa con rollback disponibile;
5. il live è stato verificato dopo il deploy;
6. Issue/PR descrivono cosa è cambiato.
