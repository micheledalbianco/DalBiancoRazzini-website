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

## Foto ancora da sostituire
Nella pagina restano immagini segnaposto in base64 per:
- i 5 ritratti del team (Dal Bianco, Razzini, Chierici, Chiappini, igienista) e lo staff (Isa, Vasilica, Donia)

## Ritocchi sulle foto
- `scansione-digitale`: rimosso il nome dell'utente visibile sullo schermo del
  laptop (clonata la porzione di interfaccia vuota alla stessa altezza). Il
  master 2000px ritoccato è in `_master/`, da lì si rigenera la webp.
