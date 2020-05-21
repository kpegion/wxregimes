# Cluster Analysis Python Codes 

These are a collection of Jupyter Notebooks that reproduce the cluster maps for 4 (Figure 1) and 5 (Figure 2) clusters from [Amini and Straus 2019](https://link.springer.com/article/10.1007/s00382-018-4409-7)

Presteps:  

1. Clone the repository from Github
`git clone xxx`

2. Setup your Python environment using the provided environment.yml file.  
This will make sure that you have all the necessary packages installed.
`conda env create -f environment.yml`
`conda activate wxregimes`

3. Make a netcdf file with the 128x64 Gaussian grid from one of David's binary files. This will be used as the grid to interpolate all the data to
`makefilefor126x64grid.ipynb` 
Make a netcdf file with the 128x64 Gaussian grid from one of David's binary files. This will be used as the grid to interpolate all the data to
* Input: `/shared/metis/tco199/T42/gm8w/grid/1986110100/01/gm8w_1986110100_01_N32.data`
* Output: `tempgaussian.128x64.nc`

1. `subsetdata_1.ipynb`
Reads the ERA-interim Z500 and U250 daily data for Dec-Jan-Feb-Mar, extracts PNA region, re-grids to 128x64 Gaussian grid
* Input: `/shared/working/rean/era-interim/daily/data/yyyy/ei.oper.an.pl.regn128cm.yyyymmddhh`
* Output: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_DJF.1980-2015.nc`
This program processes A LOT of data.  It takes several hours to run.  However, once this program has run and the data are subsetted, the rest of the programs run quickly and easily.  I suggest running it on `atlas1` or `atlas2`. 

2. `runningmeans_2.ipynb`
Calculates the 5-day running means, extracts out only the 88 days of DJF running means for each year
* Input: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_DJF.1980-2015.nc`
* Output: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980-2015.nc`

3. `calcanoms_3.ipynb`
Calculates the anomalies by removing the average parabola fit to each year's data
* Input: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980-2015.nc`
* Output: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980-2015.anoms.nc`

4. `calcPCs_4.ipynb`
Calculates the EOFs and PC timeseries for 12 EOFs/PCs. PCs are written out to file.
* Input: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980 2015.anoms.nc`
* Output: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980 2015.pcs.nc`

5. `calc_clusters_5.ipynb`
Calculates and plots the composite cluster maps.

* Input: `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980-2015.pcs.nc` and `/project/predictability/kpegion/wxregimes/era-interim/erai.z500_u250_pna_5dyrm_DJF.1980-2015.anoms.nc`

* Output: `ERAI_clusters_5_1980-2015_DJF.png`, `ERAI_clusters_4_1980-2015_DJF.png`, `ERAI_clusters_6_1980-2015_DJF.png`

`ERAI_clusters_5_1980-2015_DJF.png` matches Amini and Straus, Figure 2
`ERAI_clusters_4_1980-2015_DJF.png` matches Amini and Straus, Figure 1
