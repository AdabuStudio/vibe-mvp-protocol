# Decisions

Questo file contiene decisioni consolidate, di due tipi:

- **tech** → stack, architettura, schema dati, librerie, convenzioni;
- **product** → cosa si fa e cosa no, cambi di scope, scelte di priorità che non
  si leggono dal codice (es. "niente login social nell'MVP").

Non aggiungere supposizioni come fatti.

Quando una decisione è dedotta dal codice ma non documentata esplicitamente, usare:

**Status:** inferred

Quando è stata confermata esplicitamente dall'owner, usare:

**Status:** confirmed

Una decisione superata non si cancella: si marca **Status:** superseded e si
indica quale la sostituisce.

---

## Template

### YYYY-MM-DD — Titolo decisione

**Area:** tech | product
**Status:** inferred | confirmed | superseded by <titolo>

#### Decision

...

#### Reason

...

#### Evidence

...

#### Do not change unless

...
