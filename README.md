# 🧊 Pallet Atlas

**Explore pallet measurements, simulation uncertainty, and box-level threshold exceedance in an interactive 3D view.**

🌐 Offline web app · 📦 20 boxes · 🧱 Four layers · 🎲 Monte Carlo analysis · 🐍 Reproducible Python workflows

## 🎯 Project brief

Pallet Atlas turns state-space observations and saved Monte Carlo simulations into an interactive, traceable view of a pallet. Explore how measurements vary by box, layer, and time, then inspect the source records behind each result.

The project combines Excel data cleaning, statistical summaries, simulation comparisons, spatial visualization, and source alignment checks. Deliverables include the offline application, source workbooks, analysis scripts, CSV results, charts, and a browser presentation.

## 🖼️ Preview

![Pallet Atlas](pallet%20webpage/preview.png)

## ✨ Features

| Feature | What it provides |
| --- | --- |
| **Interactive pallet** | Rotate through 360 degrees, zoom, separate layers, and select any box. |
| **Box reports** | Compare observed means, simulated values, percentile intervals, and threshold exceedance across time. |
| **Data & alignment** | Inspect individual trials, saved simulations, chart inputs, and top-down layouts. |
| **Source downloads** | Bundled workbook and CSV snapshots with SHA-256 fingerprints. |
| **Reproducible analysis** | Python cleaning, box/layer summaries, comparison charts, and audited data export. |
| **Offline operation** | Bundled data, canvas rendering, and no external JavaScript, font, or network dependencies. |

## 🚀 Quick start

1. Clone or download this repository.
2. Open `pallet webpage/index.html` in a modern browser.
3. Drag to rotate, scroll to zoom, and click a box to inspect its report.
4. Change the selected hour or separate layers to explore the full pallet.
5. Open **Data & alignment** to review the source records behind a result.

No installation or server is required to explore the saved results. GitHub displays HTML source; open the downloaded files locally to use the application.

```bash
git clone https://github.com/aasrith12/Pallet-Atlas-.git
cd Pallet-Atlas-
```

Read the [Atlas usage and data guide](pallet%20webpage/README.md), or open [the presentation](Pallet_Temperature_Risk_Presentation.html) locally in your browser.

## 🗂️ Repository map

| Location | Contents |
| --- | --- |
| `pallet webpage/index.html` | Main interactive pallet view. |
| `pallet webpage/analysis-data.html` | Source records, alignment checks, geometry review, and downloads. |
| `pallet webpage/app.js`, `styles.css` | Canvas projection, selection, and interface styling. |
| `pallet webpage/data.js` | Bundled offline data snapshot. |
| `pallet webpage/build_data.py`, `audit_data.py` | Data export and source verification. |
| `pallet webpage/sources/` | Downloadable source snapshots. |
| `pallet webpage/verify.cjs` | Optional browser interaction checks. |
| `New folder/` | Original pallet workbooks, cleaning and analysis scripts, CSVs, charts, and summaries. |
| `Pallet_Temperature_Risk_Presentation.html` | Browser presentation of the pallet analysis. |

Keep the existing folder names: the data builder reads the sibling `New folder` directory.

## 📊 Dataset coverage

- **20 boxes** distributed across **four layers**.
- **1,170 observed readings**, summarized into **260 box-hour records**.
- Observations span **0–24 hours**, in two-hour increments.
- **50,000 saved simulation values**, with **500 simulations per box-hour** at hours **0, 6, 12, 18, and 24**.
- **100 simulation box-hour summaries**, including means, standard deviations, percentiles, and threshold percentages.

The alignment audit checks workbook readings, saved simulations, summary statistics, first observed crossings, and the coordinates used in the heat maps.

## 🔬 Reproduce the results

Use **Python 3.10+**. From the repository root, install the analysis dependencies:

```bash
python -m pip install pandas openpyxl matplotlib
```

Clean the workbooks and regenerate the analyses in this order:

```bash
python "New folder/clean_state_space_data.py"
python "New folder/clean_monte_carlo_data.py"
python "New folder/analyze_state_space_summaries.py"
python "New folder/analyze_monte_carlo_summaries.py"
python "New folder/analyze_state_space_vs_monte_carlo.py"
```

The scripts write CSV summaries, PNG charts, and explanatory text under:

- `New folder/state_space_summary_results/`
- `New folder/monte_carlo_summary_results/`
- `New folder/state_space_vs_monte_carlo_results/`

Refresh the application snapshot afterward:

```bash
python "pallet webpage/build_data.py"
```

The builder checks source alignment before writing `data.js` and copying source downloads. Reload the page after export. Refreshing existing results only requires `openpyxl`; it does not rerun the analysis scripts or generate new Monte Carlo simulations.

## ✅ Verification

The export audit recalculates observed and simulated summaries and checks them against source records before publishing a snapshot.

Optional browser interaction checks require Node.js, an installed `playwright-core` module, and its compatible Chromium browser:

```bash
node "pallet webpage/verify.cjs"
```

You may pass the absolute path to an installed `playwright-core` module as the first argument.

## 🧭 Interpretation & known limits

- **Threshold exceedance:** “risk” is the percentage of simulated values **≥ 4**, not a validated probability of spoilage.
- **Units:** the source measurement unit is unconfirmed. Values are displayed without a Celsius claim.
- **Uncertainty:** simulation percentile intervals describe simulated values, not confidence intervals for a mean.
- **Validation:** simulations centered on observed averages do not independently validate the observations or predictive accuracy.
- **Crossings:** the first observed crossing occurs when any available trial reaches the threshold, even if the box mean remains below it.
- **Geometry:** source centers are in inches; nominal box dimensions and the pallet structure are inferred for display. Layer 1 is highest and Layer 4 is lowest.
- **Exposure discrepancies:** L2B7 and L2B9 have recorded outer-side counts that differ from the nominal layout. These are retained and flagged. Bottom contact with the pallet is not confirmed air exposure.

## 🛠️ Technology & skills demonstrated

| Area | Tools and methods |
| --- | --- |
| Data processing | Python, pandas, openpyxl, Excel ingestion, and CSV export. |
| Analysis | Observed/simulated comparisons, percentiles, threshold crossings, and box/layer rankings. |
| Visualization | Matplotlib, HTML, CSS, JavaScript, and canvas-based 3D projection. |
| Traceability | Source alignment audits, downloadable snapshots, and SHA-256 fingerprints. |

## 🗺️ Next steps

- Confirm measurement units and the source exposure definitions.
- Validate the physical stacking plan and inferred dimensions.
- Extend analysis with additional observations and independently validated simulations.

## 🔗 Related project

Pallet Atlas was developed alongside the sensor analysis in [Internal and External Temperature Correlation](https://github.com/aasrith12/Internal-and-External-Temperature-Correlation).
