# Mine Excavation Monitoring and No-Go Zone Violation Detection

## Overview
This project implements a satellite-based system for monitoring excavation activity in mining regions using Sentinel-2 imagery and Google Earth Engine. The system detects excavation, analyzes its temporal evolution, and identifies violations occurring within restricted (no-go) zones. The approach is data-adaptive and avoids fixed thresholds, enabling robust performance across different mines and terrain conditions.

---

## Objectives
- Detect excavation activity using multispectral satellite imagery  
- Track excavation growth over time  
- Quantify excavation within legal mine boundaries  
- Detect and report excavation inside no-go zones  
- Provide clear spatial and temporal visualizations  
- Support scalable analysis across multiple mines  

---

## Data Used
- Satellite imagery: Sentinel-2 Surface Reflectance (COPERNICUS/S2_SR)  
- Vector data:
  - Mine boundary polygons  
  - Synthetic no-go zones representing residential areas, commercial areas, forest buffers, water bodies, and other sensitive regions  

---

## Methodology

### Image Preprocessing
- Cloud and shadow masking using Sentinel-2 Scene Classification Layer (SCL)  
- Temporal filtering of imagery from 2019 to 2024  

### Spectral Indices
- Normalized Difference Vegetation Index (NDVI) for vegetation detection  
- Bare Soil Index (BSI) for exposed soil and excavation detection  

### Excavation Detection
Excavation is detected using an adaptive local-baseline approach:
- An excavation score is computed as the difference between BSI and NDVI  
- A local median filter is applied as a baseline  
- Positive deviations from this baseline are classified as excavation  

This method adapts to local surface conditions and avoids the need for manually defined thresholds.

---

## No-Go Zone Analysis
Synthetic no-go zones are generated for each mine to simulate restricted regions such as settlements, water bodies, forest buffers, and environmentally sensitive areas. Detected excavation masks are spatially intersected with these zones to quantify violations and monitor their progression over time.

---

## Outputs

### Temporal Analysis
- Time-series of excavated area within mine boundaries  
- Time-series of excavated area within no-go zones  

### Spatial Visualization
- Excavation detection maps for individual timestamps  
- Overlays with mine boundaries and no-go zones  
- Interactive maps for visual inspection and validation  

### Alerts
- Identification of the first date of no-go zone violation  
- Detection of incremental excavation growth events within restricted areas  

---

## User Interface
Results are visualized using interactive maps and time-series plots. The workflow is designed to be easily extended into a web-based dashboard (e.g., Streamlit) that allows users to select a mine and explore the corresponding outputs.

---

## Installation and Setup

### Requirements
- Python 3.8 or later  
- Google Earth Engine account with API access  

### Install Dependencies
```bash
pip install earthengine-api geopandas pandas matplotlib folium
```

### Authenticate and Initialize Earth Engine
```bash
earthengine authenticate
```

```python
import ee
ee.Initialize(project='your-gcp-project-id')
```

---

## Usage
1. Load mine boundary data as a FeatureCollection  
2. Generate synthetic no-go zones for each mine  
3. Run the excavation detection pipeline  
4. Generate time-series plots, spatial maps, and alert logs  

---

## Expected Results
- Clear temporal trends of excavation activity  
- Early identification of illegal excavation in restricted areas  
- Comparable excavation metrics across different mines  
- Actionable insights for regulatory monitoring and compliance  

---

## Future Work
- Confidence and uncertainty estimation for detected excavation  
- Near real-time monitoring and alerting  
- Integration with SAR data (Sentinel-1)  
- Full web-based dashboard deployment  
- Automated report generation  

---

## Author
Sowmya  
Engineering Physics  
Geospatial AI and Remote Sensing  

---

## License
This project is intended for academic and research purposes. License terms can be updated as required.
