# DSC-054 step 4: Source finding and catalogue generation

This notebook is a first implementation of DSC-057, Continuum Source Finding: step 4 of https://confluence.skatelescope.org/display/SRCSC/DSC-057+Detailed+breakdown

Ticket: TEAL-1135 https://jira.skatelescope.org/browse/TEAL-1135

## Interactive Workflow
`pybdsf_lofar_sourcefind.ipynb` is the primary workspace for exploring PyBDSF on LOFAR-like FITS data. The notebook walks through FITS header inspection, optional cube collapsing, PyBDSF configuration, and review of the resulting catalogs and plots. Start there for iterative tuning and to document parameter choices.

## Requirements
- Python 3.9 or newer
- PyBDSF (`bdsf`), Astropy, NumPy, Matplotlib, Threadpoolctl
- A science FITS image or cube; a lightweight cutout (`test_cut.fits`) is bundled for smoke tests

## Quickstart
 Follow the cells in order, adjusting parameters such as island/pixel thresholds, RMS box sizes, or à trous wavelet controls as needed.

## Notebook Highlights
- Inspect FITS headers and WCS metadata with Astropy utilities.
- Collapse spectral cubes with mean/median/min/max reducers or select a single plane for analysis.
- Run PyBDSF with configurable background and detection thresholds, including multiscale fitting.
- Export GAUL/SRL catalogs, diagnostic FITS products, and an overlay PNG for visual validation.

## Outputs
- `*.pybdsf.srl.fits` — source catalog
- `*.pybdsf.gaul.fits` — Gaussian components
- `*.overlay.png` — detected sources overlaid on the image
- Additional RMS, model, and residual FITS products written under `pybdsf_out/`

Clean up temporary artifacts by removing or ignoring `pybdsf_out/` when sharing commits.

## Troubleshooting
- If importing PyBDSF fails, ensure the `bdsf` wheel compiled successfully (macOS users often install `cfitsio` via Homebrew first).
- Large cubes can exceed memory; reduce cores via the PyBDSF `ncores` setting and limit BLAS threads when necessary.
- Use Astropy’s `fitsheader` or the notebook’s inspection cells to confirm WCS alignment if source positions appear offset.
