# Start — primo ingresso nel progetto

Questo file si usa **una volta sola**, quando il protocollo entra in un progetto.
Dai all'agente questo messaggio:

> Leggi `vibe/START.md` ed eseguilo.

Il primo ingresso è l'unica sessione in cui si legge tutto `vibe/`. Dopo vale la
lettura a due livelli di `RULES.md`.

## Regola

In questa sessione **non si scrive codice applicativo**. Si prepara la memoria
del progetto e ci si ferma.

Non fare reset Git, force checkout o pulizie: non scartare niente.

## 1. Leggi

Tutti i file di `vibe/`, in quest'ordine: `PROJECT.yaml`, `RULES.md`,
`VISION.md`, `ROADMAP.md`, `TASKS.md`, `IDEAS.md`, `DECISIONS.md`, `STATE.md`,
`HANDOFF.md`. Poi:

```bash
git status && git branch --show-current && git log --oneline -20
```

## 2. Capisci da dove parti

**Caso A — idea nuova** (repo vuoto o quasi): vai al punto 3A.

**Caso B — progetto esistente** (c'è già codice): vai al punto 3B.

## 3A. Idea nuova

Fai all'owner **un solo giro di domande**, tutte insieme:

1. L'app in una frase: chi la usa e per fare cosa?
2. Che problema risolve, e come lo risolvono oggi?
3. Qual è il percorso minimo che, se funziona, rende l'app utile?
4. Cosa **non** deve fare, almeno nell'MVP?
5. Piattaforme: web, mobile, API…?
6. Stack: confermi le preferenze di `PROJECT.yaml` → `stack.preferred`
   (GitHub, Cloudflare, Neon) o scegli altro? Linguaggio e framework?
7. Vincoli: tempi, budget, dati sensibili.
8. Agenti: lavoreranno Claude Code e Codex? Uno alla volta (`sequential`) o
   insieme su task diversi (`parallel`)? Chi integra i branch su `main`? Quali
   modelli ha davvero l'account Codex per ogni tier?

Con le risposte compila `VISION.md`, `PROJECT.yaml` (`project`, `stack`, `agents`) e
proponi in `ROADMAP.md` 2-4 milestone intermedie fino all'MVP, ciascuna con un
criterio di uscita verificabile. Ciò che è emerso ma non serve all'MVP va in
`IDEAS.md`. Le risposte mancanti restano `TO VERIFY`.

## 3B. Progetto esistente

Guarda anche i branch esistenti (`git branch -a`) e i worktree
(`git worktree list`): potrebbero esserci lavori di altri agenti in corso.

Analizza README, struttura, dipendenze, configurazioni, schema/migrazioni, test,
script, CI, `.env.example`, deploy, TODO e FIXME, cronologia Git recente.

Poi:

- `STATE.md` → fotografia concisa: stack, architettura, cosa funziona, cosa è a
  metà, problemi noti, come si installa/avvia/testa/builda;
- `PROJECT.yaml` → `project` e `stack` per ciò che si deduce con certezza;
  `agents` (roster, modalità, integratore) chiedendolo all'owner;
- `DECISIONS.md` → solo decisioni deducibili, con `Status: inferred`;
- `TASKS.md` → lavoro in corso e TODO reali, con ID e milestone;
- `VISION.md` e `ROADMAP.md` → una **bozza** dedotta dal codice, da far
  confermare all'owner;
- `IDEAS.md` → spunti trovati che non sono lavoro deciso.

Se trovi memoria sparsa (`TODO.md`, `NOTES.md`, regole proprie in `CLAUDE.md` o
`AGENTS.md`, `.cursorrules`…) smistala nei file giusti invece di duplicarla, e
riduci `CLAUDE.md` / `AGENTS.md` al solo blocco di puntamento.

Non inventare: quello che non sai resta `UNKNOWN` o `TO VERIFY`.

## 4. Chiudi

Riscrivi `HANDOFF.md` e mostra all'owner:

1. cosa hai capito del progetto;
2. cosa hai scritto in `vibe/` (e cosa hai migrato, da dove);
3. le milestone proposte fino all'MVP;
4. le domande ancora aperte;
5. il primo task che proponi.

Poi **fermati**. Non iniziare l'implementazione finché l'owner non conferma
visione, stack e roadmap.
