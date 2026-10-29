[README.md](https://github.com/user-attachments/files/34117557/README.md)
# Food-system boundaries and production pathways: Burkina Faso as a test case

Data, code, and figures for the article:

> **Can a fast-growing, food-insecure country feed itself within its fair share of the food-system boundaries? A dynamic assessment to 2100.**
> Submitted to the *Journal of Cleaner Production* (Elsevier).

The repository reproduces every table, figure, and number in the article and its Supplementary Material from official
statistics (FAOSTAT, AQUASTAT, World Bank, UN World Population Prospects 2024, Global Carbon Budget, Global Yield Gap Atlas).
The framework uses only data that exist for every country, so the scripts can be adapted to other national food systems
by changing the FAOSTAT area code and the country-specific inputs in `data.py`.

## Files

| File | Content |
|:--|:--|
| `data.py` | Official input series, with FAOSTAT domain, item, and element codes (retrieved 20–21 Oct 2026) |
| `model.py` | Pressures, boundaries, sharing principles (EPC, AP, GF, RE), trajectories to 2100, decoupling test, NDC/IPCC climate pathways, Monte Carlo (N = 20,000, seed 20261020), and sensitivity analysis; writes `results.json` |
| `scen.py` | 30 production-pathway scenarios (5 diets × 2 trade regimes × 3 cereal-yield levels) for 2050 and 2100, with one-at-a-time tests of the agronomic assumptions; reads `results.json`, writes `scen.json` |
| `figures.py` | Figs. 1–5 and 7 and Supplementary Fig. S5 (PNG, TIFF, and vector PDF) |
| `fig_scen.py` | Fig. 6 (production-pathway scenarios; PNG, TIFF, and vector PDF) |
| `fig_s4_nitrogen.py` | Supplementary Fig. S4; needs `exc_nsur_crit_mi_all_ph.asc` from the te Wierik et al. (2025) supporting data ("Data for Figure 4"), `bfa_poly.json`, and the Natural Earth borders in `wa_10m.json` |
| `make_si.py` | Supplementary tables, including Section S8 (Tables S14–S16), as Markdown |
| `make_wb.py` | Calculation workbook with live formulas |
| `results.json`, `scen.json` | All model and scenario outputs |
| `Workbook.xlsx` | Calculation workbook (blue = official input, black = formula); sheets `Scenario_inputs`, `Scenarios`, and `Scenario_sensitivity` hold the production pathways |
| `N_local.json` | Summary of the critical nitrogen-surplus raster of te Wierik et al. (2025) for Burkina Faso |
| `conv.json` | Monte Carlo convergence check |
| `Fig1.pdf` … `Fig7.pdf`, `Fig1.tif` … `Fig7.tif` | Figures as submitted: vector PDF (fonts embedded) and 600-dpi TIFF |
| `FigS1_map.png`, `FigS3_lulc.png`, `FigS4_landcover.png`, `FigS4_N_local.png` | Supplementary maps |

Figure numbering follows the article: Fig. 1 framework; Fig. 2 status; Fig. 3 climate; Fig. 4 sharing principles;
Fig. 5 decoupling; Fig. 6 production-pathway scenarios; Fig. 7 robustness.

## How to reproduce

Python 3.11 or later.

```bash
pip install numpy matplotlib openpyxl pillow
mkdir fig
python model.py       # writes results.json (identical to the file provided)
python scen.py        # writes scen.json (identical to the file provided)
python figures.py     # writes fig/Fig1_framework … fig/Fig5_decoupling, fig/Fig7_uncertainty (PNG, TIFF, PDF)
python fig_scen.py    # writes fig/Fig6_scenarios (PNG, TIFF, PDF)
python make_si.py     # writes supplementary_material.md (copy the FigS*.png files into fig/ first)
python make_wb.py     # writes Workbook.xlsx
```

## Data sources

All inputs are public: FAOSTAT domains GT, RL, ESB, EMN, RP, QCL, TCL, FBS, FBSH, and FS (area codes: Burkina Faso 233,
World 5000); AQUASTAT; World Bank World Development Indicators; UN World Population Prospects 2024 (medium variant);
Global Carbon Budget 2023 cumulative emissions via Our World in Data; the Global Yield Gap Atlas (water-limited yield
potential); Burkina Faso NDC 3.0; IPCC AR6 WGIII; and the SOFITEX 2022/23 cotton input tender. Use of the original data is
subject to the terms of each provider.

## Citation

If you use this material, please cite the article (reference to be added on publication) and this repository.

## Licence

Code: MIT License. Derived data, workbook, and figures: CC BY 4.0, unless the terms of the original data provider require
otherwise.
