# Start — onboarding veloce

Si usa **una volta sola**, al primo ingresso nel progetto. L'owner scrive
all'agente:

> Leggi `vibe/START.md` ed eseguilo.

Obiettivo: in **10-15 minuti** l'owner sa come funziona il percorso, ha
risposto a poche domande semplici, e il progetto è pronto per la fase M0.

## Regole dell'onboarding

- Niente codice applicativo in questa sessione.
- Niente reset Git, force checkout o pulizie: non si scarta niente.
- Linguaggio semplice, come da `RULES.md` → *Lavorare con un owner che non è
  sviluppatore*.
- Le domande sono **poche e tutte insieme**, ognuna con una risposta consigliata
  già pronta: l'owner può rispondere anche solo "ok".

## 1. Leggi (in silenzio)

Tutti i file di `vibe/`. È l'unica sessione in cui si legge tutto: dopo vale la
lettura a due livelli di `RULES.md`. Poi:

```bash
git status && git branch -a && git worktree list && git log --oneline -20
```

Se c'è già codice, analizzalo prima delle domande (punto 4B): così chiedi solo
quello che non puoi dedurre.

## 2. Benvenuto (un messaggio, breve)

Presenta all'owner il percorso in poche righe, con parole tue, più o meno così:

> Costruiamo la tua app in 7 tappe: idea e cantiere → infrastruttura → dati →
> utenti e permessi → funzione principale → qualità e sicurezza → pubblicazione.
> Per ogni tappa ti dico cosa devi decidere, cosa faccio io e cosa controlli tu
> con dei piccoli test a mano. Ogni tappa chiusa è una versione dell'app, a cui
> si può sempre tornare. Alla fine avrai un'app online e un documento per
> passarla a uno sviluppatore. Tutto resta scritto nella cartella `vibe/`.

## 3. Le domande (un solo messaggio)

Adatta le domande a quello che già sai. Per ognuna proponi una risposta.

1. **L'idea in una frase**: chi la userà e per fare cosa?
2. **Il problema**: come lo risolvono oggi, senza la tua app?
3. **Il percorso principale**: quali sono i 3-5 passi che, se funzionano,
   rendono l'app utile?
4. **Cosa non deve fare**, almeno per ora?
5. **Dove si usa**: dal browser, da telefono, entrambi? *(consigliato: web
   adatto anche al telefono)*
6. **Utenti**: serve un accesso con account? Ci sono tipi diversi di utenti?
7. **Strumenti**: va bene GitHub per il codice, Cloudflare per far girare
   l'app e Neon per i dati? *(consigliato: sì — costo iniziale zero o quasi;
   le scelte tecniche di dettaglio le propongo io e te le spiego)*
8. **Vincoli**: tempi, budget mensile, dati sensibili (salute, minori,
   pagamenti)?
9. **Esperienza**: hai mai programmato? *(serve a capire quanto spiegare)*
10. **Agenti**: userai Claude, Codex o entrambi? *(consigliato: uno alla volta,
    con l'altro come revisore sulle parti critiche)*

## 4A. Idea nuova — con le risposte

- `VISION.md` compilato, in stato `draft`;
- `PROJECT.yaml`: `project` (nome, owner, `owner_experience`, piattaforme),
  `stack` (le scelte confermate e le proposte ancora da confermare),
  `agents` (roster, modalità);
- `ROADMAP.md`: il percorso è già scritto. Proponi solo gli adattamenti: fasi
  da saltare (es. M3 se non ci sono account), M4 da dividere se il percorso
  principale è lungo;
- `IDEAS.md`: tutto ciò che è emerso ma non serve all'MVP;
- `TESTS.md` e `CONSEGNA.md` restano modelli: si riempiono fase per fase.

Le risposte mancanti restano `TO VERIFY`.

## 4B. Progetto esistente

Analizza README, struttura, dipendenze, configurazioni, schema e migrazioni,
test, CI, `.env.example`, deploy, TODO e FIXME, cronologia Git, branch e
worktree.

- `STATE.md` → fotografia concisa: stack, cosa funziona, cosa è a metà,
  problemi noti, come si installa, avvia, testa, pubblica;
- `PROJECT.yaml` → ciò che si deduce con certezza;
- `ROADMAP.md` → segna le fasi già coperte dal codice esistente (con le caselle
  verificate davvero) e indica da quale fase si riparte;
- `DECISIONS.md` → solo decisioni deducibili, `Status: inferred`;
- `TASKS.md` → lavoro in corso e TODO reali, con ID e fase;
- `CONSEGNA.md` → *Debito tecnico* con i problemi già visibili;
- `VISION.md` → bozza dedotta, da far confermare all'owner;
- memoria sparsa (`TODO.md`, `NOTES.md`, regole proprie in `CLAUDE.md` o
  `AGENTS.md`, `.cursorrules`…) → smistata nei file giusti, e `CLAUDE.md` /
  `AGENTS.md` ridotti all'entrypoint.

Non inventare: quello che non sai resta `UNKNOWN` o `TO VERIFY`.

## 5. Chiudi (un messaggio, breve)

Riscrivi `HANDOFF.md` e di' all'owner, in parole semplici:

1. cosa hai capito dell'app (3 righe);
2. le scelte fatte e quelle ancora da confermare;
3. eventuali adattamenti proposti al percorso;
4. **la prima cosa che farete insieme** in M0, e cosa dovrà fare lui
   (es. creare l'account GitHub — con i passi).

Poi **fermati**. Si comincia M0 solo dopo il suo ok su visione e strumenti.
