# Software for Lidar Visualization and Analysis

Choosing the appropriate software for your project will depend on the scale and goals of your research.
Lidar data consists of raw point cloud data that can be manipulated and filtered to generate additional
visualizations to assess questions regarding terrain, the built environment, and canopy. Anyone working
with Lidar data should have some familiarity with raw point cloud data, as these data represent the actual,
accurate returns from the Lidar survey. Any other products will be based on the point cloud data and may
involve some form of interpolation to create a more continuous surface.

Free, open access, and open source software is available. Some examples have approachable graphical user
interfaces (GUI), while others rely entirely on coding. Although not necessary, some familiarity with coding
will open the door to working with big data and automated analyses.

**Free, Open Access, and/or Open Source**

[Cloud Compare](https://www.danielgm.net/cc)

Cloud Compare is a completely free 3D point cloud viewing and processing software. Despite being free,
Cloud Compare excels at displaying large point cloud data in a simple interface. The software also includes
filtering and raster surface generation. Several tutorials are available on Youtube.

[R, Rstudio](https://posit.co/download/rstudio-desktop)

R is a software and programming language for statistical analysis and visualization. The "lidR" package is useful
for exploratory analysis and automation, although some of the functionality can be slow with large datasets.

[QGIS](https://qgis.org/en/site)

QGIS is an open source software for geographic information systems. Although some point cloud functionality
has been introduced, large datasets can still be a challenge. QGIS is more useful for generating raster derivatives and producing maps.

[Potree](https://github.com/potree/potree) (requires a web server)

Potree is a useful point cloud viewer for sharing data on a website. However, the point cloud viewer only
works with a dedicated web server. Files can be very large.

[PDAL](https://pdal.io/en/2.6.0)

Like R, PDAL is a software that requires coding knowledge. PDAL is a C++ language and is generally faster than R.

**Licensed**

[ArcGIS Pro](https://www.geoplan.ufl.edu/software/arcgis-pro) (available to UF students)

ArcGIS remains one of the most popular geographic informations system software, and although the software is
proprietary, students at UF have access. Like QGIS, ArcGIS Pro is generally better for raster analysis, as the point cloud viewer can be slow with large datasets. The ground filtering algorithm in ArcGIS Pro is among the fastest. ArcGIS Pro does not suppor .laz formats.

[LAStools](https://lastools.github.io/) (some tools are open access)

LAStools software consists of an extensive and useful set of tools for analyzing and processing Lidar data.
Some of the tools are open access, for example, las2las and lasinfo for converting and reading point cloud
data, respectively.

[Sketchfab](https://sketchfab.com)

Sketchfab is "the best 3D viewer on the web" for sharing data online, without requiring a web server. The platform is subscription-based, with upload limits. Still, Sketchfab remains the best option for sharing 3D data. Support for .las files is not reliable, but .asc files work.