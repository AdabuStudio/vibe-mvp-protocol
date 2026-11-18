# Ideas

> Il parcheggio delle idee. Qui finisce tutto ciò che è venuto in mente ma non è
> deciso: feature, miglioramenti, refactor "già che ci sono", feedback degli
> utenti, intuizioni a metà.
>
> - Un'idea che nasce durante un task **va qui, non nel codice**.
> - L'agente può aggiungere (`raw`) e, se l'owner lo chiede, valutare (`evaluated`).
> - Solo l'owner promuove, parcheggia o scarta.
> - Le idee scartate **restano** con il motivo: evitano di riproporle.
> - Un'idea promossa porta il link a dove è finita (`→ T-031` o `→ M2`).

Stati: `raw` → `evaluated` → `promoted` | `parked` | `rejected`

Prossimo ID libero: I-001

## Template

```
### I-NNN — Titolo breve

Status: raw
Date: YYYY-MM-DD
Source: owner | agente (<nome>) durante T-NNN | feedback utente | altro

Problema / opportunità:
<cosa risolve o abilita, per chi>

Valutazione:            # compilare solo in stato evaluated
- Valore:  basso | medio | alto — <perché>
- Sforzo:  S | M | L — <perché>
- Rischi:  <cosa può rompere o complicare>
- Coerenza con VISION.md: sì | in tensione con <non-obiettivo>

Esito:                  # promoted → T-NNN / M-N · parked fino a <condizione> · rejected perché <motivo>
```

---

## Aperte

<!-- raw ed evaluated, le più recenti in alto -->

## Parcheggiate

<!-- parked: buone ma non ora. Indicare la condizione che le riapre. -->

## Chiuse

<!-- promoted e rejected, con l'esito. -->
