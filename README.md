# pycurrents_ADCP_processing

For processing raw ADCP data in Python using the UHDAS `pycurrents` package (https://currents.soest.hawaii.edu/docs/adcp_doc/codas_setup/index.html).

*ADCP_pycurrents_L1.py* is based off of Jody Klymak's script (https://gist.github.com/jklymak/b39172bd0f7d008c81e32bf0a72e2f09). This version contains changes to variable names (following BODC conventions); addition of variables, variable and global attributes, and dimensions to match the netCDF ADCP files produced before using R; and minimal ("L1") processing.  

"L1" stands for "level 1 processing". This comprises:
* Corrections for magnetic declination
* Calculation of sea surface height from pressure values and latitude
* Flagging leading and trailing ensembles from before and after deployment and setting them to nan's
* Rotation into enu coordinates if this is not already the coordinate system of the dataset.

## Installation
To download *ADCP_pycurrents_L1.py* and *add_var2nc.py* from this repository without having to clone the whole repository:
1. Open a file in a GitHub repository and click on the button "raw" in the top right corner to view the raw file in a new browser tab. Copy the url of the raw file (e.g. ht<span>tps://</span>raw.githubusercontent.com/username/reponame/path/to/file).
2. To save this file to your computer, open a terminal window and enter
    
        wget https://raw.githubusercontent.com/username/reponame/path/to/file --no-check-certificate
   
   "--no-check-certificate" allows the user to connect to GitHub insecurely and download a file successfully.<br/>

### *ADCP_pycurrents_L1.py* dependencies
The following instructions are for installing packages used in the *ADCP_pycurrents_L1.py* script.
  
#### `pycurrents`
To install the Python package `pycurrents`, follow the instructions at https://currents.soest.hawaii.edu/ocn_data_analysis/installation.html.
  
#### `gsw`
To install the TEOS-10 `gsw` package: 
1. Download a .zip file of the repository at https://github.com/TEOS-10/GSW-Python and extract its contents to a folder called "GSW-Python-master"
2. In a terminal window, activate the virtual environment (e.g., "py37") created during the installation of `pycurrents` with the command `conda activate py37`. cd to the "GSW-Python-master/" folder.
3. Enter the command: `pip install .` to build `gsw`.
  
#### `num2words`
To install the `num2words` package:
1. Open a terminal window and activate the virtual environment (e.g., "py37") created during the installation of `pycurrents` with the command `conda activate py37`.
2. Install the package with the command: `pip install num2words`

### *add_var2nc.py* dependencies
`ios_data_transform` package: Please follow the instructions for installation at https://github.com/onedwd/cioos-siooc_data_transform.

### Pre-requisites
* Linux (or Unix-like) environment

## Usage
*ADCP_pycurrents_L1.py* uses the `pycurrents` package to open a raw ADCP file in Python and export it in netCDF file format. The script also uses a .csv metadata file for the raw ADCP file whose contents are combined with the raw data in the netCDF file, so that the netCDF file is self-describing. This metadata file is filled out by the user and a template can be found at https://github.com/hhourston/ADCP_processing_visualization/tree/master/ADCP_metadata_template. 

A description of output data format can be found in the RDI Ocean Surveyor technical manual at http://www.teledynemarine.com/Documents/Brand%20Support/RD%20INSTRUMENTS/Technical%20Resources/Manuals%20and%20Guides/Ocean%20Surveyor_Observer/Ocean%20Surveyor%20Technical%20Manual_Apr18.pdf, starting on page 148.

## Credits
*ADCP_pycurrents_L1.py* is based off of the gist, *RdiToNetcdf.ipynb*, by Jody Klymak (https://github.com/jklymak), and includes contributions from Di Wan (https://github.com/onedwd) and Eric Firing (https://github.com/efiring). *add_var2nc.py* was written by Di Wan. 
