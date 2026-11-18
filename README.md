# Vibe MVP Protocol

Un metodo per costruire **la tua app con l'intelligenza artificiale anche se non
sei uno sviluppatore**, usando Claude Code e Codex, fino a un **MVP**: una prima
versione pubblicata, usabile da persone vere e pronta da consegnare a uno
sviluppatore.

Il protocollo è un insieme di file nella cartella `vibe/` del tuo progetto.
Gli agenti AI li leggono a ogni sessione: così ricordano cosa è stato fatto,
cosa hai deciso e cosa manca, anche se cambi agente o ricominci il giorno dopo.

## Onboarding in 3 passi

1. **Crea il progetto** partendo da questo modello:

   ```bash
   git clone https://github.com/AdabuStudio/vibe-mvp-protocol.git mia-app
   ```

   ```bash
   cd mia-app && rm -rf .git && git init
   ```

2. **Apri Claude Code o Codex** nella cartella `mia-app`.
3. **Scrivi:**

   > Leggi `vibe/START.md` ed eseguilo.

L'agente ti spiega il percorso e ti fa una decina di domande semplici, ognuna
con una risposta consigliata. In 10-15 minuti sei pronto per la prima tappa.

Hai già un progetto? Copia dentro la cartella `vibe/`, `AGENTS.md` e
`CLAUDE.md`, poi fai il passo 3: l'agente ricostruisce lo stato dal codice.

## Il percorso

| Tappa | Cosa succede | Versione |
|---|---|---|
| **M0** Idea e cantiere | chiarisci l'idea, scegli gli strumenti, il progetto si avvia sul tuo computer | 0.1.0 |
| **M1** Infrastruttura | l'app vive in tre posti: il tuo computer, un ambiente di prova, la produzione | 0.2.0 |
| **M2** Dati | quali informazioni conserva l'app e come sono collegate | 0.3.0 |
| **M3** Utenti e permessi | chi entra, come, e cosa può fare ciascuno | 0.4.0 |
| **M4** Funzione chiave | il percorso principale dell'app funziona dall'inizio alla fine | 0.5.0 |
| **M5** Qualità e sicurezza | errori comprensibili, niente falle note, problemi visibili | 0.9.0 |
| **MVP** Pubblicazione e consegna | l'app va online e lo sviluppatore ha tutto per continuare | 1.0.0 |

Per ogni tappa `vibe/ROADMAP.md` dice **cosa decidi tu**, **cosa fai tu** (con
istruzioni passo-passo), **cosa fa l'agente** e **cosa verifichi tu**. Le tappe
che non servono alla tua app si saltano; quelle grandi si dividono.

## Cosa fai tu

- **Decidi**: cosa deve fare l'app, per chi, cosa non deve fare, chi può fare cosa.
- **Crei gli account** dei servizi (GitHub, Cloudflare, Neon…) seguendo le
  istruzioni dell'agente. Le password e le chiavi le tieni in un password
  manager: **non incollarle mai in chat**.
- **Collaudi**: a ogni tappa provi l'app a mano seguendo dei piccoli scenari
  scritti in `vibe/TESTS.md`, e dici all'agente se va tutto bene.
- **Dai il via libera** alle cose che non si possono annullare: pubblicare,
  cancellare dati, attivare un piano a pagamento.

Tutto il resto lo fa l'agente: scrive il codice e i test automatici, tiene le
versioni, documenta, e ti spiega cosa ha fatto e come verificarlo.

## I file

| File | A cosa serve |
|---|---|
| `vibe/START.md` | l'onboarding: si usa una volta sola |
| `vibe/VISION.md` | perché esiste l'app, per chi, cosa non fa |
| `vibe/ROADMAP.md` | il percorso a tappe fino all'MVP, con le caselle da spuntare |
| `vibe/TASKS.md` | il lavoro di adesso |
| `vibe/IDEAS.md` | il parcheggio delle idee: si decide dopo se farle |
| `vibe/TESTS.md` | test automatici e collaudi che fai tu |
| `vibe/CONSEGNA.md` | il documento per lo sviluppatore che prenderà in mano l'app |
| `vibe/DECISIONS.md` | le decisioni prese e perché |
| `vibe/STATE.md` | com'è il progetto adesso, come si avvia |
| `vibe/HANDOFF.md` | il passaggio di consegne tra una sessione e l'altra |
| `vibe/PROJECT.yaml` | nome, versione, strumenti scelti, agenti |
| `vibe/RULES.md` | le regole che seguono gli agenti |
| `CHANGELOG.md` | cosa cambia a ogni versione (lo crea l'agente in M0) |
| `AGENTS.md`, `CLAUDE.md` | il punto d'ingresso per Codex e Claude Code |

## Strumenti consigliati

Il protocollo non impone niente: gli strumenti li scegli tu. Come partenza
consiglia **GitHub** (dove sta il codice e girano i test), **Cloudflare** (dove
gira l'app) e **Neon** (dove stanno i dati): all'inizio costano zero o quasi.
L'agente te li propone e ti spiega le alternative.

## Claude e Codex insieme

Puoi usare un solo agente o entrambi, configurandolo in `vibe/PROJECT.yaml` →
`agents`.

- **Uno alla volta**: si passano le consegne con `vibe/HANDOFF.md`.
- **In parallelo**: ognuno prende un task diverso (`@claude`, `@codex`) e
  lavora sulla sua copia (branch); le unisci tu, o l'agente che indichi.
- **Revisione incrociata**: sulle parti critiche (accesso, permessi, dati,
  pubblicazione) e alla fine di ogni tappa, il lavoro di uno lo rivede l'altro.
  Due "cervelli" diversi trovano errori diversi.

## Glossario minimo

| Parola | Significato |
|---|---|
| **repository (repo)** | la cartella del progetto con tutta la sua storia |
| **commit** | un salvataggio del progetto, con una descrizione |
| **branch** | una copia di lavoro separata, che poi si unisce a quella principale (`main`) |
| **tag / versione** | un salvataggio con un nome (`v0.3.0`) a cui si può sempre tornare |
| **ambiente** | un posto dove gira l'app: locale (il tuo computer), prova, produzione |
| **deploy / pubblicare** | mettere online una versione dell'app |
| **database** | dove l'app conserva i dati |
| **migrazione** | una modifica alla struttura del database, salvata e ripetibile |
| **variabile d'ambiente / secret** | un'impostazione o una chiave segreta tenuta fuori dal codice |
| **CI** | i controlli automatici che GitHub fa a ogni modifica (segno verde o rosso) |
| **test automatico** | un controllo scritto in codice che verifica che una funzione vada |
| **collaudo** | una prova che fai tu a mano, usando l'app |
| **MVP** | la prima versione utile, con il minimo indispensabile |
| **debito tecnico** | una scorciatoia presa per andare veloci, da sistemare in futuro |

## Aggiornare il protocollo in un progetto

Si sovrascrivono solo i file del metodo: `vibe/RULES.md`, `vibe/START.md`,
`AGENTS.md`, `CLAUDE.md` (se contengono solo l'entrypoint). Tutti gli altri
file di `vibe/` sono il contenuto del tuo progetto e non si toccano.

## Versione

Protocollo v1
