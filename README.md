# Structural Biology Explorer

**Live site:** https://klausenhauser.github.io/structbio-explorer/

Interactive, in-browser teaching pages for the three main methods used to determine
macromolecular structures: **X-ray crystallography**, **cryo-electron microscopy** and
**NMR spectroscopy**. Each page is a single self-contained HTML file that runs entirely in
the browser (no server, no install). 3D views use [three.js](https://threejs.org) r128,
loaded from a CDN.

> Made with [Claude](https://claude.ai) (Anthropic). The pages were designed and coded with
> Claude, then reviewed, curated and published by Kelvin Lau.

## Pages and data sources

Each page says on screen which parts are **real experimental data** and which are **simulated**.

### X-ray crystallography: *Diffraction at PXI* (`xray/`)

| | |
|---|---|
| What it shows | An undulator beamline opened up from source to detector; real diffraction frames tied to their points in reciprocal space (Ewald sphere). |
| **Real data** | Raw EIGER 16M diffraction images from the dataset deposited with **PDB [9QBT](https://www.rcsb.org/structure/9QBT)** (KEAP1), collected at SLS X06SA (PXI), 8 Feb 2023. Raw data: [doi:10.18430/M39QBT](https://doi.org/10.18430/M39QBT) (proteindiffraction.org). Frames 1–200 (0–20°, 0.1° each) as images; frames 201–1800 summed into 1° wedges. Geometry, indexing and spot predictions from the deposited XDS files (GXPARM.XDS, INTEGRATE.HKL, CORRECT.LP). |
| Simulated | The 3D beamline and goniometer model, and the reciprocal-lattice/Ewald-sphere rendering (computed from the deposited XDS geometry). |
| Files | `frames/` (0.1° frames), `wedges/` (1° sums), `zoom/` (zoomed crops), `refl.txt`, `recip.txt`, `xds.json` (processed reflections and geometry). |

### Cryo-EM: *Frozen in the Beam* (`cryoem/`)

| | |
|---|---|
| What it shows | A transmission electron microscope opened up; move the stage across a grid (atlas → square → hole → exposure), change defocus and dose, and see particles emerge from the noise. |
| Real data | Particle coordinates from **PDB [5A1A](https://www.rcsb.org/structure/5A1A)**, *E. coli* β-galactosidase (UniProt [P00722](https://www.uniprot.org/uniprotkb/P00722)), Bartesaghi et al., *Science* 2015, reduced to Cα beads. |
| **Simulated** | **All images are simulated** in the browser: grid atlas, squares, holes, ice thickness, micrographs, CTF (300 kV, Cs 2.7 mm, B = 60 Å²), power spectrum and shot noise. No raw micrographs are used. |

### NMR: *Ubiquitin at 800 MHz* (`nmr/`)

| | |
|---|---|
| What it shows | A triple-resonance pulse sequence driving the spin system, the resulting spectra (HSQC, strips, slices) and a backbone sequence walk. |
| Real data | Assigned chemical shifts from **BMRB [6457](https://bmrb.io/data_library/summary/index.php?bmrbId=6457)** (Cornilescu, Marquardt, Ottiger & Bax, *J. Am. Chem. Soc.* 1998, 120, 6836), human ubiquitin (UniProt [P0CG48](https://www.uniprot.org/uniprotkb/P0CG48)), pH 6.6, 292 K. Structure and φ angles from **PDB [1UBQ](https://www.rcsb.org/structure/1UBQ)**. |
| **Simulated** | **All spectra are simulated** from those shifts (product-operator formalism; TOCSY by full spin-system calculation) at 18.8 T. No raw FIDs are used. |

## Repository layout

```
index.html        landing page (X-ray, Cryo-EM, NMR sections)
xray/             Diffraction at PXI  + its image and data files
cryoem/           Frozen in the Beam  (self-contained)
nmr/              Ubiquitin at 800 MHz (self-contained)
LICENSE           MIT
.nojekyll         serve files as-is on GitHub Pages
```

## Run locally

Any static file server works, for example:

```bash
python3 -m http.server 8000
```

then open http://localhost:8000. (The X-ray page loads its frames with `fetch`, so opening
the file directly from disk will not work.)

## Adding a page

Put the page in the matching folder (as `index.html` plus any data files), then add a card
to the section in the top-level `index.html`.

## Licence

Code and page content: **MIT License, Copyright (c) 2026 Kelvin Lau.** See [LICENSE](LICENSE).

Third-party data (PDB, BMRB and proteindiffraction.org entries listed above) are not covered
by the MIT licence and remain under the terms of their providers; please cite the original
depositions.
