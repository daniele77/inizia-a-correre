# Opuscolo "Iniziare a correre"

[![Pages online](https://img.shields.io/badge/Pages-online-2ea44f)](https://daniele77.github.io/running_pamphlet/)
[![Download PDF](https://img.shields.io/badge/PDF-download-2ea44f)](https://daniele77.github.io/running_pamphlet/book.pdf)

Progetto LaTeX compilato con **XeLaTeX** tramite `latexmk`.

## Requisiti

Assicurati di avere installato:

- `texlive-xetex`
- `latexmk`
- pacchetti LaTeX usati dal progetto (`stix2`, `sourcesanspro`, `tcolorbox`, ecc.)

Su Debian/Ubuntu, ad esempio:

```bash
sudo apt update
sudo apt install texlive-xetex latexmk texlive-latex-extra texlive-fonts-extra
```

## Compilazione

Dalla root del progetto:

```bash
latexmk -pdf book.tex
```

La configurazione è definita in `latexmkrc`:

- motore: `xelatex`
- directory output: `build/`

PDF finale:

- `build/book.pdf`

## Workflow consigliato (scrittura)

Per lavorare in modo fluido, usa la compilazione continua:

```bash
latexmk -pvc -pdf book.tex
```

In questo modo, a ogni salvataggio di `book.tex` (o dei file inclusi) il PDF viene rigenerato automaticamente in `build/book.pdf`.

Per interrompere la modalità continua, premi `Ctrl+C` nel terminale.

Suggerimento pratico:

- tieni aperto `build/book.pdf` affiancato all'editor per vedere subito ogni modifica.

## Pulizia file generati

Pulizia standard:

```bash
latexmk -c
```

Pulizia completa (incluso PDF):

```bash
latexmk -C
```

## Note

- Le immagini sono nella cartella `images/`.
- In `book.tex` è impostato `\graphicspath{{images/}}`, quindi negli `\includegraphics` puoi usare solo il nome file.

## GitHub Actions

Sono presenti tre workflow:

- `build-pdf.yml`: build del PDF su push/PR con artifact scaricabile.
- `release-pdf.yml`: build e allegato PDF automatico alle release su tag `v*`.
- `pages-pdf.yml`: pubblicazione su GitHub Pages del PDF (`book.pdf`) con una pagina `index.html` minimale.

### Attivare GitHub Pages

Nel repository GitHub:

1. Vai in **Settings → Pages**.
2. In **Build and deployment**, seleziona **GitHub Actions** come source.

Dopo un push su `main`/`master` (o esecuzione manuale del workflow), il PDF sarà disponibile all'URL Pages del repo.

### Badge Pages nel README

Badge già configurato per questo repository:

```md
[![Pages online](https://img.shields.io/badge/PDF-GitHub%20Pages-blue)](https://daniele77.github.io/running_pamphlet/)
```

Esempio URL del PDF pubblicato:

- `https://daniele77.github.io/running_pamphlet/book.pdf`
