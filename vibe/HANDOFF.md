# Handoff

> Il testimone tra sessioni e tra agenti. Si **riscrive**, non si accoda: lo
> storico è in Git. Scrivilo per chi non ha visto la tua chat e magari usa un
> altro strumento. Regole in `RULES.md` → *Handoff* e *Più agenti*.

Date: TO VERIFY
Mode: sequential                 # sequential | parallel (da PROJECT.yaml)
Last agent: TO VERIFY            # claude | codex, + modello
Next agent: TO VERIFY            # claude | codex | chiunque
Active phase: TO VERIFY
Version: TO VERIFY

## Passaggio corrente

> In modalità `sequential` si compila solo questa sezione.
> In `parallel` qui va il quadro d'insieme, il dettaglio nelle sezioni per agente.

Context:
TO VERIFY

Branch: TO VERIFY
Uncommitted changes: TO VERIFY

Fatto:
- TO VERIFY

A metà:
- TO VERIFY

Prossimo passo:
1. TO VERIFY

Non verificato:
- TO VERIFY

Non toccare senza motivo:
- TO VERIFY

Idee annotate in questa sessione (solo ID):
- TO VERIFY

Da chiedere all'owner:
- Stage e piattaforme
- Stack: campi ancora vuoti in `PROJECT.yaml` → `stack`
- Modalità di lavoro degli agenti (`sequential` / `parallel`)

## Routing modello

> Solo se il tier non era ovvio, o chi entra dovrebbe usare un tier o un agente
> diverso. Vedi `RULES.md` → *Scelta del modello*.

Task complexity: SIMPLE | STANDARD | COMPLEX | CRITICAL
Tier usato: economic | base | premium
Escalation: no | tier superiore | altro agente
Motivo: TO VERIFY

## Interruzione

> Solo se la sessione si è chiusa a metà task. Cancellare quando il task è chiuso.

Agente: TO VERIFY
Motivo: TO VERIFY
Branch WIP: TO VERIFY

| File | Stato | Note |
|---|---|---|
| TO VERIFY | completo / a metà / non iniziato | |

Ultimo comando eseguito: TO VERIFY
Esito: TO VERIFY
Comando successivo previsto: TO VERIFY

Non verificato:
- TO VERIFY

## Revisione richiesta

> Revisione incrociata: l'autore compila la richiesta, l'altro agente l'esito.
> Cancellare dopo il merge.

Autore: TO VERIFY                # claude | codex
Revisore: TO VERIFY              # l'altro
Task / branch: TO VERIFY
Cosa guardare: TO VERIFY

Esito: TO VERIFY                 # ok | da correggere
Problemi trovati:
- TO VERIFY                      # file:riga — scenario in cui si rompe

## Lavoro in parallelo

> Solo in modalità `parallel`. Ogni agente modifica **solo la propria sezione**.

| Agente | Task | Branch / worktree | Stato |
|---|---|---|---|
| claude | TO VERIFY | TO VERIFY | in corso / pronto per merge / bloccato |
| codex | TO VERIFY | TO VERIFY | in corso / pronto per merge / bloccato |

### claude

Fatto:
- TO VERIFY

Prossimo passo:
- TO VERIFY

Non verificato:
- TO VERIFY

### codex

Fatto:
- TO VERIFY

Prossimo passo:
- TO VERIFY

Non verificato:
- TO VERIFY
