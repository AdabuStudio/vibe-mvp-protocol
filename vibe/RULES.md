# Vibe MVP Protocol — Rules

Un metodo per permettere a una persona **che non è sviluppatore** di costruire
la propria app con AI coding agent, fino a un **MVP pubblicato e pronto da
consegnare a uno sviluppatore**. La memoria del progetto vive nel repository,
non nella chat: qualunque agente può riprendere il lavoro leggendo i file di
`vibe/`.

## Ruoli

- **owner** → la persona che guida l'app (`PROJECT.yaml` → `project.owner`).
  Decide visione, stack, roadmap, priorità e quali idee diventano lavoro.
- **agente** → un AI coding agent dichiarato in `PROJECT.yaml` →
  `agents.roster` (di default `claude` e `codex`). Esegue, propone, documenta.
  Non decide al posto dell'owner su prodotto, stack e priorità.

Le regole valgono identiche per tutti gli agenti: nessuno ha privilegi sugli
altri, salvo i ruoli che l'owner scrive in `agents.roles`.

## Lavorare con un owner che non è sviluppatore

`PROJECT.yaml` → `project.owner_experience` dice quanto spiegare
(`beginner` | `intermediate` | `developer`). Con `beginner`, il default:

- **Parla semplice.** Ogni termine tecnico, la prima volta che compare, si
  spiega in una riga. Il glossario di base è nel `README.md`.
- **Una decisione alla volta**, con l'opzione consigliata per prima, una
  alternativa realistica e le conseguenze: costo, tempo, quanto è difficile
  cambiarla dopo.
- **Le azioni dell'owner sono passo-passo.** Quando deve fare qualcosa lui
  (creare un account, cliccare in un pannello, pagare, configurare un dominio),
  l'agente scrive i passi numerati, cosa deve vedere alla fine e cosa
  riportare. Mai "configura X" e basta.
- **Mai secret in chat.** L'agente dice all'owner dove inserire chiavi e
  password (pannello del servizio, `.env` locale, password manager) e non gli
  chiede di incollarle nella conversazione.
- **Ogni "fatto" si può vedere.** A fine task l'agente dice cosa è cambiato a
  parole e come l'owner lo verifica: un indirizzo da aprire, una schermata, un
  segno verde su GitHub.
- **Prima delle cose irreversibili, chiedi.** Pubblicare in produzione,
  cancellare dati, cambiare la struttura del database di produzione, attivare
  un piano a pagamento: si spiega cosa succede e si aspetta l'ok esplicito.
- **Le domande dell'owner non sono interruzioni.** Se chiede "perché?", si
  risponde prima di proseguire.

Quando queste regole dicono "chiedi", si chiede all'owner.

## Prima di lavorare

Il protocollo si legge su **due livelli**: leggerlo tutto ad ogni avvio costa
contesto per niente.

**Sempre:**

1. `PROJECT.yaml`
2. `RULES.md` (questo file)
3. `STATE.md`
4. `TASKS.md`
5. `HANDOFF.md`
6. Git:

```bash
git status && git branch --show-current && git log --oneline -10
```

Poi sappi **chi sei** (il tuo nome in `agents.roster`) e **in che modalità** si
lavora (`agents.mode`). In parallelo, controlla in `TASKS.md` quali task sono già
presi da altri agenti prima di sceglierne uno.

**Solo quando servono:**

| File | Si legge quando |
|---|---|
| `ROADMAP.md` | scegli il prossimo task, chiudi una fase, o un task sembra fuori dalla fase attiva |
| `VISION.md` | fai una scelta di prodotto, i requisiti sono ambigui, o aggiungi qualcosa che l'utente vedrà |
| `IDEAS.md` | stai per annotare un'idea, o l'owner chiede delle idee |
| `TESTS.md` | scrivi o aggiorni test e collaudi, registri un esito, chiudi una fase |
| `CONSEGNA.md` | prendi una scorciatoia, tocchi infrastruttura, dati o permessi, chiudi una fase |
| `DECISIONS.md` | tocchi un'area già decisa o stai per contraddire una decisione (i titoli scorrili sempre) |
| `START.md` | solo al primo ingresso nel progetto |

Se `HANDOFF.md` ha una sezione **Interruzione** aperta, quello è il punto di
ripartenza: non ricominciare il task da capo.

## Fonte di verità

