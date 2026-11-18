# Test e collaudi

> Due livelli di verifica, entrambi obbligatori per chiudere una fase:
>
> - **Test automatici** → li scrive e li esegue l'agente. Girano da soli su
>   GitHub a ogni modifica. Tu guardi solo il segno: verde = ok, rosso = c'è un
>   problema.
> - **Collaudi** → li fai **tu**, a mano, usando l'app come farebbe un utente.
>   L'agente li scrive qui in parole semplici; tu li esegui e annoti l'esito.
>
> Regole in `RULES.md` → *Test e collaudi*.

## Test automatici

Comando per eseguirli: TO VERIFY
Dove vedi l'esito: GitHub → scheda **Actions** del repository
Cosa coprono: TO VERIFY

## Come si fa un collaudo

1. Apri l'ambiente indicato nello scenario: **locale**, **prova** o **produzione**.
2. Entra con l'utente di prova del ruolo indicato. Le credenziali di prova
   stanno nel tuo password manager, **mai in questo file**.
3. Segui i passi uno per uno.
4. Confronta quello che vedi con il *Risultato atteso*.
5. Aggiungi una riga negli esiti: `ok`, oppure `ko` e cosa hai visto (uno
   screenshot aiuta). Basta dirlo all'agente: la riga la scrive lui.

Un collaudo `ko` diventa un task di correzione in `TASKS.md`, collegato al
collaudo (`T-031 [M3] Correggere C-007`). Dopo la correzione, il collaudo si
ripete.

Una fase si chiude solo quando tutti i suoi collaudi hanno l'ultimo esito `ok`
**sulla versione che si sta chiudendo**.

## Formato

```
### C-NNN [Fase] Titolo

Ambiente: locale | prova | produzione
Ruolo: nessuno | <ruolo>
Passi:
1. ...
Risultato atteso:
...

| Data | Versione | Ambiente | Esito | Note |
|---|---|---|---|---|
```

Prossimo ID libero: C-003

---

## Scenari

### C-001 [M0] L'app si avvia sul tuo computer

Ambiente: locale
Ruolo: nessuno
Passi:
1. Apri il terminale nella cartella del progetto.
2. Esegui il comando di avvio scritto in `STATE.md` → *Run*.
3. Apri nel browser l'indirizzo che il comando ti mostra.

Risultato atteso:
Si apre la pagina iniziale dell'app, senza errori.

| Data | Versione | Ambiente | Esito | Note |
|---|---|---|---|---|

### C-002 [M3] Un utente non può fare ciò che il suo ruolo non permette

Ambiente: prova
Ruolo: TO VERIFY (il ruolo con meno permessi)
Passi:
1. TO VERIFY — l'agente lo compila dalla tabella dei permessi.

Risultato atteso:
L'azione viene bloccata con un messaggio comprensibile, e i dati non cambiano.

| Data | Versione | Ambiente | Esito | Note |
|---|---|---|---|---|
