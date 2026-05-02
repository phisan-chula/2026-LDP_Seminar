The **ReadMe.md**[cite: 3] file is provided below. You can copy this content directly into a new text file named `ReadMe.md` in your project's root directory.

# Constr_LDP: Design of Low Distortion Projections[cite: 3]

**Constr_LDP** is a Python-based utility developed for engineers and surveyors to design **Low Distortion Projections (LDPs)**[cite: 3]. It minimizes the linear distortion between projected grid coordinates and actual horizontal distances at the surface of an engineering project by optimizing the projection plane and scale factor ($k_0$)[cite: 3].

## Key Features[cite: 3]
* **Automated $k_0$ Calculation**: Determines the optimal scale factor based on the project's mean elevation and latitude[cite: 3].
* **Support for Multiple Projections**: Supports Transverse Mercator (TM) and Lambert Conformal Conic (LCC)[cite: 3].
* **Geoid Awareness**: Utilizes the Karney Geoid model (TGM2017) for accurate ellipsoidal height transitions[cite: 3].
* **Flexible Input**: Supports test points from GeoPackage (GPKG), Excel (XLSX), or synthetic buffers around a center point[cite: 3].
* **GIS Ready**: Exports LDP definitions as WKT strings and GeoPackage layers for seamless integration with GIS software and total stations[cite: 3].

## Technical Methodology[cite: 3]
The application follows a rigorous surveying workflow[cite: 3]:
1. **Centroid Analysis**: Calculates the mean Latitude and MSL of the project site[cite: 3].
2. **Elevation Scaling**: Converts MSL to Ellipsoidal Height ($h = H + N$) using the Geoid model[cite: 3].
3. **Curvature Adjustment**: Computes $k_0$ using the Gaussian Radius of Curvature ($R_G$)[cite: 3]:
   $$k_0 = 1 + \frac{h_{PP}}{R_G}$$[cite: 3]
4. **Distortion Verification**: Validates the Combined Scale Factor (CSF) across the site to ensure minimal ppm (parts per million) error[cite: 3].

## Installation[cite: 3]
Ensure you have Python 3.11+ installed[cite: 3]. Install the required dependencies via pip[cite: 3]:

```bash
pip install numpy pandas geopandas pyproj pygeodesy matplotlib shapely
```

*Note: Ensure the `tgm2017-1.pgm` geoid file is present in the application directory or system Geoid path[cite: 3].*

## Usage[cite: 3]
Run the application by providing a TOML configuration file[cite: 3]:

```bash
python constr_LDP.py MyLDP.toml [options]
```

### Command Line Arguments[cite: 3]
* `LDP_TOML`: Path to the configuration file (Required)[cite: 3].
* `-c`, `--csf`: Display a detailed Combined Scale Factor (CSF) distribution table[cite: 3].
* `-u`, `--utm`: Display a comparison between standard UTM and LDP coordinates[cite: 3].
* `-o OFFSET_PP`: Override the project plane offset in meters[cite: 3].

## Configuration (TOML)[cite: 3]
Example `MyLDP.toml`[cite: 3]:
```toml
PROJECT = "Udon Thani Construction"
LDP = ["TM", "102:54"]
FALSE_EN = "AUTO"

[TEST_POINT]
POS_LATLNG = [17.2677, 102.9139]
MSL = 125
BUFFER = [5000, 50]
```

## License[cite: 3]
© 2022-2026 Phisan Santitamonont, Faculty of Engineering, Chulalongkorn University[cite: 3].
