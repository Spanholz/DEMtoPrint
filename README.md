# Saxon DEM1 to STL Conversion Guide

A comprehensive guide for transforming DEM1 elevation data of the German state of Saxony into printable STL files for 3D printing terrain models.

![PXL_20241221_104502458](https://github.com/user-attachments/assets/958d5659-76ae-4b37-a0e2-ada13c6ed46a)



## Overview
The process involves a python script and QGIS. First converting the downloaded XYZ elevation data to GeoTIFF format using Python, then using QGIS with a specialized plugin to generate STL files.

## Prerequisites

### Software Requirements - all open-source
- **Python 3.x** with Jupyter Notebook
- **QGIS** (free, open-source GIS software)
- **DEM to 3D printing** plugin for QGIS

## Step 1: Download Saxon DEM1 Data

1. Visit the Saxon geodata download portal: https://www.geodaten.sachsen.de/downloadbereich-digitale-hoehenmodelle-4851.html
2. Select your desired area for download
3. Download the DGM1 files (Digital Elevation Model with 1-meter resolution)
4. Extract the ZIP file into a project folder
5. The extracted files will be in XYZ format

## Step 2: Data Conversion Using Python Script

### Setting Up the Jupyter Notebook

Download the Jupyter notebook and

#### Configure Project Folder

This is the folder where the extracted data lies. The script will look into the individual subfolders for the .xyz-files. An example can be seen below.
![Folder Structure](https://github.com/user-attachments/assets/4e6ad3ed-8c4e-4ec9-994f-233a2e38dfd9)

### Start the script by executing the cell

In the end a single will be there `merged_dem.tif`




### Performance Notes
- Processing time depends on area size and hardware
- Example: 16km² takes approximately 45 seconds on a Ryzen 3600 with 16GB RAM
- The script creates temporary files during processing and cleans them up automatically


## Step 3: QGIS Setup and STL Generation

### Install the DEM to 3D Printing Plugin
1. Open QGIS
2. Go to **Plugins > Manage and Install Plugins**
3. Search for "DEM to 3D printing"
4. Install the plugin


### Load Your Data
1. Start QGIS
2. Drop the the generated `merged_transformed.tif` file into QGIS
3. The elevation data should display as a raster layer

### Configure STL Export Settings

Use the following configuration in the DEM to 3D printing plugin:
![DEM Screen Cap](https://github.com/user-attachments/assets/dfbe0f03-855e-4134-b5bd-4f5204b91a7a)


#### 1. Area Selection
- **Use the full area of the GeoTIFF**: Set the boundaries to cover your entire elevation model
- This ensures you capture all the elevation data you processed

#### 2. Print Dimensions
- **Width and Length**: Set the physical dimensions of your final print
- **Important**: If you plan to print in multiple parts (e.g., 2x2 grid), these dimensions represent the **full assembled model size**, not individual print bed size

#### 3. Model Division
- **Divide your model**: Split into 2x2 individual STL<
 files (or adjust based on your printer's bed size)
- This creates separate STL files for each section that can be printed individually and assembled later

#### 4. Base Height Settings
- **Set height lower than lowest point**: This creates a solid base for stable printing
- The base ensures your terrain model sits flat on the print bed
- Recommended: Set base thickness to 2-4mm below the lowest elevation point

### Export Process
1. Configure all settings as described above
2. Choose your output directory for STL files
3. Click **Generate STL files**
4. The plugin will create individual STL files for each section of your divided model

## Step 4: Preparing for 3D Printing

### 3D Printing Tips
1. **Scaling**: Verify the scale matches your intended physical dimensions
2. **Layer Height**: Use 0.2 layer height for good detail vs. speed balance
3. **Support**: Terrain models typically require minimal to no support due to gradual slopes
4. **Infill**: 5-15% infill is usually sufficient for terrain models
5. **Orientation** Either print flat to get a distinctive layer look or sideways for smoother walls but beware of overhangs.
