# Tasks

> Lavoro interno concreto. Ogni task ha:
> - un ID stabile `T-NNN`, progressivo e mai riusato;
> - la milestone che serve, tra parentesi quadre (`[M1]`);
> - in `NOW`, un criterio di completamento verificabile (`Done when:`);
> - quando un agente lo prende: `@claude` o `@codex` e il branch.
>
> Un task già preso da un altro agente non si tocca.
> Un task significativo può portare anche `Complexity:` e `Tier:`
> (vedi `RULES.md` → *Scelta del modello*). Non serve sui micro-task.
>
> Un task che non serve la milestone attiva non va in `NOW`.
> Un'idea non ancora decisa non è un task: va in `IDEAS.md`.

Formato:

```
- [ ] T-012 [M1] Titolo breve — Done when: <criterio verificabile>
- [ ] T-013 [M1] Titolo breve — Done when: <criterio> — @codex codex/T-013-slug
- [x] T-009 [M1] Titolo breve — @claude, merged
```

In `parallel` si prende un task con un commit **su `main`** che cambia solo quella riga, così
l'altro agente lo vede subito:

```bash
git commit -am "chore(T-013): preso da codex"
```

Prossimo ID libero: T-004

## NOW

- [ ] T-001 [M0] Definire l'idea con l'owner — Done when: `VISION.md` ha `Status: confirmed`.
- [ ] T-002 [M0] Far decidere lo stack all'owner — Done when: `PROJECT.yaml` → `stack` compilato e voce in `DECISIONS.md`.
- [ ] T-003 [M0] Proporre milestone M1…MVP — Done when: l'owner ha approvato `ROADMAP.md`.

## NEXT

- [ ] TO VERIFY

## BLOCKED

> Per ogni task: cosa lo blocca e chi può sbloccarlo.

- [ ] TO VERIFY

## BACKLOG

- [ ] TO VERIFY

## RECENTLY DONE

> Ultimi 10 circa. Quelli più vecchi si tolgono: lo storico è in Git.

- [x] Installazione Vibe MVP Protocol.
