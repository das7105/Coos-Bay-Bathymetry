# Coos-Bay-Bathymetry
Coos Bay bathymetry product created from merging different datasets together. Please cite forthcoming papers on Coos Bay bathy depending on which file you use: either Emily Eidam et al. 2019 or Ted Conroy et al. 2019). The bathymetry is used in numerical simulations of the hydrodynamics of the estuary; hence it is on an unstructured mesh-type grid. 

Bathymetry data for Coos Estuary Oregon
Dave Sutherland, University of Oregon. (dsuth@uoregon.edu)

The sources of bathymetry data include:

1. NOAA/USACE topobathy LiDAR (https://coast.noaa.gov/htdata/lidar1_z/geoid12b/data/4905/)
Coordinate info: Horizontal - geographic (lat/lon) NAD83 Vertical - NAVD88 (meters)

2. USACE channel surveys (http://www.nwp.usace.army.mil/Missions/Navigation/Surveys/)
Coordinate info: Horizontal - Oregon South State Plane North American Data 1983 (survey feet) Vertical - MLLW (feet)

3. NOAA 1/3 arc second Port Orford DEM (https://data.noaa.gov//metaview/page?xml=NOAA/NESDIS/NGDC/MGG/DEM/iso/xml/410.xml&view=getDataView&header=none)
Coordinate info: Horizontal - geographic WGS1984 Vertical - MHW (meters)

4. Single Beam Sonar collected by P. Ruggiero and J. Woods (Oregon State University)
Coordinate info: Horizontal - Oregon State Plane South (meters) Vertical - NAVD88 (meters)

5. ODFW (SEACOR) Horizontal WGS84
Vertical - MLLW (meters)

Before merging, all data was converted to:
Horizontal - geographic NAD83 (very similar to WGS 1984)
Vertical - Mean Sea Level (MSL) (meters) 
Vertical datum information (in meters) is from NOAA (https://tidesandcurrents.noaa.gov/datums.html?id=9432780).

MERGING DATA
The final products are in Oregon State Plane coordinates. There are two bathy data files (xyz columns in .dat files). To merge the data together, we take two approaches :
1) CoosBay_Bathy_ModelGrid_Eidam.dat: For Emily Eidam's paper on modeling scenarios, we combine all bathy data together in MATLAB using do_bathymetry.m. This m-file combines data together in non-overlapping regions, relying on the LiDAR dataset wherever possible, and filling in from there. The NOAA DEM is the last product used to fill in gaps (and has elevations everywhere). This product is not smoothed and does have 'bumps' and irregularities at certain resolutions. 

2) CoosBay_Bathy_ModelGrid_Conroy.dat: For Ted Conroy's paper on modeling the year 2014, the same bathymetry sources were used, but the final merged product was weight interpolated using MB-system (https://www.mbari.org/products/research-software/mb-system/) and then interpolated onto the model grid. For areas where limited bathymetry data exist such as in the upper reaches of smaller channels, a linear along channel slope with uniform across channel depth was prescribed. Bathymetry on the model grid was smoothed to a limited degree to maintain the sharp bathymetry gradients that exist due to recurring dredging. 