- Il codice e Git sono la verità tecnica.
- I file di `vibe/` sono la memoria operativa e di prodotto: visione, roadmap,
  task, idee, decisioni. Versionati con il codice.
- Se documentazione e realtà divergono: verifica il codice, verifica Git,
  aggiorna la documentazione.

`STATE.md` riporta `Last verified commit`. Se diverge da `HEAD`, prima capisci
cosa è cambiato:

```bash
git log --oneline <sha>..HEAD
```

## Il metodo

```
VISION  →  ROADMAP (M0 … MVP)  →  TASKS  →  codice
   ↑            ↑
   └── IDEAS ───┘   (solo se l'owner le promuove)
```

- `VISION.md` → **perché** esiste l'app e per chi. Cambia raramente.
- `ROADMAP.md` → **il percorso** fino all'MVP. È già scritto con le fasi che ogni
  app attraversa — idea e cantiere, infrastruttura, dati, utenti e permessi,
  funzione chiave, qualità e sicurezza, pubblicazione e consegna — e per
  ognuna dice cosa decide l'owner, cosa fa l'agente e cosa verifica l'owner.
  L'ultima fase è sempre **MVP**.
- `TASKS.md` → **cosa si fa adesso**. Ogni task serve una fase.
- `IDEAS.md` → il **parcheggio** di tutto ciò che non è ancora deciso.

Regole:

- Una sola fase `active` alla volta, nell'ordine della roadmap.
- Un task che non serve la fase attiva non va in `NOW`.
- Visione e roadmap le cambia l'owner: l'agente propone (dividere una fase,
  saltarne una che non serve), e scrive solo dopo l'ok.
- Una fase si chiude quando tutte le sue caselle sono spuntate **e verificate**,
  compresi i collaudi dell'owner. Non basta che i task siano chiusi.
- Alla chiusura di una fase l'agente: aggiorna versione e `CHANGELOG.md`,
  aggiorna `CONSEGNA.md` e `STATE.md`, segna la fase `done` con data e
  versione, e chiede all'owner l'ok per attivare la successiva.
- **L'MVP è il traguardo.** Tutto ciò che non serve all'MVP aspetta: va in
  `IDEAS.md` o in *Dopo l'MVP* della roadmap.

## Stack e infrastruttura

Lo stack lo sceglie l'owner, e si scrive in `PROJECT.yaml` → `stack`.

- Se un campo di `stack` è vuoto e il task ne ha bisogno, **l'agente chiede**.
  Può proporre la preferenza indicata in `stack.preferred`, ma non la dà per
  scelta senza risposta.
- Non aggiungere servizi, provider o piattaforme non dichiarati in `stack`.
- Una scelta di stack confermata va anche in `DECISIONS.md`.
- Account, chiavi e pannelli dei servizi li gestisce l'owner. L'agente non crea
  account, non cambia piani a pagamento, non deploya in produzione senza una
  richiesta esplicita.

## Idee

Un'idea che nasce durante il lavoro — una feature in più, un refactor "già che ci
sono" — **va in `IDEAS.md`, non nel codice**. È così che lo scope resta sotto
controllo e l'MVP arriva.

- L'agente può **aggiungere** idee (`raw`) e, se l'owner lo chiede, **valutarle**
  (`evaluated`).
- Solo l'owner le **promuove**, le **parcheggia** o le **scarta**. Le scartate
  restano nel file con il motivo.

## Durante il lavoro

- Non rifare lavoro già completato.
- Non modificare parti non necessarie al task.
- Preservare le modifiche di altri agenti; prima di toccare un file modificato da
  altri, `git diff`.
- Non cambiare architettura senza una ragione concreta.
- Non introdurre dipendenze inutilmente.
- Non eliminare codice senza verificarne l'uso.
- Secret solo in `.env` locale, mai committato; `.env.example` aggiornato ad ogni
  nuova variabile. Mai stampare valori di secret in chat o nei log.
- Niente force push, niente reset distruttivi, niente modifiche dell'utente scartate.
- Modifiche piccole, verificabili e reversibili.

## Versioni

L'app ha una versione fin dal primo giorno, così si sa sempre cosa è
pubblicato e si può tornare indietro.

- Formato `MAGGIORE.MINORE.CORREZIONE`. Fino all'MVP la versione è `0.x.y`;
  l'MVP è `1.0.0`.
