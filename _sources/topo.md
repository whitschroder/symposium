# Datasets for Digital Elevation Models

## DEM vs. DSM vs. DTM

The terms digital elevation model (DEM), digital surface model (DSM), and digital terrain model (DTM) do not have consistent definitions. In some usages, DEM can refer to any raster surface that reflects height, and therefore a DSM and a DTM are a type of DEM. In other uses, DEM and DTM are synonymous and refer to only the elevation of the ground. In the United States, a DTM more often refers to a DEM that has additional data, namely vectors that mark additional data, including rivers, ridges, and breaklines. Some archaeologists have suggested using DTM to refer to a DEM that includes above ground archaeological features. The term used most consistently is DSM, which models all ground and above ground objects.

## Sensor Types for Modeling Topography

The most commonly used methods used for generating digital elevation models include photogrammetry, radar, and lidar. Photogrammetry (based on stereoscopy) uses cameras to take overlapping imagery that can be used to generate three dimensional models. Although accurate, photogrammetry is unable to model topography under dense vegetation. Radar uses radio waves to measure the distance between the earth's surface and the sensor. As an active sensor, radar generates it's own energy source, in contrast to photogrammetry (a passive technology) that records the reflected energy from the sun. Therefore, radar can be used during the day or night. Although better able to penetrate vegetation compared to photogrammetry, radar is still unable to model the ground's surface in areas of dense vegetation or steep topography. Finally, lidar has emerged as a common technology for topographic modeling, especially in documenting archaeological and cultural landscapes. Lidar is also an active sensor that sends pulses of light and measures the time and distance traveled between pulses and returns. Most of these returns reflect off vegetation and above ground objects, but some pulses are able to reach the ground, allowing for the highest resolution and most accurate modeling of the ground's surface.

## SRTM

The Shuttle Radar Topography Mission (SRTM) used two radar antennae mounted on the Space Shuttle Endeavour in 2000 to produce the first near global DEM, specifically 80% of the Earth's land surface between 60° north and 56° south latitude. Although radar can penetrate vegetation, results can be poor in densely forested areas and rugged terrain.

SRTM data are available in three formats:

<b>SRTM Non-Void Filled</b> elevation data contains voids from densely forested areas and rugged terrain at a resolution of 1-arc second (approximately 30 m at the equator) in the United States and 3-arc seconds (approximately 90 m at the equator) outside the United States.

<b>SRTM Void Filled</b> elevation data combined interpolation and other data sources to fill voids. The resolution is 1-arc second (approximately 30 m at the equator) in the United States and 3-arc seconds (approximately 90 m at the equator) outside the United States. 

<b>SRTM 1 Arc-Second Global</b> is a near-global dataset with improved resolution of 1-arc second (approximately 30 m at the equator), except for areas above 50° north and below 50° south latitude, which were sampled at a resolution of 1-arc second by 2-arc seconds. Some voids may still be present.

SRTM data are available through the [USGS Earth Explorer](https://earthexplorer.usgs.gov/).

## ASTER

The Advanced Spaceborne Thermal Emission and Reflection Radiometer (ASTER) was a Japanese multispectral sensor mounted on NASA's Terra satellite in 1999. Stereo imagery was processed to generate the first version of the ASTER Global Digital Elevation Model (GDEM), perhaps more appropriately called a DSM, covering 99% of the Earth's land surface between 83° north and 83° south latitude. The third version of the GDEM was released in 2019 with significant improvements, removing above ground artifacts.

ASTER data are no longer available through the USGS Earth Explorer and can instead be downloaded from [NASA Earth Data Search](https://search.earthdata.nasa.gov/search). 

## AIRSAR

A product of the Jet Propulsion Laboratory (JPL), the Airborne Synthetic Aperture Radar (AIRSAR) instrument was an airborne system that operated from 1988 to 2004, collecting limited data over selected study regions, at approximately 5 m resolution. AIRSAR data can be browsed through a list of [missions](https://airsar.jpl.nasa.gov/cgi-bin/internet.plex) a search for [precision data](https://airsar.jpl.nasa.gov/cgi-bin/search.plex), and an [interactive map](https://airsar.jpl.nasa.gov/cgi-bin/map.pl).

## USGS 3D Elevation Program (3DEP)

Near nationwide digital elevation models for the U.S. are available at the [National Map](https://apps.nationalmap.gov/downloader/). Data are available at 1 m, 5 m, 10 m, and 30 m resolution.

## Open Topography

Additional topographic data may be available at [Open Topography](https://opentopography.org/). This website provides convenient links to available USGS and user-submitted data.