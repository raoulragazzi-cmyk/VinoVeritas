# VinoVeritas

Repository operativo per VinoVeritas.

## Stato del repository

**BOOTSTRAP IN CORSO — NON DEPLOYARE IN PRODUZIONE**

Questo repository non contiene ancora il sorgente applicativo verificato della produzione Cloudflare. Fino alla chiusura della Issue #1, qualunque copia storica o file recuperato da backup deve essere trattato esclusivamente come riferimento.

## Source of truth

La fonte autorevole durante il bootstrap è il codice effettivamente distribuito su Cloudflare per:

- Worker API `vinoveritas-api`;
- frontend / Area Cantina;
- configurazione reale dei binding D1 e R2;
- rotte e domini attivi.

Quando una copia locale, un backup o un file della Library differisce dalla produzione, **vince la produzione**. Solo dopo l'acquisizione e verifica della baseline live GitHub diventerà la source of truth.

## Baseline storica nota

È disponibile un backup di produzione datato 18 luglio 2026 con manifest, architettura, Area Cantina, Worker API, schemi SQL e procedure di ripristino. Il Worker storico dichiara la versione `2026-07-16-reset-email`. Questa baseline è utile per confronto forense ma non è automaticamente la versione attuale.

## Regola di sicurezza

Nessun deploy automatico, migrazione D1, modifica R2 o cambio di dominio deve essere abilitato da questo repository finché:

1. il live Cloudflare non è stato acquisito;
2. gli hash e i file non sono stati confrontati;
3. la baseline production non è stata committata senza modifiche funzionali;
4. esiste uno staging separato con dati sintetici;
5. i test critici sono verdi;
6. è documentato il rollback.

Tracciamento principale: Issue #1 — `Bootstrap production source into GitHub before enabling deploys`.