- Chiusura di una fase → la versione indicata in `ROADMAP.md` (`0.1.0`, `0.2.0`…).
- Correzione di un errore tra una fase e l'altra → si alza l'ultimo numero
  (`0.3.0` → `0.3.1`).
- La versione sta in `PROJECT.yaml` → `project.version` e nel file di
  configurazione dell'app (es. `package.json`): devono coincidere.
- **`CHANGELOG.md`** alla radice del repo, scritto per l'owner, non per
  sviluppatori: cosa cambia per chi usa l'app. La sezione *Non ancora
  pubblicato* si aggiorna a ogni task utile; alla nuova versione prende numero
  e data.

```markdown
## [0.4.0] - 2026-03-12
### Aggiunto
- Accesso con email e password, con recupero della password.
### Corretto
- La lista prenotazioni ora si vede anche da telefono.
```

- A ogni versione si crea un **tag** Git `vX.Y.Z`, dopo l'ok dell'owner sulla
  chiusura della fase. Il tag è il punto a cui si può tornare: se una versione
  pubblicata ha un problema grave, si ripubblica il tag precedente.
- Messaggi di commit: `tipo(T-NNN): descrizione`, con `tipo` tra `feat`
  (funzione nuova), `fix` (correzione), `test`, `docs`, `chore` (manutenzione).

## Test e collaudi

Due livelli, entrambi in `TESTS.md`:

- **Test automatici** — li scrive l'agente, insieme al codice, non dopo.
  - Ogni funzione nuova ha almeno un test; ogni riga della tabella dei permessi
    ha il suo test; ogni errore corretto ha un test che lo avrebbe trovato.
  - Girano su GitHub a ogni modifica (CI). **Un task non è fatto se i test non
    passano.**
  - L'owner non deve leggerli: l'agente gli dice se sono verdi e dove vederlo.
- **Collaudi** — li fa l'owner, a mano.
  - L'agente li scrive in `TESTS.md` in parole semplici, uno per ogni cosa che
    l'owner deve verificare nella fase (la sezione *Verifichi tu* di
    `ROADMAP.md`), e indica su quale ambiente farli.
  - L'esito lo dice l'owner; la riga la può scrivere l'agente.
  - Un collaudo `ko` diventa un task di correzione collegato (`Correggere
    C-007`). Dopo la correzione si ripete.
  - Una fase si chiude solo con tutti i suoi collaudi `ok` sulla versione che
    si sta chiudendo.

## Debito tecnico e consegna

L'obiettivo finale è un MVP che uno **sviluppatore** possa prendere in mano.
Per questo `CONSEGNA.md` si scrive durante il lavoro, non alla fine.

- Per arrivare all'MVP si prendono scorciatoie: sono lecite, ma ognuna va
  scritta subito in `CONSEGNA.md` → *Debito tecnico*, con rischio e come si
  sistemerebbe. Una scorciatoia non scritta è un difetto nascosto.
- Sulle aree critiche — accesso, permessi, pagamenti, dati personali —
  scorciatoie non se ne prendono.
- Ogni fase aggiorna le sezioni di `CONSEGNA.md` che la riguardano (ambienti,
  servizi, modello dati, permessi, sicurezza).
- `CONSEGNA.md` non contiene mai secret: solo nomi delle variabili e dove si
  trovano i valori.

## Task

- Ogni task ha un ID stabile (`T-001`, mai riusato) e la fase che serve.
- I task in `NOW` sono **bounded**: hanno un `Done when:` verificabile senza
  intervento umano (test che passa, build pulita, schermata che si apre,
  endpoint che risponde).
- Aggiornare `TASKS.md` quando un task si chiude, ne emerge uno nuovo, cambia la
  priorità o compare un blocker.

## Decisioni e stato

- Le decisioni significative, tecniche e di prodotto, vanno in `DECISIONS.md`.
  Non si riaprono salvo nuova evidenza, bug, requisiti cambiati o richiesta
  esplicita.
- `STATE.md` descrive il progetto **adesso**. Non è un diario. Si aggiorna, con
  `Last verified commit`, quando il progetto cambia materialmente.

## Fine sessione

Prima di chiudere una sessione significativa:

1. verificare il lavoro, eseguire test e build: devono passare;
2. committare;
3. aggiornare `STATE.md`, `TASKS.md` e la sezione *Non ancora pubblicato* di
   `CHANGELOG.md`;
