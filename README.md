# Greco San Martino · Pallavolo Under 12

Webapp per gestire la squadra Under 12: giocatori con numero di maglia, valutazione dei fondamentali (Battuta, Ricezione, Attacco, Palleggio, Mobilità) da 1 a 10 con storico nel tempo, voto complessivo, preparazione automatica delle formazioni per i 3 set di ogni partita e archivio dei risultati.

È un unico file, `index.html`, senza dipendenze né build: basta aprirlo nel browser.

## Pubblicarla con GitHub Pages
1. Crea un nuovo repository su GitHub e carica i file di questa cartella (`index.html`, `README.md`, `.nojekyll`).
2. Vai su **Settings → Pages**.
3. In *Build and deployment* scegli **Deploy from a branch**, branch `main`, cartella `/ (root)`, poi **Save**.
4. Dopo circa un minuto l'app è online su `https://<tuo-utente>.github.io/<nome-repo>/`.

## Dove sono salvati i dati
I dati sono salvati in un database **Firebase (Firestore)** condiviso, protetto da login con email e password: gli allenatori che accedono vedono e modificano gli stessi dati da qualsiasi dispositivo.
- Gli utenti si creano in Firebase Console → Authentication → Users (non esiste la registrazione dall'app).
- Le regole di Firestore consentono lettura e scrittura solo agli utenti autenticati.
- Il documento unico `squadra/main` contiene giocatori, valutazioni e partite (come testo JSON).
- Al logout i dati vengono rimossi dal dispositivo.
- In Archivio c'è comunque "Copia backup" / "Ripristina da backup" per una copia di sicurezza.
- Al primo avvio, se il database è vuoto, la rosa viene precompilata con i 13 giocatori (voto iniziale 5).

## Come funzionano le formazioni
- Si scelgono i presenti e il capitano (che gioca il primo set).
- Per ogni set si propongono due versioni: la più forte in battuta in posizione 1 (palla nostra) o in posizione 2 (palla agli avversari).
- Si evita di mettere vicine giocatrici con voto basso, ricezione bassa o mobilità bassa (rispetto alla media dei presenti).
- Tutti giocano nei primi due set e la differenza tra un giocatore e l'altro è al massimo di 1 set; il terzo set va ai giocatori con il voto più alto.
- Le formazioni si possono ritoccare toccando due giocatori per scambiarli.
