<!-- vibe-mvp:entrypoint -->
# Agent Entrypoint

Questo repository usa il **Vibe MVP Protocol**. Vale per ogni agente che ci
lavora (Codex legge questo file, Claude Code lo importa da `CLAUDE.md`).

Prima di modificare qualsiasi cosa, leggi in ordine:

1. `vibe/PROJECT.yaml`
2. `vibe/RULES.md`
3. `vibe/STATE.md`
4. `vibe/TASKS.md`
5. `vibe/HANDOFF.md`

Gli altri file del protocollo (visione, roadmap, idee, decisioni, avvio) si
aprono **solo quando servono**: `RULES.md` dice quali e quando.

Poi:

```bash
git status && git branch --show-current && git log --oneline -10
```

Riconosci il tuo nome in `vibe/PROJECT.yaml` → `agents.roster` (`claude` o
`codex`) e la modalità di lavoro (`agents.mode`): da questo dipendono branch,
task che puoi prendere e sezione di `HANDOFF.md` da scrivere.

`vibe/RULES.md` prevale sui default del tuo agente. Le regole di progetto non si
scrivono qui né in `CLAUDE.md`: stanno in `vibe/`.

Se durante il lavoro ti viene un'idea fuori dal task, va in `vibe/IDEAS.md`,
non nel codice.

Prima di chiudere la sessione — o se vieni interrotto — esegui la procedura di
handoff descritta in `vibe/RULES.md`.
