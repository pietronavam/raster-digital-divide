# Raster Digital Divide — Territorial Digital Divide Analysis (Cusco, Peru)

## Project Description

This project measures the **territorial digital divide** in the Cusco region, Peru, by cross-referencing two satellite-derived raster datasets:

- **NASA Black Marble VNL 2025** — nighttime lights as a proxy for urbanization
- **OSIPTEL Mobile Coverage Kernel Density 2019** — mobile network coverage as a proxy for internet access

**Research question:** Where are the zones in Cusco with significant urbanization but insufficient internet connectivity, and what is the spatial distribution of digitally excluded populations?

## Repository Structure

```
raster-digital-divide/
├── data/                              # Input rasters (NOT committed — add to .gitignore)
│   ├── VNL_cusco_2025.tif
│   └── kernel_cobmovil2019_50m.tif
├── notebooks/
│   └── digital_divide_cusco.ipynb    # Main analysis notebook (10 steps)
├── output/                            # Generated rasters and figures
│   ├── vnl_norm.tif
│   ├── conn_norm.tif
│   ├── ibd_brecha_digital.tif
│   ├── clasificacion_brecha.tif
│   └── dashboard_brecha_digital.png
├── README.md
└── requirements.txt
```

## Dependencies

```bash
pip install -r requirements.txt
```

Required packages: `rasterio`, `numpy`, `matplotlib`, `scipy`, `seaborn`, `pandas`

## Data Download

Download the raster files from Google Drive and place them in `data/`:

- **Drive folder:** https://drive.google.com/drive/folders/16oP-IEX8EWklvuigtt-cTWJfDdD4E0ec
- `VNL_cusco_2025.tif` — NASA nighttime lights (EPSG:4326)
- `kernel_cobmovil2019_50m.tif` — Mobile coverage density (EPSG:32719)

## How to Run

1. Clone the repo and install dependencies
2. Download the raster files to `data/`
3. Open `notebooks/digital_divide_cusco.ipynb` in Jupyter
4. Run all cells top to bottom (Kernel → Restart & Run All)

All outputs are saved automatically to `output/`.

## Output Files

| File | Description |
|------|-------------|
| `vnl_norm.tif` | Nighttime lights normalized to [0, 1] via 2nd–98th percentile |
| `conn_norm.tif` | Connectivity normalized to [0, 1] via 2nd–98th percentile |
| `ibd_brecha_digital.tif` | Digital Divide Index (VNL_norm − Connectivity_norm), range [−1, 1] |
| `clasificacion_brecha.tif` | 4-class territorial classification raster |
| `dashboard_brecha_digital.png` | Composite dashboard with all 5 thematic maps |

## Main Findings

The analysis reveals a clear spatial pattern of digital inequality in Cusco: urban centers display moderate-to-high nighttime light intensity but often insufficient mobile connectivity (positive IBD values), indicating an active digital divide even in relatively urbanized areas. Rural highlands exhibit the highest digital exclusion risk (EDT near 1.0), with populations that lack both electricity infrastructure and internet access. Welch's t-test confirms a statistically significant difference in nighttime light intensity between Urban Connected (Class 1) and Critical Divide (Class 4) zones.
