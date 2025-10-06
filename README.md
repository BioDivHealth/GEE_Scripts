# Google Earth Engine Export Scripts

This repository contains a collection of Google Earth Engine (GEE) scripts to export spatial data for a region of interest, including:

- NDVI (Normalized Difference Vegetation Index)
- ESA WorldCover
- Elevation (SRTM)
- Dynamic World
- Dynamic Land

Each script follows a consistent structure for defining a region of interest (ROI), selecting a date range, processing data, and exporting results to Google Drive as GeoTIFF files.

### Instructions
1. Open in Google Earth Engine

You can open and run these scripts directly in the Google Earth Engine Code Editor:
👉 https://code.earthengine.google.com/

Upload or copy each .js file into your “Scripts” panel.

2. Define Your Region of Interest (ROI)

Each script begins with two options for defining the region of interest:

**Option A: Draw on the Map**

Use the “Geometry Tools” (polygon, rectangle, or point icons) in the GEE interface to draw your area of interest.
The variable geometry will automatically reference your drawn shape.

**Option B: Specify Coordinates**

Uncomment and edit the following lines in the script to set bounding box coordinates:

var minLat = 37.7749;
var minLon = -122.4194;
var maxLat = 37.8049;
var maxLon = -122.3894;
var geometry = ee.Geometry.Rectangle([minLon, minLat, maxLon, maxLat]);

3. Set the Date Range

Modify the following variables in each script as needed:

var startDate = '2024-01-01';
var endDate = '2025-01-01';

4. Run the Script

Click “Run” in the GEE Code Editor.

The processed image (e.g., NDVI, WorldCover, Elevation) will display on the map.

Review and adjust visualization parameters if needed.

5. Export Results

Each script includes an export block similar to:

Export.image.toDrive({
  image: ndviClipped,
  description: 'NDVI_Export',
  scale: 30,
  region: geometry,
  fileFormat: 'GeoTIFF',
  maxPixels: 1e9
});


After running the script:

Go to “Tasks” (upper right in GEE).

Click “Run” next to your export task.

The GeoTIFF will be saved to your Google Drive.

### Script Overview

| Script | Dataset | Description | Typical Resolution | Export Band(s) |
|--------|----------|--------------|--------------------|----------------|
| `NDVI` | **Landsat 8 TOA** (`LANDSAT/LC08/C02/T1_TOA`) | Computes NDVI (Normalized Difference Vegetation Index) to assess vegetation greenness. | 30 m | `NDVI` |
| `WorldCover` | **ESA WorldCover 2021** (`ESA/WorldCover/v200`) | Exports categorical land cover classification (11 global classes). | 10 m | `Map` |
| `Elevation` | **SRTM** (`USGS/SRTMGL1_003`) | Exports surface elevation above sea level. | 30 m | `elevation` |
| `DynamicWorld` | **Google Dynamic World** (`GOOGLE/DYNAMICWORLD/V1`) | Exports land cover probability maps derived from Sentinel-2 imagery. | 10 m | `class`, `probability` |
| `DynamicLand` | **Dynamic Land** (`projects/sat-io/open-datasets/DynamicLand`) | Exports land cover time-series data for monitoring changes. | 30 m | `landcover` |


### Customization Tips

- Adjust the scale parameter to control output resolution.
- Modify date ranges to analyze seasonal or annual trends.
- Clip to administrative boundaries or shapefiles using geometry = ee.FeatureCollection('FAO/GAUL/2015/...').

### Dependencies


- A **Google Earth Engine account** – [Sign up here](https://signup.earthengine.google.com/)
- Internet browser with JavaScript enabled
- Enough **Google Drive storage** for exported GeoTIFFs
