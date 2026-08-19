# Bootstrap status

Stato: **bloccato volontariamente sul deploy production** fino alla cattura del live Cloudflare.

## Completato

- repository inizializzato;
- branch `main` creato;
- governance engineering definita;
- baseline storiche inventariate con SHA-256;
- `.gitignore` per secret, dump e database;
- Pull Request template;
- Bootstrap Safety Guard registrato anche sul branch base `main` per rendere effettivi i controlli PR;
- guard rafforzato: se il repository è pubblico, l'introduzione di sorgenti deployabili (`src/`, frontend, Worker, Wrangler, migrations) viene bloccata;
- Issue #1 per import baseline production;
- Issue #2 per normalizzazione default branch;
- Issue #4 per rendere il repository privato prima dell'import del sorgente production verificato.

## Prossimo gate

1. accesso Cloudflare disponibile;
2. verifica dell'integrazione Cloudflare/GitHub con repository privati;
3. repository VinoVeritas reso privato;
4. export live Worker + frontend;
5. hash e confronto con candidati;
6. import baseline production senza modifica funzionale;
7. staging isolato;
8. test critici;
9. solo dopo: deploy automation.
