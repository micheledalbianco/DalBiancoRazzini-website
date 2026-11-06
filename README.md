# Studio Dentistico Dal Bianco-Razzini — sito

Sito statico a pagina singola. Nessuna build: `index.html` + `assets/`.

## Struttura
- `index.html` — la pagina (font Cormorant incorporato in base64)
- `assets/studio-reception.{jpg,webp}` — foto di copertina, 2000px
- `assets/studio-reception-1200.{jpg,webp}` — variante mobile (<720px)
- `netlify.toml` — publish dir e cache header

## Deploy
Netlify collegato a questo repo: ogni push su `main` pubblica.

## Foto ancora da sostituire
Nella pagina restano immagini segnaposto in base64 per:
- i 5 ritratti del team (Dal Bianco, Razzini, Chierici, Chiappini, igienista) e lo staff (Isa, Vasilica, Donia)
- le 3 immagini della striscia "Ambiente dello Studio"
