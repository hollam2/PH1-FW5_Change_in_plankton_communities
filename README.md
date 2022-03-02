# PH1-FW5_Change_in_plankton_communities
This repository contains the code to run the PH1/FW5 lifeforms indicator which aggregates plankton abundance datasets to lifeform level and produces several metrics to detect 
change in plankton communities over time.

The repository contains all the data files and scripts to convert the raw plankton abundance data into a set of lifeform time-series, run the PH1 indicator
(Kendall statistic, lifeform pairs indicator and links to drivers), and generate outputs as figures.

Some of the larger data files have been encoded as .fst files for better file compression than .csv. 
These files are openable with the "read_fst()" function from the "fst" R-package. These files can be re-encoded as .csv if desired. 

The R-scripts are designed to be run in sequence from 1-6. Open the R project file entitled "R.proj" and run the scripts in order. 
Each script generates outputs which are required by subsequent scripts.

The purpose of each script is described below:

1-RAW_CPR_loader:
  -This tool reads raw CPR data and prepares it to be in the same format as the other plankton datasets.
  
2-RAW_plankton_loader:
  -This tool reads raw plankton data from national datasets which has already been aggregated into a single dataframe. 
  -This data is combined with the CPR data from the previous step and lifeforms are identified from a Master Taxa List before saving the output.
  
3-PROCESSED_spatial:
  -This tool reads processed aggregated and disaggregated plankton lifeform abundance data before interpolating over the polygons of a shapefile. 
  -It then calculates mean values for spatial polygons of a shapefile per lifeform, year and month and uses the interpolated data to fill gaps in the time-series. 
  -It then saves the output data to disk.
  
4-PH1_indicator:
  -This tool reads processed plankton abundance data that has been converted into a time-series with gaps filled by extracting by shapefile polygons 
  from the IDW interpolated rasters and performs the pelagic indicator assessment, outputting a set of figures to an "Output" folder.
  
5-Environmental_drivers:
  -This script is for analysing plankton lifeform abundance data alongside processed nutrient and SST data.
  -Boruta wrapper around random forest is used to determine the ability of environmental drivers to predict variation in lifeform abundance. 
  
6-Integration:
  -This script is for loading the results of the modelling environmental drivers and integrating with Kendall statistic for the plankton lifeform abundance time-series.
  

Any questions about this code can be directed to: matt.holland@plymouth.ac.uk


