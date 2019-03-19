# Coos-Bay-Bathymetry
Coos Bay bathymetry product created from merging different datasets together. Please cite forthcoming paper on Coos Bay bathy (either Eidam et al. 2019 or Conroy et al. 2019). The bathymetry is used in numerical simulations of the hydrodynamics of the estuary; hence it is on an unstructured mesh-type grid. 

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

6. I also made a DEM off of this website: https://maps.ngdc.noaa.gov/viewers/wcs-client/

All data was converted to:
Horizontal - geographic NAD83 (very similar to WGS 1984)
Vertical - Mean Sea Level (MSL) (meters) 
Vertical datum information (in meters) is from NOAA (https://tidesandcurrents.noaa.gov/
datums.html?id=9432780).

MERGING DATA
To merge the data together, we combine all bathy data together in MATLAB using do_bathymetry.m. This m-file combines data together in non-overlapping regions, relying on the LiDAR dataset wherever possible, and filling in from there. The NOAA DEM is the last product used to fill in gaps (and has elevations everywhere). 

The resulting merged product was smoothed before final use in the model. In addition, we had to quality control several areas of the estuary where data were not available and we knew that deeper depths existed (Isthmus Slough, Coos River, etc.).
