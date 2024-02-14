# Applying RGB Colors to Point Clouds

We can add actual RGB colors to the point cloud based on an aerial orthophoto. The source of the orthophoto
can be from drone imagery, for example. Alternatively, we can capture imagery from Google Earth Pro. Using Historical Imagery, we can select the closest date to the Florida Peninsular Lidar data, in this case 2017.

```{image} /googleearth.png
:alt: googleearth
:class: bg-primary mb-1
:width: 100%
```

Under Edit < Copy Image, we can save the file in .tif format. The image now needs to be georeferenced, either
in [ArcGIS](https://pro.arcgis.com/en/pro-app/3.1/help/data/imagery/overview-of-georeferencing.htm) or [QGIS](https://docs.qgis.org/2.18/en/docs/training_manual/forestry/map_georeferencing.html). Once georeferenced,
there should be a .tfw file with the same name as your .tif. Using LAStools, we can add the RGB imagery
to the point cloud.

```
lascolor -i "..\file.las" -image "..\file.tif" -o "..\output.las"
```

We now have a colorized point cloud.

```{image} /colorized.png
:alt: colorized
:class: bg-primary mb-1
:width: 100%
```