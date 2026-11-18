# Roadmap — il percorso fino all'MVP

> Il percorso che porta un'idea a un **MVP pubblicato e consegnabile a uno
> sviluppatore**. Le fasi sono quelle che ogni app attraversa: qui sono già
> scritte, con cosa decidi tu, cosa fa l'agente e cosa verifichi tu.
>
> - Una sola fase `active` alla volta, nell'ordine.
> - Una fase si chiude quando **tutte le caselle sono spuntate e verificate**.
>   Alla chiusura l'app prende la versione indicata (vedi `RULES.md` → *Versioni*).
> - L'owner può adattare il percorso: dividere una fase in più fasi (tipico per
>   M4), o chiudere come `dropped`, con il motivo, una fase che non serve (es. M3
>   per un'app senza utenti). L'agente propone, l'owner approva.
> - I task in `TASKS.md` citano la fase (`[M3]`). I collaudi in `TESTS.md` anche.
> - Ciò che non serve all'MVP va in *Dopo l'MVP* o in `IDEAS.md`.

Stati: `planned` | `active` | `done` | `dropped`

---

## M0 — Idea e cantiere

Status: active · Versione alla chiusura: 0.1.0

> Si chiarisce cosa costruiamo e si prepara il "cantiere": dove sta il codice,
> con quali strumenti si costruisce, come si avvia sul tuo computer.

**Decidi tu**
- [ ] la visione: `VISION.md` in stato `confirmed`
- [ ] lo stack, su proposta dell'agente (consigliato: GitHub + Cloudflare + Neon), registrato in `DECISIONS.md`
- [ ] chi lavora: solo Claude, solo Codex o entrambi, e in che modalità

**Fai tu** (l'agente ti dà le istruzioni passo-passo)
- [ ] account GitHub, con verifica in due passaggi (2FA) attiva
- [ ] un password manager dove tenere accessi e chiavi del progetto

**Fa l'agente**
- [ ] struttura del progetto e repository su GitHub
- [ ] un solo comando per avviare l'app in locale, scritto in `STATE.md`
- [ ] `.env.example` e `.gitignore` che esclude i secret
- [ ] primo test automatico e CI: i test girano da soli su GitHub a ogni modifica
- [ ] `CHANGELOG.md` e versione `0.1.0`

**Verifichi tu** (collaudi `[M0]` in `TESTS.md`)
- [ ] l'app vuota si apre sul tuo computer seguendo solo le istruzioni di `STATE.md`
- [ ] su GitHub vedi il codice e il segno verde dei test

---

## M1 — Infrastruttura e ambienti

Status: planned · Versione alla chiusura: 0.2.0

> L'app vive in tre posti separati: **locale** (il tuo computer), **prova**
> (un indirizzo online per testare) e **produzione** (quella vera, per gli
> utenti). I dati di prova non si mescolano mai con quelli veri.

**Decidi tu**
- [ ] quanto sei disposto a spendere al mese per i servizi (spesso zero all'inizio)
- [ ] dove stanno i dati (consigliato: Unione Europea, per il GDPR)
- [ ] dominio: subito, dopo, o solo l'indirizzo gratuito del servizio

**Fai tu** (con istruzioni passo-passo)
- [ ] account Cloudflare e Neon (o quelli scelti), con 2FA
- [ ] inserire le chiavi dove l'agente indica (pannello del servizio o `.env` locale), **mai in chat**

**Fa l'agente**
- [ ] pubblicazione automatica sull'ambiente di prova a ogni modifica su `main`
- [ ] database separati per sviluppo, prova e produzione
- [ ] variabili d'ambiente configurate, elencate per nome in `CONSEGNA.md`
- [ ] backup del database attivo e procedura di ripristino scritta in `CONSEGNA.md`
- [ ] servizi, costi e proprietario di ogni account in `CONSEGNA.md`

**Verifichi tu**
- [ ] apri l'indirizzo di prova anche dal telefono
- [ ] una modifica pubblicata compare sull'ambiente di prova
- [ ] un dato creato in prova non compare in produzione

---

## M2 — Dati

Status: planned · Versione alla chiusura: 0.3.0

> Quali informazioni conserva l'app e come sono collegate tra loro (es. un
> cliente ha molte prenotazioni). È la parte più difficile da cambiare dopo:
> vale la pena pensarci bene.

**Decidi tu**
- [ ] le "cose" dell'app e le loro informazioni (l'agente propone, tu correggi)
- [ ] cosa è obbligatorio e cosa facoltativo
- [ ] quali sono **dati personali** e per quanto tempo si conservano

**Fa l'agente**
- [ ] modello dati e migrazioni versionate (ogni cambio di struttura è tracciato)
- [ ] dati di esempio per sviluppo e prova
- [ ] descrizione **a parole** del modello dati in `CONSEGNA.md`
- [ ] decisioni sul modello dati in `DECISIONS.md`

**Verifichi tu**
- [ ] la descrizione a parole rispecchia la realtà del tuo lavoro
- [ ] in prova crei, modifichi e cancelli un elemento, e ritrovi quello che ti aspetti

---

## M3 — Utenti, accesso e permessi

Status: planned · Versione alla chiusura: 0.4.0

> Chi può entrare, come, e cosa può vedere o fare ciascuno. È una parte
> **critica**: un errore qui espone dati di altri. Si usa sempre un sistema di
> accesso già collaudato, mai uno scritto da zero.

**Decidi tu**
- [ ] i tipi di utente (ruoli), es. amministratore, cliente, ospite
- [ ] la **tabella dei permessi**: per ogni ruolo, cosa può vedere, creare, modificare, cancellare
- [ ] come si entra: email e password, link via email, Google…
- [ ] registrazione libera, su invito o solo creata da un amministratore
- [ ] cosa succede se un utente dimentica la password o vuole cancellarsi

**Fa l'agente**
- [ ] accesso con un servizio o una libreria consolidata
- [ ] permessi controllati sul server, non solo nascosti nell'interfaccia
- [ ] un test automatico per ogni riga della tabella dei permessi
- [ ] tabella dei permessi in `CONSEGNA.md` e in `DECISIONS.md`
- [ ] revisione incrociata dell'altro agente (se ne usi due), o revisione su tier premium

**Verifichi tu** (l'agente prepara gli scenari in `TESTS.md`)
- [ ] con un utente di prova per ogni ruolo: fai ciò che è permesso → funziona
- [ ] con lo stesso utente: provi ciò che **non** è permesso → viene bloccato
- [ ] recupero password, uscita, accesso da un secondo dispositivo

---

## M4 — Funzione chiave

Status: planned · Versione alla chiusura: 0.5.0

> Il percorso principale di `VISION.md` funziona dall'inizio alla fine. Se è
> grande, si divide in più fasi (M4a, M4b…): ognuna aggiunge un pezzo usabile.

**Decidi tu**
- [ ] schermate, testi e ordine dei passaggi (l'agente propone bozze)
- [ ] cosa succede quando qualcosa va storto (dato mancante, errore di rete…)

**Fa l'agente**
- [ ] implementazione a piccoli passi, ognuno pubblicato in prova
- [ ] test automatici per ogni passaggio del percorso
- [ ] interfaccia usabile da telefono e da computer

**Verifichi tu**
- [ ] collaudo completo del percorso in prova, da computer e da telefono
- [ ] fai provare l'app ad almeno 1-2 persone vere e annoti cosa non capiscono (in `IDEAS.md` o come bug)

---

## M5 — Qualità e sicurezza

Status: planned · Versione alla chiusura: 0.9.0

> Prima di aprire l'app a utenti veri la si rende affidabile: errori
> comprensibili, niente falle note, problemi visibili quando accadono.

**Decidi tu**
- [ ] testi legali (privacy, cookie, termini): l'agente prepara una bozza, **non è consulenza legale**
- [ ] a chi arrivano gli avvisi quando l'app ha un errore

**Fa l'agente**
- [ ] messaggi di errore comprensibili per l'utente
- [ ] controllo dei dati inseriti e limiti contro gli abusi (es. troppi tentativi di accesso)
- [ ] nessun secret nel codice, dipendenze aggiornate e senza vulnerabilità note
- [ ] monitoraggio degli errori in produzione
- [ ] revisione di sicurezza dell'intera app (incrociata se usi due agenti)
- [ ] sezione *Sicurezza* di `CONSEGNA.md` aggiornata: cosa è stato verificato e cosa no

**Verifichi tu**
- [ ] tutti i collaudi di `TESTS.md` ripetuti in prova sulla versione 0.9.0: tutti `ok`

---

## MVP — Pubblicazione e consegna

Status: planned · Versione alla chiusura: 1.0.0

> L'app va online per utenti veri ed è pronta per essere presa in mano da uno
> sviluppatore.

**Decidi tu**
- [ ] il via libera alla pubblicazione in produzione

**Fa l'agente**
- [ ] pubblicazione in produzione, solo dopo il tuo ok
- [ ] versione `1.0.0`, tag e `CHANGELOG.md`
- [ ] `CONSEGNA.md` completo, compreso il *Debito tecnico*
- [ ] `STATE.md` aggiornato e nessun task `[MVP]` aperto

**Verifichi tu**
- [ ] collaudi principali ripetuti **in produzione**: tutti `ok`
- [ ] un ripristino da backup provato almeno una volta (in prova)
- [ ] un agente in una sessione nuova, o uno sviluppatore, avvia il progetto seguendo **solo** `CONSEGNA.md`

---

## Dopo l'MVP

Direzioni probabili, non ancora fasi. Niente lavoro su queste finché l'MVP non
è `done`.

- TO VERIFY

## Storico

Fasi chiuse o abbandonate, con data, versione e una riga di esito.

- TO VERIFY
