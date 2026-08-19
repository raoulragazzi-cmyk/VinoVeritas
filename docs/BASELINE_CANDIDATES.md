# VinoVeritas — baseline candidates

## Scopo

Questo documento registra le copie storiche disponibili durante il bootstrap GitHub. Nessuno dei file elencati è autorizzato al deploy finché non viene confrontato con il live Cloudflare corrente.

## Baseline backend storica

| Artefatto | Dimensione | SHA-256 | Stato |
|---|---:|---|---|
| Worker storico candidato (backup luglio 2026) | 365071 B | `fb5d0313b6a18c37e65e22450501b097f40b2555076db7036ea9776fe42f6cbb` | REFERENCE ONLY |

Il Worker storico dichiara `/health` con versione `2026-07-16-reset-email`, coerente con il manifest del backup del 18/07/2026.

## Area Cantina — copie storiche

| File storico | Dimensione | SHA-256 | Nota | Stato |
|---|---:|---|---|---|
| `index(5).html` | 785415 B | `ab1c483602897f1bc9b6c5fbee66f5673f428fbcfd97e68f833827de0e0b2733` | copia grande precedente alle ultime modifiche | REFERENCE ONLY |
| `index(7).html` | 785895 B | `30f78591aa937bac909e8351203d5b75ce1a1202c767311a0d8f2e38c2d66084` | leggermente successiva a index(5), ma ancora obsoleta | REFERENCE ONLY |
| `index-1.html` | 763860 B | `e10920df1cc1e86ade7dd9645c1c07912a5630364be293f0c37faf5cf1afa46b` | contiene ancora elementi UI rimossi successivamente | REFERENCE ONLY |
| `index-2.html` | 460896 B | `d691a4c97d67ef5c3028c5db61a7ec7f1a66931178bd40885a6c7ac254f46edd` | copia più piccola / differente | REFERENCE ONLY |

Le copie principali conservano ancora CTA come `Modifica dati` e `Elimina etichetta`, già rimosse nelle modifiche più recenti. Per questo nessuna è considerata la versione corrente.

## Materiale Worker archiviato

Un'ulteriore copia testuale del Worker ha SHA-256:

`9f852d26625d570a73da22c35aab7c574e56dab7f9660597538da5adcd3ec994`

Dimensione: 365078 B. È quasi coincidente per dimensione con il Worker storico candidato, ma non va considerata equivalente senza confronto byte-per-byte.

## Procedura di promozione a baseline verificata

1. Recuperare da Cloudflare il contenuto effettivamente distribuito di `vinoveritas-api` e del frontend Area Cantina.
2. Calcolare SHA-256 dei file live.
3. Confrontare live vs ogni candidato storico.
4. Documentare differenze funzionali e di configurazione.
5. Committare il live verificato **senza modifiche funzionali** su un branch dedicato.
6. Eseguire smoke test e dry-run.
7. Solo dopo il merge della baseline verificata, GitHub diventa source of truth.

## Regola assoluta

Un nome file più recente, una dimensione maggiore o una data di upload più nuova non bastano per identificare la produzione. La produzione Cloudflare corrente è l'unica autorità durante il bootstrap.
