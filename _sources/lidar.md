# Analyzing and Visualizing Lidar Data

Whatever goals and software you have chosen for your project, the first step when working with Lidar data
is visualizing the point cloud. This tutorial will work with several datasets from Florida's Peninsular Lidar
available at: <https://apps.nationalmap.gov/downloader>. Zoom into Levy County and select "Elevation Source Data
(3DEP) - Lidar, IfSAR." Click "Search Products." Download the following 3 products:

Cedar Key: USGS_LPC_FL_Peninsular_2018_D18_LID2019_445066_W.laz  
Shell Mound: USGS_LPC_FL_Peninsular_2018_D18_LID2019_443564_W.laz  
Rosewood: USGS_LPC_FL_Peninsular_2018_D18_LID2019_442972_W.laz

```{image} /USGS.png
:alt: USGS
:class: bg-primary mb-1
:width: 100%
```  

This point cloud can be loaded into Cloud Compare (File < Open). To open in ArcGIS Pro, first convert to .las
format using the las2las tool in LAStools. The following command can be run from the Command Prompt:

```
cd C:\LAStools\bin
```

```
las2las -i "USGS_LPC_FL_Peninsular_2018_D18_LID2019_442972_W.laz" -o "USGS_LPC_FL_Peninsular_2018_D18_LID2019_442972_W.las"
```

In Cloud Compare, under "Scalar Fields," change to "Classification." Adjust the "Color Scale."

The Classification is based on the American Society for Photogrammetry and Remote Sensing (ASPRS) standard
classification codes for point cloud data:

| Classification Value | Meaning                       |
| ---                  | ---                           |
| 0                    | Created, never classified     |
| 1                    | Unclassified                  |
| 2                    | Ground                        |
| 3                    | Low Vegetation                |
| 4                    | Medium Vegetation             |
| 5                    | High Vegetation               |
| 6                    | Building                      |
| 7                    | Low Point (noise)             |
| 8                    | Reserved                      |
| 9                    | Water                         |
| 10                   | Rail                          |
| 11                   | Road Surface                  |
| 12                   | Reserved                      |
| 13                   | Wire - Guard (Shield)         |
| 14                   | Wire - Conductor (Phase)      |
| 15                   | Transmission Tower            |
| 16                   | Wire-structure Connector (e.g., Insulator |
| 17                   | Bridge Deck |
| 18                   | High Noise |
| 19-63                | Reserved |
| 64-255               | User definable |

After adjusting the colors of the point cloud based on classification, the Cedar Key point cloud look something
like this:  

<div class="sketchfab-embed-wrapper"> <iframe title="Cedar Key, Florida" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" allow="autoplay; fullscreen; xr-spatial-tracking" xr-spatial-tracking execution-while-out-of-viewport execution-while-not-rendered web-share width="640" height="480" src="https://sketchfab.com/models/b4a408d1624b4870ac8a77a1405ba1d4/embed"> </iframe> </div>  

The Shell Mound data are in a more forested area with fewer buildings:  

<div class="sketchfab-embed-wrapper"> <iframe title="Shell Mound, Florida" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" allow="autoplay; fullscreen; xr-spatial-tracking" xr-spatial-tracking execution-while-out-of-viewport execution-while-not-rendered web-share width="640" height="480" src="https://sketchfab.com/models/6c6cb8086e684cf48298391e08f7dfb3/embed"> </iframe> </div>  

We can filter out the trees, creating a digital terrain model or bare earth surface, and we can color the points based on ground elevation.  

<div class="sketchfab-embed-wrapper"> <iframe title="Shell Mound Terrain" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" allow="autoplay; fullscreen; xr-spatial-tracking" xr-spatial-tracking execution-while-out-of-viewport execution-while-not-rendered web-share width="640" height="480" src="https://sketchfab.com/models/38a3e58c855a4d6eb2d58ba361f2c31e/embed"> </iframe> </div>  

Here are the point cloud data for Rosewood. What are some other ways to visualize the data?  

<div class="sketchfab-embed-wrapper"> <iframe title="Rosewood, Florida" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" allow="autoplay; fullscreen; xr-spatial-tracking" xr-spatial-tracking execution-while-out-of-viewport execution-while-not-rendered web-share width="640" height="480" src="https://sketchfab.com/models/50dec59c9a1642e8a10be4d5a59e38d6/embed"> </iframe> </div>

[Palenque](https://pointcloud.ucsd.edu/published/Palenque_3D_Atlas.html)  
[Cedar Key Point Cloud on Potree](https://whitschroder.github.io/cedarkey)  
[Shell Mound](https://whitschroder.github.io/shellmound)  
[Rosewood](https://whitschroder.github.io/rosewood)  

```
lascolor -i "..\file.las" -image "..\file.tif" -o "..\output.las"
```

```
PotreeConverter.exe "..\output.las" -o "..\destinationFolder" -generate-page pageName
```

```Bash
cd "..\repositoryFolder"
```

```Bash
git clone https://github.com/<my-org>/<my-repository-name>
```

Copy Potree files into the new folder created in the repository folder.

```Bash
cd "..\repositoryFolder\newfolder"
```

```Bash
git add ./*
```

```Bash
git commit -m "adding"
```

```Bash
git push
```

Go to your repository settings, scroll to "Pages." Under "Branch," change "None" to "main" and save.