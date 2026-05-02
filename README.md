Here is the clean version of your **ReadMe.md** without the citation tags, formatted for immediate use in your repository.

# Constr_LDP: Design of Low Distortion Projections

**Constr_LDP** is a Python-based utility developed for engineers and surveyors to design **Low Distortion Projections (LDPs)**. It minimizes the linear distortion between projected grid coordinates and actual horizontal distances at the surface of an engineering project by optimizing the projection plane and scale factor ($k_0$).

## Key Features
* **Automated $k_0$ Calculation**: Determines the optimal scale factor based on the project's mean elevation and latitude.
* **Support for Multiple Projections**: Supports Transverse Mercator (TM) and Lambert Conformal Conic (LCC).
* **Geoid Awareness**: Utilizes the Karney Geoid model (TGM2017) for accurate ellipsoidal height transitions.
* **Flexible Input**: Supports test points from GeoPackage (GPKG), Excel (XLSX), or synthetic buffers around a center point.
* **GIS Ready**: Exports LDP definitions as WKT strings and GeoPackage layers for seamless integration with GIS software and total stations.

## Technical Methodology
The application follows a rigorous surveying workflow:
1. **Centroid Analysis**: Calculates the mean Latitude and MSL of the project site.
2. **Elevation Scaling**: Converts MSL to Ellipsoidal Height ($h = H + N$) using the Geoid model.
3. **Curvature Adjustment**: Computes $k_0$ using the Gaussian Radius of Curvature ($R_G$):
   $$k_0 = 1 + \frac{h_{PP}}{R_G}$$
4. **Distortion Verification**: Validates the Combined Scale Factor (CSF) across the site to ensure minimal ppm (parts per million) error.

## Installation
Ensure you have Python 3.11+ installed. Install the required dependencies via pip:

```bash
pip install numpy pandas geopandas pyproj pygeodesy matplotlib shapely
```

*Note: Ensure the `tgm2017-1.pgm` geoid file is present in the application directory or system Geoid path.*

## Usage
Run the application by providing a TOML configuration file:

```bash
python constr_LDP.py MyLDP.toml [options]
```

### Command Line Arguments
* `LDP_TOML`: Path to the configuration file (Required).
* `-c`, `--csf`: Display a detailed Combined Scale Factor (CSF) distribution table.
* `-u`, `--utm`: Display a comparison between standard UTM and LDP coordinates.
* `-o OFFSET_PP`: Override the project plane offset in meters.

## Configuration (TOML)
Example `MyLDP.toml`:
```toml
PROJECT = "Udon Thani Construction"
LDP = ["TM", "102:54"]
FALSE_EN = "AUTO"

[TEST_POINT]
POS_LATLNG = [17.2677, 102.9139]
MSL = 125
BUFFER = [5000, 50]
```

## License
© 2022-2026 Phisan Santitamonont, Faculty of Engineering, Chulalongkorn University.
