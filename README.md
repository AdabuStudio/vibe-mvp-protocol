# Vibe MVP Protocol

Un metodo semplice per sviluppare un'app con più AI coding agent — pensato per
**Claude Code** e **Codex** — **dall'idea a un MVP finito**.

Il principio: la memoria del progetto vive nel repository, non nella chat.
Un agente può continuare il lavoro lasciato da un altro leggendo pochi file, non
ricostruendo una conversazione. E un metodo fisso — visione, roadmap, task,
idee — tiene lo scope sotto controllo fino al traguardo.

## Come funziona

```
VISION  →  ROADMAP (M0 … MVP)  →  TASKS  →  codice
   ↑            ↑
   └── IDEAS ───┘   (solo se l'owner le promuove)
```

| File | Ruolo |
|---|---|
| `vibe/PROJECT.yaml` | identità dell'app, stack scelto, agenti (roster, modalità, modelli per tier) |
| `vibe/RULES.md` | le regole del metodo — uguali per ogni progetto |
| `vibe/VISION.md` | perché esiste l'app, per chi, cosa non fa |
| `vibe/ROADMAP.md` | milestone con criterio di uscita, fino all'MVP |
| `vibe/TASKS.md` | NOW / NEXT / BLOCKED / BACKLOG, con ID e milestone |
| `vibe/IDEAS.md` | parcheggio delle idee: raw → evaluated → promoted / parked / rejected |
| `vibe/DECISIONS.md` | decisioni tecniche e di prodotto |
| `vibe/STATE.md` | fotografia dello stato attuale |
| `vibe/HANDOFF.md` | passaggio di consegne tra sessioni e agenti, revisioni incrociate |
| `vibe/START.md` | istruzioni per il primo ingresso |
| `AGENTS.md` | entrypoint unico (Codex lo legge direttamente) |
| `CLAUDE.md` | importa `AGENTS.md` per Claude Code |

Ad ogni sessione l'agente legge solo `PROJECT.yaml`, `RULES.md`, `STATE.md`,
`TASKS.md`, `HANDOFF.md`. Gli altri file li apre quando servono.

## Più agenti: Claude Code e Codex

Il protocollo è pensato per far lavorare sullo stesso repo **Claude Code** e
**Codex**, a turno o insieme. Si configura in `vibe/PROJECT.yaml` → `agents`.

- **Ingresso unico.** Codex legge `AGENTS.md`, Claude Code `CLAUDE.md`, che
  importa `AGENTS.md`: un solo entrypoint, nessuna regola duplicata.
- **Identità.** Ogni agente ha un nome (`claude`, `codex`) che usa nei task
  presi (`@codex`), nei branch (`codex/T-014-login`) e nei commit (trailer
  `Agent: codex`). `git log` dice chi ha fatto cosa.
- **Sequenziale.** Un agente alla volta; il testimone passa con
  `vibe/HANDOFF.md`, scritto per chi non ha visto la chat.
- **Parallelo.** Un task per agente, preso con un commit su `main`; un branch
  (meglio un worktree) per agente; ognuno scrive solo la sua sezione di
  `HANDOFF.md`; i merge su `main` li fa l'integratore (di default l'owner).
- **Revisione incrociata.** Sui task critici e alla chiusura di una milestone il
  lavoro di un agente lo rivede l'altro: due fornitori diversi vedono errori
  diversi.
- **Modelli per tier.** Le regole parlano di `economic` / `base` / `premium`; i
  nomi dei modelli di ciascun agente stanno solo in `PROJECT.yaml`.

## Stack

Il protocollo non impone infrastruttura: lo stack lo decide l'owner in
`vibe/PROJECT.yaml` → `stack`. Come punto di partenza suggerisce **GitHub**
(repo e CI), **Cloudflare** (hosting, Workers/Pages) e **Neon** (Postgres
serverless). L'agente li propone, ma chiede prima di usarli e non aggiunge
servizi non dichiarati.

## Uso

**Nuova app** — parti da una copia di questo repo:

```bash
git clone <url-di-questo-repo> mia-app
```

```bash
cd mia-app && rm -rf .git && git init
```

**Progetto esistente** — copia dentro il protocollo:

```bash
cp -R /percorso/vibe-mvp-protocol/vibe /percorso/vibe-mvp-protocol/AGENTS.md /percorso/vibe-mvp-protocol/CLAUDE.md .
```

Se il progetto ha già un `AGENTS.md` o `CLAUDE.md`, non sovrascriverlo: anteponi
il blocco di puntamento e lascia che il primo avvio smisti il resto.

Poi, in entrambi i casi, apri l'agente nel repo e scrivi:

> Leggi `vibe/START.md` ed eseguilo.

L'agente fa le domande sull'idea (o ricostruisce lo stato del codice), compila
visione, stack e roadmap, e si ferma per la tua conferma.

Ricordati di ignorare i secret nel `.gitignore` dell'app (`.env`, `.env.local`,
`.dev.vars` per Cloudflare).

## Aggiornare il protocollo in un progetto

Si sovrascrivono solo i file del metodo: `vibe/RULES.md`, `vibe/START.md`,
`AGENTS.md`, `CLAUDE.md` (se contengono solo l'entrypoint). Tutti gli altri file
di `vibe/` sono contenuto del progetto e non si toccano.

## Versione

v1
