# Studio Dentistico Dal Bianco-Razzini — sito

Sito statico a pagina singola. Nessuna build: `index.html` + `assets/`.

## Struttura
- `index.html` — la pagina (font Cormorant incorporato in base64)
- `assets/studio-reception.{jpg,webp}` — foto di copertina, 2000px
- `assets/hero-mobile.{jpg,webp}` — hero su telefono (<720px): **ritaglio
  verticale** 890×1335 preso dall'originale a x=950. Su un telefono la finestra
  dell'hero è quasi 1:2 e `cover` su una foto 3:2 ne mostrava una fetta centrale
  illeggibile; questo ritaglio tiene insieme corridoio, logo FACExp e la scritta
  sul vetro. Per rifarlo:
  `convert 1.jpg -crop 890x1335+950+0 +repage -quality 74 hero-mobile.webp`
- `assets/studio-reception-1200.{jpg,webp}` — vecchia variante mobile, non più
  referenziata
- `assets/{sala-attesa,sala-operativa,sala-visita,ingresso-ascensore,
  sterilizzazione,scansione-digitale}.webp` — galleria "Lo studio", 1600px. Il crossfade è nello `<style id="gallery-cycle">`
  in fondo a `index.html`: per aggiungere una slide, inserisci l'`<img>` nella
  `.gallery`, porta la durata di `gcyc6` a N×2s, aggiungi un `nth-child` con
  delay (N-1)×2s e metti i due stop intermedi a 100/N−2 % e 100/N+4 %.
- `netlify.toml` — publish dir e cache header

## Deploy
Netlify collegato a questo repo: ogni push su `main` pubblica.

## Ritratti del team
`assets/{giuseppe-dal-bianco,luciana-razzini,viviana-salvalai,isa,vasilica,
donia}.webp`, 900px.
Sono verticali dentro riquadri quasi quadrati: `#team .ph img{object-position:
center 12%}` evita che `cover` tagli la fronte.

## Foto ancora da sostituire
Restano segnaposto stock in base64 (3 schede su 9):
- Dott. Davide Chiappini, "Igienista dentale", Lidia

## Ritocchi sulle foto
- `scansione-digitale`: rimosso il nome dell'utente visibile sullo schermo del
  laptop (clonata la porzione di interfaccia vuota alla stessa altezza). Il
  master 2000px ritoccato è in `_master/`, da lì si rigenera la webp.
- `Dott. Viviana Salvalai` ha foto e ruolo ma **nessuna bio**: la sua scheda ha
  sostituito quella del Dott. Alessandro Chierici ed è volutamente senza il
  retro apribile, che va riattivato quando arriva il testo.

