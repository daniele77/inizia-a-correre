# Opuscolo "Iniziare a correre"

[![Pages online](https://img.shields.io/badge/Pages-online-2ea44f)](https://daniele77.github.io/inizia-a-correre/)
[![Download PDF](https://img.shields.io/badge/PDF-download-2ea44f)](https://daniele77.github.io/inizia-a-correre/book.pdf)
[![Licenza: CC BY-NC-SA 4.0](https://img.shields.io/badge/Licenza-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

Progetto LaTeX compilato con **XeLaTeX** tramite `latexmk`.

## Licenza

Quest'opera è distribuita con licenza **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)**.

- Testo completo della licenza: `LICENSE`
- Sintesi leggibile: <https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it>

### Attribuzione consigliata

Se riusi o adatti questo materiale, puoi usare questa formula:

> Pallastrelli, Daniele. *Fatti un regalo: inizia a correre*. Licenza CC BY-NC-SA 4.0. Repo: <https://github.com/daniele77/inizia-a-correre>

## Struttura del progetto

Il file `book.tex` è ora un orchestratore leggero che include i moduli principali:

- `tex/preamble.tex`: pacchetti, font, colori, macro e opzioni globali.
- `tex/frontmatter.tex`: copertina, pagine iniziali e indice.
- `content/main.tex`: contenuto del libro (capitoli) in un unico file.
- `tex/backcover.tex`: retro-copertina.

Questa organizzazione mantiene la modifica semplice (senza un file per capitolo) e rende più facile trovare le sezioni da aggiornare.

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

In questo modo, a ogni salvataggio di `book.tex` o dei file inclusi (`tex/*.tex`, `content/*.tex`) il PDF viene rigenerato automaticamente in `build/book.pdf`.

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

Sono presenti quattro workflow:

- `build-pdf.yml`: build del PDF su push/PR con artifact scaricabile.
- `release-pdf.yml`: build e allegato PDF automatico alle release su tag `v*`.
- `pages-pdf.yml`: pubblicazione su GitHub Pages del PDF (`book.pdf`) con una pagina `index.html` minimale.
- `lint-actions.yml`: validazione dei workflow GitHub Actions con `actionlint` su push/PR ai file `.github/workflows/*`.

### Attivare GitHub Pages

Nel repository GitHub:

1. Vai in **Settings → Pages**.
2. In **Build and deployment**, seleziona **GitHub Actions** come source.

Dopo un push su `main`/`master` (o esecuzione manuale del workflow), il PDF sarà disponibile all'URL Pages del repo.

### Badge Pages nel README

Badge già configurato per questo repository:

```md
[![Pages online](https://img.shields.io/badge/PDF-GitHub%20Pages-blue)](https://daniele77.github.io/inizia-a-correre/)
```

Esempio URL del PDF pubblicato:

- `https://daniele77.github.io/inizia-a-correre/book.pdf`
