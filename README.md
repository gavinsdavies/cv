
# My Personal CV

[![LaTeX Build Status](https://github.com/gavinsdavies/cv/actions/workflows/build-latex.yml/badge.svg)](https://github.com/gavinsdavies/cv/actions)
[![PDF](https://img.shields.io/badge/PDF-latest-purple.svg?style=flat)](../orphan/lualatex/gavinsdavies.pdf)

## Build Source Of Truth

The published PDF is built by GitHub Actions using the workflow at [.github/workflows/build-latex.yml](.github/workflows/build-latex.yml).

The workflow compiles with LuaLaTeX and pushes the generated PDF to the orphan/lualatex branch. The badge and PDF link above track that automated build.

## Local Build Notes

Local compilation is optional and mainly useful for previewing changes before pushing. If you build locally, use LuaLaTeX, not pdfLaTeX.

## VS Code Integration

This workspace includes LaTeX Workshop settings in [.vscode/settings.json](.vscode/settings.json) that set the default recipe to `latexmk (lualatex)`.

Recommended setup:

- Install [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop).
- Open [gavinsdavies.tex](gavinsdavies.tex).
- Build using the LaTeX Workshop command palette entries or GUI controls.

Optional tooling and credits:

- [LaTeX Utilities](https://marketplace.visualstudio.com/items?itemName=tecosaur.latex-utilities) for extra LaTeX editing helpers.
- Live Preview is provided by [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) via its PDF viewer.
- Word count can be done with [TeXcount](https://app.uio.no/ifi/texcount/) (`texcount gavinsdavies.tex`) after installing `texlive-extra-utils`.

### VS Code Commands

Open the Command Palette and run:

1. `LaTeX Workshop: Build LaTeX project`  
   Builds [gavinsdavies.tex](gavinsdavies.tex) using the workspace default recipe (`latexmk (lualatex)`).
2. `LaTeX Workshop: View LaTeX PDF file`  
   Opens the generated PDF in the LaTeX Workshop viewer (live preview).
3. `LaTeX Workshop: Clean up auxiliary files`  
   Removes build artifacts like `.aux`, `.fls`, `.fdb_latexmk`, and `.log`.
4. `LaTeX Workshop: Recipe: latexmk (lualatex)`  
   Manually selects the LuaLaTeX recipe.

You can also use the LaTeX Workshop GUI buttons/status items in VS Code (build, view PDF, clean, recipe select) instead of the Command Palette.

If builds fail in VS Code, check both:

- The `PROBLEMS` panel for parsed diagnostics.
- The LaTeX Workshop output channel for full compiler logs.

### Required tools

- `latexmk`
- `lualatex` (via TeX Live LuaLaTeX packages)
- `texcount` (optional, for word count)

On Debian/Ubuntu:

```bash
sudo apt install texlive-luatex lmodern texlive-fonts-recommended texlive-latex-extra texlive-extra-utils
```

### Build command

```bash
latexmk -lualatex -interaction=nonstopmode -halt-on-error gavinsdavies.tex
```

### Common issues

- `texcount: command not found`:
  install `texlive-extra-utils`.
- `fontspec requires XeTeX or LuaTeX`:
  build is running with pdfLaTeX; switch to LuaLaTeX.
- `module 'luaotfload-main' not found`:
  LuaLaTeX components are incomplete; install `texlive-luatex`.

If you still see LuaLaTeX/font loader errors after installing packages, this recovery sequence fixed the issue in this repo:

```bash
sudo apt install texlive-luatex lmodern texlive-fonts-recommended texlive-latex-extra
sudo mktexlsr
latexmk -C && latexmk -g -lualatex -interaction=nonstopmode -halt-on-error gavinsdavies.tex
```