4. aggiornare `ROADMAP.md` (caselle spuntate, fase chiusa) e `TESTS.md` (nuovi
   collaudi da fare);
5. aggiornare `CONSEGNA.md` se hai preso scorciatoie o toccato infrastruttura,
   dati o permessi; `DECISIONS.md` e `IDEAS.md` se serve;
6. riscrivere `HANDOFF.md`;
7. dire all'owner, in parole semplici: cosa è cambiato, come vederlo, e quali
   collaudi lo aspettano.

## Handoff

`HANDOFF.md` è il testimone tra una sessione e la successiva, anche quando la
successiva è un altro agente. Descrive solo il passaggio corrente: si riscrive,
non si accoda.

Deve dire sempre:

- chi esce (agente + modello) e chi è atteso (`claude`, `codex` o "chiunque");
- cosa è stato fatto e su quale branch;
- cosa è a metà e il prossimo passo concreto;
- cosa **non** è stato verificato;
- cosa non va toccato senza motivo.

Scrivilo per un lettore che non ha visto la tua conversazione e usa un altro
strumento: niente rimandi a "come detto prima", niente comandi propri del tuo
tool senza l'equivalente in shell.

## Interruzione a metà task

Limite di token, crash, cambio agente.

**Chi esce:**

1. non lascia il working tree sporco:

```bash
git add -A && git commit -m "wip(T-NNN): <task> — interrotto, vedi HANDOFF"
```

   (se il lavoro è instabile, prima `git switch -c <prefisso>wip-T-NNN`);
2. scrive in `HANDOFF.md` la sezione **Interruzione**: motivo, file toccati con
   stato (completo / a metà / non iniziato), ultimo comando e suo esito reale,
   comando successivo previsto, cosa **non** è stato verificato;
3. aggiunge il proprio nome in `agents.worked_so_far`.

**Chi entra** legge `HANDOFF.md`, controlla con `git diff` che corrisponda alla
realtà e continua da lì. Se divergono, vince `git diff` e va segnalato. Se
l'uscita è stata improvvisa e non c'è niente di scritto, ricostruisce da
`git status && git diff && git log --oneline -5`.

## Più agenti

Il progetto è pensato per essere lavorato da più agenti — di default **Claude
Code** (`claude`) e **Codex** (`codex`) — anche su fornitori diversi. Funziona
perché nessuno dei due si fida della propria memoria: tutto passa dai file di
`vibe/` e da Git.

### Ingresso

Ogni strumento legge al boot un file diverso: Codex `AGENTS.md`, Claude Code
`CLAUDE.md`. **La fonte è `AGENTS.md`**; `CLAUDE.md` lo importa e basta. Regole
di progetto non si scrivono in nessuno dei due: stanno in `vibe/`.

### Identità

Ogni agente si riconosce con il nome che ha in `agents.roster` e lo usa ovunque:

- nei task presi (`@claude`, `@codex`);
- nei branch (`branch_prefix`, es. `codex/T-014-login`);
- nei commit, con il trailer `Agent:`:

```
feat(T-014): form di login

Agent: codex
```

Così `git log` dice chi ha fatto cosa, anche quando lo strumento non lo aggiunge.

### Modalità sequenziale (`agents.mode: sequential`)

Un agente alla volta, sullo stesso branch o su `main`.

- Si lavora, si chiude con la procedura di *Fine sessione*, si passa il
  testimone con `HANDOFF.md`.
- Chi entra dopo un agente **di un altro fornitore** applica comunque il
  controllo di *Interruzione*: `HANDOFF.md` contro `git diff`, prima di toccare
  codice.

### Modalità parallela (`agents.mode: parallel`)

Più agenti nello stesso momento. Le regole servono a non pestarsi i piedi:

1. **Un task, un agente.** Prima di iniziare, l'agente prende il task in
   `TASKS.md` aggiungendo `@<nome>` e il branch, e committa questa sola riga
   **su `main`**, prima di creare il suo branch: è l'unico commit diretto su
   `main` ammesso, e serve perché l'altro agente lo veda. Un task già preso non
   si tocca. Per vedere i task presi da un worktree:

```bash
git show main:vibe/TASKS.md
```
2. **Un agente, un branch** (meglio: un worktree suo). Mai due agenti sullo
   stesso branch, mai lavoro diretto su `main`.

```bash
git worktree add ../<repo>-codex -b codex/T-014-login
```

