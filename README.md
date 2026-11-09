# Studio Dentistico Dal Bianco-Razzini — sito

Sito statico a pagina singola. Nessuna build: `index.html` + `assets/`.

## Struttura
- `index.html` — la pagina (font Cormorant incorporato in base64)
- `assets/studio-reception.{jpg,webp}` — foto di copertina, 2000px
- `assets/studio-reception-1200.{jpg,webp}` — variante mobile (<720px)
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
Le schede di "Aree di cura" non girano più: aprono un pannello che scorre sopra
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
In `#casi`, duplica un `<article class="case">` e compila:
- `.case-cover` — copertina (togli il commento e punta al file in `assets/casi/`)
- `.case-tag`, `h3`, `.case-sub` — etichetta, titolo e riga di sintesi
- `.case-detail` — testo lungo, `dl.sheet-facts` (durata, trattamento, equipe) e
  `.sheet-gallery` con una `<figure class="ba">` per ogni coppia prima/dopo:
  sostituisci i `<div class="ph-slot">` con gli `<img>`

I riquadri tratteggiati sono i posti vuoti e spariscono appena metti
un'immagine. Le foto vanno ottimizzate prima (webp ~1600px per le gallerie,
~1200px per le copertine).

> Nota: la riga sotto le schede dice che le immagini sono pubblicate con il
> consenso dei pazienti e che i risultati non sono garantiti. Va tenuta e
> adattata al testo del consenso che lo studio fa firmare.
