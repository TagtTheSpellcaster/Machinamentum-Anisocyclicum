# Machinamentum Anisocyclicum

![Brevetto meccanico](https://img.shields.io/badge/BREVETTO%20MECCANICO-1.1.2-b8860b)
![Machina](https://img.shields.io/badge/Machina%20N%C2%B0-006-8a6c42)
![Anno](https://img.shields.io/badge/anno-1894-5a4632)
![Licenza](https://img.shields.io/badge/licenza-AGPL--3.0-blue)
![HTML5](https://img.shields.io/badge/HTML5-canvas-e34f26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-f7df1e?logo=javascript&logoColor=black)
![Dipendenze](https://img.shields.io/badge/dipendenze-nessuna-brightgreen)
![File singolo](https://img.shields.io/badge/file-singolo-informational)

Enigma steampunk a treno di ingranaggi, in un unico file HTML. Machina N° 006 della serie OFFICINA DEGLI ENIGMI.

Il giocatore deve collegare un motore a uno o più perni scegliendo e posizionando ingranaggi dal vassoio, in modo che ogni perno giri con la velocità e il verso richiesti. Il gioco inizia con un tutorial animato sul funzionamento degli ingranaggi.

**BREVETTO MECCANICO 1.1.2 – 1894**

## Requisiti

- Un browser moderno con supporto per HTML5 Canvas e Web Audio.
- Nessuna installazione, nessuna dipendenza, nessuna connessione di rete.
- Facoltativo: il file `clockwork_cogitation.mp3` nella stessa cartella dell'HTML, per la musica di sottofondo. Se manca, il gioco funziona normalmente e il pulsante MUSICA mostra "FILE NON TROVATO".

## Avvio

Aprire `machinamentum-anisocyclicum.html` nel browser (doppio clic, oppure `File > Apri`). Con un server statico qualsiasi funziona allo stesso modo:

```
python3 -m http.server 8000
```

e poi `http://localhost:8000/machinamentum-anisocyclicum.html`.

## Come si gioca

- Trascinare gli ingranaggi dal vassoio sulla scacchiera. Si agganciano da soli agli ingranaggi vicini, ai perni (cerchi con croce) e alle posizioni di ingranamento valide.
- Doppio clic o clic destro su un ingranaggio posato lo rimette nel vassoio.
- Un tocco senza trascinamento su un ingranaggio singolo lo sposta sull'altro piano (ottone o rame).
- Le ruote ottone (piano posteriore) e rame (piano anteriore) ingranano solo con ruote dello stesso colore.
- Una ruota doppia ha due ingranaggi sullo stesso asse, uno per piano: girano insieme e collegano i due piani.
- Se due ingranaggi si bloccano a vicenda (rapporti incompatibili, per esempio tre ruote ingranate in cerchio) il treno è inceppato e le ruote tremano in rosso.
- Il livello è superato quando tutti i requisiti restano soddisfatti per 1,2 secondi (tolleranza del 5%).
- Non tutte le ruote del vassoio servono: da un certo livello in poi alcune sono inutili e devono restare fuori.

### Regola di calcolo

```
giri finali = giri del motore × denti del motore ÷ denti dell'ultima ruota
```

Le ruote intermedie (una per asse) non cambiano la velocità finale, ma invertono il verso a ogni ingranamento e coprono le distanze. Fa eccezione la ruota doppia, che cambia il rapporto.

## Livelli

| N. | Titolo |
|----|--------|
| 1 | Come funzionano gli ingranaggi (tutorial animato) |
| 2 | Verso concorde |
| 3 | Riduzione di giri |
| 4 | Moltiplicazione |
| 5 | Le colonne |
| 6 | Asse doppio |
| 7 | Due uscite |
| 8 | Tre colonne |
| 9 | Albero doppio, utenza fissa |
| 10 | Il bivio |
| 11 | Moltiplicazione composta |
| 12 | Il gran regolatore |

Ogni livello ha al massimo una ruota doppia.

## Musica e suoni

- Pulsante MUSICA: ON/OFF con cursore di volume orizzontale logaritmico (da −50 dB a 0 dB).
- Pulsante EFFETTI: ON/OFF per i suoni sintetizzati (Web Audio).
- Musica, volume e progressi sono salvati nel browser (`localStorage`: `mc_music`, `mc_vol`, `mc_done`, `mc_best`, `mc_tut`).

## Dettagli tecnici

- Un unico file HTML con CSS e JavaScript inline, rendering su `<canvas>` con scala per densità di pixel.
- Modello: raggio primitivo = 2,5 px × numero di denti; due ruote ingranano se la distanza fra i centri è la somma dei raggi (tolleranza 1,5 px) e collidono se è inferiore.
- Due piani (0 ottone, 1 rame); le ruote doppie condividono la velocità angolare.
- Cinematica: visita del grafo di ingranamenti con rapporti con segno; rilevamento dell'inceppamento in caso di rapporti in conflitto.
- Aggancio: punto più vicino sui cerchi di ingranamento, intersezioni fra cerchi, perni; preferenza per le posizioni che ingranano più ruote e per i perni.

## Verifiche

- Per i livelli 2–7 un risolutore automatico (ricerca con approfondimento iterativo) ha trovato una soluzione con le stesse regole del gioco.
- I livelli 8–12 sono stati verificati costruendo una soluzione; non è stata cercata la soluzione minima né verificata l'esistenza di soluzioni alternative.
- Tutti i livelli 2–12 sono stati risolti trascinando con il mouse in Chromium.

Non verificati: input touch su dispositivi reali, audio, Safari, difficoltà percepita da giocatori umani.

## Licenza

Distribuito con licenza GNU Affero General Public License, versione 3 (AGPL-3.0). Il testo completo è nel file `LICENSE`, da scaricare da <https://www.gnu.org/licenses/agpl-3.0.txt>. Chi ospita una versione modificata come servizio di rete deve offrire agli utenti il codice sorgente corrispondente.

## Serie

OFFICINA DEGLI ENIGMI · Machina N° 006 · BREVETTO MECCANICO 1.1.2 – 1894