3. **Task che non si sovrappongono.** Se due task toccano gli stessi file o la
   stessa migrazione di database, non vanno in parallelo: uno aspetta in `NEXT`.
4. **File di `vibe/` in parallelo:** sul proprio branch l'agente aggiorna solo
   la riga del suo task in `TASKS.md` e la **sua sezione** di `HANDOFF.md`.
   `STATE.md`, `ROADMAP.md` e `DECISIONS.md` li aggiorna chi integra, dopo il
   merge. Idee nuove sì, in fondo ad `IDEAS.md`, con ID preso al momento.
5. **Integrazione.** I branch li porta su `main` `agents.integrator` (di default
   l'owner). Un agente non fa merge su `main` e non fa push se non è lui
   l'integratore o l'owner non lo chiede.
6. **Niente orchestrazione a catena.** Un agente non lancia altri agenti di primo
   livello; può usare sotto-sessioni del proprio strumento (vedi *Scelta del
   modello*).

### Revisione incrociata

Due fornitori diversi vedono errori diversi: è il vantaggio di avere sia
Claude che Codex. Per i casi in `agents.cross_review` — di default task
`CRITICAL` (auth, permessi, pagamenti, dati, migrazioni distruttive, produzione)
e chiusura di una fase — il lavoro di un agente lo **rivede l'altro** prima del
merge.

- Chi chiede la revisione lo scrive in `HANDOFF.md` → *Revisione richiesta*:
  branch, task, cosa guardare.
- Chi rivede **non riscrive il lavoro**: elenca i problemi trovati, ciascuno con
  file, riga e scenario concreto in cui si rompe, e li mette nella stessa
  sezione con l'esito (`ok` / `da correggere`).
- Le correzioni le fa l'autore, o chi indica l'owner.

### Disaccordi tra agenti

Se un agente trova una scelta di un altro che ritiene sbagliata, non la
riscrive di sua iniziativa: se è in `DECISIONS.md` vale la regola delle
decisioni; altrimenti la segnala in `HANDOFF.md` e decide l'owner.

## Scelta del modello

Si usa il **modello più economico che fa bene il task**. I modelli premium sono
uno strumento di escalation, non il default. Le regole parlano solo di tier; i
nomi dei modelli di ogni agente stanno in `PROJECT.yaml` →
`agents.roster.<agente>.models`. Se il tier che serve è vuoto per il tuo agente,
dillo: non inventare un nome di modello.

| Il task è | Tier |
|---|---|
| CSS, UI minore, rinomina, documentazione, contenuti, test banali, CRUD ovvio | `economic` |
| feature normale, API, componente, refactor locale, bug con causa nota, specifica chiara | `base` (default) |
| causa sconosciuta, architettura, più moduli, performance, requisiti ambigui | `premium` per capire e pianificare, poi `base` per eseguire |
| auth, permessi, pagamenti, dati sensibili, migrazioni distruttive, produzione | `premium` per il piano, revisione prima di applicare |

Regole:

- **Due tentativi falliti sullo stesso problema = stop.** Si documenta il
  problema e si propone di salire di tier, non si fa un terzo tentativo uguale.
- Trovata la causa o fatto il piano, si **torna giù** di tier per eseguire.
- Per un pezzo di lavoro a un tier diverso non serve cambiare sessione: si
  **delega a una sotto-sessione** con un mandato chiuso (obiettivo, area, criterio
  di fine). La sotto-sessione non rilegge il protocollo e non scrive nei file di
  `vibe/`: quelli li aggiorna solo la sessione principale.
- Se serve cambiare il modello della sessione principale, l'agente si ferma e
  scrive in `HANDOFF.md` quale tier serve e perché.
- Su `SIMPLE` e `STANDARD` l'agente procede senza chiedere. L'escalation si
  propone in una frase, solo quando è utile.
- Un'escalation può anche essere **verso l'altro agente**: dopo due tentativi
  falliti, un modello premium di un altro fornitore spesso sblocca dove il tuo
  si è incagliato. Si propone in `HANDOFF.md`, non si lancia da soli.
- Un tier in `agents.forbid_tiers` non si usa: se il task lo richiederebbe, ci
  si ferma e lo si scrive.

## Strumenti esterni

Il protocollo funziona con il solo repository. Se si usano anche tracker, wiki o
memorie AI esterne: il repo resta la fonte, e l'agente non scrive su servizi
esterni se l'owner non lo chiede in quella sessione.
