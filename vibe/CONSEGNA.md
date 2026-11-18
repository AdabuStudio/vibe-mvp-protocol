# Consegna allo sviluppatore

> Il documento per lo sviluppatore che prenderà in mano l'app dopo l'MVP. Deve
> poter capire, avviare e modificare il progetto leggendo **solo** questo file e
> i link che contiene.
>
> Si compila **durante** lo sviluppo, non alla fine: ogni fase aggiorna le sue
> sezioni (vedi `ROADMAP.md`). Il *Debito tecnico* si aggiorna ogni volta che si
> prende una scorciatoia.
>
> **Nessun secret qui**: solo nomi delle variabili e dove si trovano i valori.

Versione: TO VERIFY
Ultimo aggiornamento: TO VERIFY

## In breve

Cosa fa l'app, per chi, in 5 righe. Rimando a `VISION.md`.

TO VERIFY

## Avviare il progetto

Prerequisiti, installazione, avvio, test, pubblicazione: rimando a `STATE.md` →
*Development*, che deve essere sufficiente da solo.

## Architettura

Componenti principali e come si parlano, a parole o con uno schema testuale.

```
TO VERIFY
```

## Ambienti

| Ambiente | Indirizzo | Database | Come si pubblica |
|---|---|---|---|
| locale | TO VERIFY | TO VERIFY | — |
| prova | TO VERIFY | TO VERIFY | TO VERIFY |
| produzione | TO VERIFY | TO VERIFY | TO VERIFY |

## Servizi e account

| Servizio | A cosa serve | Proprietario dell'account | Piano / costo | 2FA |
|---|---|---|---|---|
| GitHub | codice, CI | TO VERIFY | TO VERIFY | TO VERIFY |
| TO VERIFY | | | | |

## Variabili d'ambiente

| Nome | A cosa serve | Dove sta il valore |
|---|---|---|
| TO VERIFY | | `.env` locale / pannello di <servizio> |

## Modello dati

A parole: le "cose" dell'app, le loro informazioni principali e i collegamenti.
Dove stanno lo schema e le migrazioni.

TO VERIFY

## Utenti e permessi

Ruoli, metodo di accesso e tabella dei permessi.

| Azione | TO VERIFY ruolo | TO VERIFY ruolo |
|---|---|---|
| TO VERIFY | sì / no / solo i propri | |

## Test

- Automatici: comando, cosa coprono, dove si vedono → `TESTS.md`
- Collaudi manuali e loro esiti → `TESTS.md`

## Versioni e rilascio

Come si pubblica una nuova versione e come si torna alla precedente.
Storico delle versioni → `CHANGELOG.md`.

TO VERIFY

## Backup e ripristino

Cosa viene salvato, con che frequenza, e i passi per ripristinare.
Ultimo ripristino provato: TO VERIFY

## Sicurezza

Cosa è stato verificato e cosa no. Lo sviluppatore deve sapere dove guardare per primo.

- Verificato: TO VERIFY
- Non verificato: TO VERIFY

## Debito tecnico

Scorciatoie prese per arrivare all'MVP. Sono lecite: l'importante è che siano
scritte qui.

| Scorciatoia | Dove (file / area) | Rischio | Come si sistema | Priorità |
|---|---|---|---|---|
| TO VERIFY | | | | alta / media / bassa |

## Problemi noti

- TO VERIFY

## Per il resto

- Decisioni prese e perché → `DECISIONS.md`
- Idee aperte, cose chieste e non fatte → `IDEAS.md`
- Direzioni dopo l'MVP → `ROADMAP.md` → *Dopo l'MVP*
