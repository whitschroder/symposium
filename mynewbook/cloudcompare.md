# Visualizing Lidar Data in Cloud Compare

Point cloud data can be viewed with several types of software. The Florida Peninsular Lidar data are
available in .laz format, which is a zipped point cloud format. To view the point cloud in ArcGIS, the
data must first be converted to the standard .las format. LAStools supports point cloud conversion
through the Command Prompt.

# Converting Point Cloud File Types

```
cd C:\LAStools\bin
```

```
las2las -i "..\USGS_LPC_FL_Peninsular_2018_D18_LID2019_442972_W.laz" -o "..\USGS_LPC_FL_Peninsular_2018_D18_LID2019_442972_W.las"
```

# Cloud Compare

Alternatively, Cloud Compare already supports .laz format, and the above step can be skipped. Load data
in Cloud Compare under File < Open.

```{image} /cloudcompare.png
:alt: cloudcompare
:class: bg-primary mb-1
:width: 100%
```

The default visualization uses RGB colors of the aerial view of the point cloud. The Florida Peninsular Lidar
data do not include RGB colors. For a more useful visualization, select the point cloud in Cloud Compare and
scroll down to Scalar Fields under Properties. Choose Classification:

```{image} /classification.png
:alt: classification
:class: bg-primary mb-1
:width: 100%
```

Or Intensity:

```{image} /intensity.png
:alt: intensity
:class: bg-primary mb-1
:width: 100%
```

# Extracting Elevation Data

We can also extract elevation data to a new Scalar Field. Go to Edit < Scalar Fields < Export coordinate(s)
to SF(s). Make sure Z is selected in the next window and click OK. Scalar Fields under Properties should
automatically be updated to Coord.Z. Under SF display parameters under Properties, you may have to adjust
the sliders to change the minimum and maximum display values to improve the visualization.

```{image} /elevation.png
:alt: elevation
:class: bg-primary mb-1
:width: 100%
```

# Updating Default Visualization

You can update the default visualization by replacing RGB with your preferred visualization, for example, elevation. Go to Edit < Scalar Fields < Convert to RGB. Choose No (do not mix with existing values). You can
also delete all other Scalar Fields except the default to save a smaller file for sharing. Go to Edit < Scalar
Fields < Delete all (!). You can also reduce the file size by choosing Edit < Subsample and selecting a min. space between points (values from 1 to 3 feet, for example) to reduce the point cloud density. Finally, Save your
point cloud as a new file.