## Pannello di dettaglio (aree di cura e casi clinici)
Le schede di "Aree di cura" non girano più ("tocca per i dettagli e i casi
clinici"): aprono un pannello che scorre sopra
il sito, con la pagina dietro sfocata (scheda centrata da 721px in su, foglio
dal basso su mobile). Stessa meccanica per i casi clinici.

Come funziona: ogni elemento `.area` o `.case` contiene un blocco marcato
`data-sheet-body`; al click quel blocco viene clonato dentro `#sheet`. Niente
testi duplicati — si modifica il contenuto dov'è già. Gli `.hint`
("Tocca per i dettagli") vengono tolti dal clone.

Il pannello chiude con la X, con Esc e cliccando fuori; blocca lo scroll della
pagina, confina il focus al suo interno e lo restituisce alla scheda di
partenza. Le schede del team continuano invece a girare (`.mem.doc`).

### Aggiungere foto a un'area di cura
Dentro `.area-f.back` c'è un `<div class="sheet-gallery"></div>` vuoto: bastano
uno o più `<img src="assets/casi/....webp" alt="..." loading="lazy"
decoding="async">`. Vuota non viene mostrata.

### Aggiungere un caso clinico
I casi stanno **dentro l'area di cura** a cui appartengono, non in una sezione a
parte: si aprono dallo stesso pannello, in fondo al dettaglio dell'area. Dentro
`.area-f.back` c'è un `<div class="casi-area">`: duplica un `<article
class="caso">` e compila titolo (`.caso-t`), `dl.sheet-facts` (durata,
trattamento, equipe), il racconto e la `.sheet-gallery` con una `<figure
class="ba">` per ogni coppia prima/dopo, sostituendo i `<div class="ph-slot">`
con gli `<img>`.


> Nota: la riga sotto le schede dice che le immagini sono pubblicate con il
> consenso dei pazienti e che i risultati non sono garantiti. Va tenuta e
> adattata al testo del consenso che lo studio fa firmare.

## Il blu
Campionato dalle foto dello studio: vetrata FACExp `#2B7AC1` e porta blu
`#0B3153` stanno entrambe su **hue 208,4°**, il roll-up a 212°. La palette era
a 217° (più indaco). Tutta la famiglia blu è stata riportata a 208,4°
mantenendo luminosità e saturazione, così cambia il "punto" di blu e non il
tono del sito:

| era | ora | dove |
| --- | --- | --- |
| `#14233b` | `#14293b` | `--ink` |
| `#1c2c46` | `#1c3246` | `--sage` |
| `#142338` | `#142738` | `--sage-deep`, `--hero` |
| `#263a5c` / `#1a2c47` | `#26425c` / `#1a3247` | gradiente hero |

Le casacche del personale sono un altro blu (195°, più ciano) e sono state
escluse di proposito. Gli altri colori non sono stati toccati.

## Marchio
Sorriso + due fossette ad arco puro, tutto bianco (`#f4efe6`), 44px accanto al
logotipo. Le fossette sono corte e sottili (tratto 10) e inclinate di 24° con la
cima verso l'interno: si alzano come gli angoli di una bocca, così l'insieme
legge come un sorriso stilizzato. Sono accostate di 9 unità verso il centro
(`translate(±9 0)`), non abbassate: la versione abbassata bilanciava meglio le
masse ma allontanava le fossette dagli angoli della bocca: a 36px era timido, a 52px prendeva il sopravvento sulla scritta. Sta
in header, footer e favicon (lo slot `.mk` c'era già ma era `display:none`).
È inline nell'HTML: per cambiarlo si modificano i `<path>` in `.brand .mk` e
`.foot-brand .mk` (due copie) e la favicon.

> Scartata l'idea delle fossette a forma di D e R: con le lettere leggibili il
> sorriso non si leggeva più come sorriso, e accennandole appena non si
> capivano.

## Carosello delle foto dello studio
Il tasto "Sfoglia" sulla striscia apre il pannello con le foto grandi: palco,
frecce, didascalia, contatore e miniature. L'elenco è costruito a runtime dalle
`.gallery img`, quindi **aggiungendo una foto alla striscia entra anche nel
carosello**; la didascalia si prende da `data-cap`. Si naviga anche con le
frecce della tastiera.

Il crossfade della striscia è a 5s per foto (ciclo `gcyc6` da 30s).

Sul dimensionamento del palco: `aspect-ratio` **e** `max-height` insieme fanno
restringere la larghezza al browser, che tiene il rapporto riducendo entrambi i
lati — risultato, un vuoto a destra (fino a 388px a 1280). La larghezza va
fissata (`width:100%`) e l'altezza limitata: la foto riempie sempre, al massimo
si ritaglia in verticale. Didascalia e contatore stanno in sovrimpressione sulla
foto, non in una riga a parte, così le miniature restano visibili senza
scrollare.

## Hero
Titolo su tre righe, tutte della stessa dimensione: "Da oltre 40 anni" è uno
`<span class="kicker">` dentro l'`<h1>` (solo `display:block`), così resta
un'unica intestazione per i motori di ricerca e per gli screen reader. Sottotitolo ridotto a "Centro ortodontico
FACExp di Cremona". Le recensioni sono state tolte da qui perché la valutazione
Google è già nella fascia dati subito sotto (dove ora si legge `4,4 / 5`).
I due tasti restano ma sono meno "pillola": angoli a 5px, etichette in
maiuscoletto spaziato, icona telefono su Chiamaci. Lo stile vale solo per
`.hero .btn`: altrove i bottoni sono ancora a pillola.

## Fascia dati
Il tile Google non ha il numero grande: ci sono le stelline e sotto
"4,4 VALUTAZIONE GOOGLE" come frase unica, nel carattere dell'etichetta.
Le stelle sono
un solo SVG: cinque sagome chiare e le stesse cinque in ottone ritagliate
all'88% con una `clipPath`, così la quinta risulta piena per poco meno di metà
— è il 4,4 vero, non cinque stelle piene. Per cambiare voto si sposta la
`width` del `rect` dentro `#st44` (voto/5 × 100).

Le quattro etichette sono allineate sulla stessa linea con `margin-top:auto` su
`.stats-row .stat .lbl`: serve la specificità a tre classi, perché più avanti
nel file c'è un `.stat .lbl` che altrimenti vince per posizione.

## Badge FACExp
Era una sezione intera (logo, titolo, due punti, nota "chi è l'ortodontista",
CTA). Ora è un badge di certificazione: scheda centrata con filetto ottone,
logo FACExp, "Studio della rete" e "Centro Ortodontico FACExp di Cremona".
FACExp non rilascia una certificazione: è una rete, e il testo lo dice così
sia nel badge sia nel tile della fascia dati.
Tutto il badge è un link a facexp.it (nuova scheda), e lo è anche il logo nel
tile "Certificazione" della fascia dati. Il testo che c'era prima è
recuperabile dalla storia git.

> L'indirizzo `facexp.it` è stato letto dal roll-up nella foto della sala
> d'attesa: da verificare se il sito cambia.
Tolta anche la voce "Centro FACExp" dai due menu: non è più una sezione.

## Tasti dell'hero
Due tasti sempre, ma il secondo cambia: da 821px in su "Scopri il nostro team"
(ancora a `#team`), sotto gli 820 "Chiamaci" con `tel:` che fa partire la
chiamata. Si scambiano via CSS (`.solo-desk` / `.solo-mob`), nessun JS: il
vecchio script che su desktop dirottava Chiamaci verso i contatti è stato
rimosso perché ora quel tasto sul desktop non esiste.

## Form di prenotazione
Prima non inviava nulla: il JS bloccava il submit e mostrava solo il messaggio
di conferma (c'era anche la nota "Anteprima dimostrativa").

Ora è un form **Netlify Forms**: `name="prenota"`, `method="POST"`,
`data-netlify="true"`, campo nascosto `form-name` e honeypot `bot-field`
(nascosto via `.hp`, fuori schermo e non raggiungibile da tab). Il JS invia in
POST con `fetch` e mostra il riquadro di conferma solo **dopo** l'ok del
server; se l'invio fallisce riabilita il tasto e mostra la riga rossa con il
numero di telefono.

Netlify rileva il form al deploy, quindi va deployato almeno una volta.
Le richieste finiscono in **Forms** nella dashboard; per riceverle via email
serve aggiungere una *form notification* lì — l'indirizzo non sta nel codice,
così non finisce in pasto agli spam-bot.

In locale (`python3 -m http.server`) l'invio **fallisce di proposito**: il POST
su `/` risponde 501 e si vede il messaggio d'errore. Si prova solo online.

> Da sistemare: il link "informativa privacy" accanto al consenso punta a `#`.
> Un form che raccoglie nome, telefono, email e motivo della visita ha bisogno
> di una pagina vera.

