# Roadmap

> La strada dall'idea all'**MVP finale**. Milestone, non date: una data si
> aggiunge solo se esiste una scadenza reale.
>
> - Una sola milestone `active` alla volta.
> - Ogni milestone ha un **criterio di uscita verificabile**. Si chiude quando
>   il criterio è verificato, non quando i task sono spuntati.
> - Le milestone intermedie (M1, M2…) le definisce l'owner; l'agente le propone.
>   Di solito ne bastano 2-4: se sono di più, l'MVP è troppo grande.
> - **MVP è sempre l'ultima.** Ciò che non serve all'MVP va in *Dopo l'MVP*.
> - I task stanno in `TASKS.md` e citano la milestone (`[M1]`, `[MVP]`).

Stati: `planned` | `active` | `done` | `dropped`

---

## M0 — Fondamenta

Status: active
Obiettivo: idea chiara, stack deciso, progetto che si avvia e si testa da zero.

Criterio di uscita:
- [ ] `VISION.md` in stato `confirmed`
- [ ] `PROJECT.yaml` → `stack` compilato e registrato in `DECISIONS.md`
- [ ] repository con remote, primo commit, `.env.example`
- [ ] install, run e test documentati in `STATE.md` e funzionanti su una macchina pulita
- [ ] milestone M1…MVP di questo file approvate dall'owner

---

## M1 — TO VERIFY

Status: planned
Obiettivo: TO VERIFY
<!-- Esempio: il dato principale si crea, si salva e si rilegge (schema + API + UI minima). -->

Criterio di uscita:
- [ ] TO VERIFY

---

## M2 — TO VERIFY

Status: planned
Obiettivo: TO VERIFY
<!-- Esempio: l'esperienza chiave di VISION.md funziona end-to-end in locale. -->

Criterio di uscita:
- [ ] TO VERIFY

---

## MVP — Traguardo

Status: planned
Obiettivo: l'utente principale di `VISION.md` completa l'esperienza chiave
sull'app pubblicata, senza aiuto.

Criterio di uscita:
- [ ] l'esperienza chiave di `VISION.md` funziona end-to-end in produzione
- [ ] deploy riproducibile (comando o CI documentato in `STATE.md`)
- [ ] dati persistenti sul database di produzione, con backup o ripristino documentato
- [ ] secret solo nelle variabili d'ambiente della piattaforma, nessuno nel repo
- [ ] nessun task `[MVP]` aperto in `TASKS.md`, nessun bug bloccante noto
- [ ] TO VERIFY — criteri specifici di questa app

---

## Dopo l'MVP

Direzioni probabili, non ancora milestone. Niente lavoro su queste finché l'MVP
non è `done`.

- TO VERIFY

## Storico

Milestone chiuse o abbandonate, con data e una riga di esito.

- TO VERIFY
