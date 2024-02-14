# Analyzing and Visualizing Lidar Data

Lidar data is useful for creating 3D models of cultural heritage objects and the built environment. Raw lidar
data consists of a point cloud that can be classified to define objects in space. This point cloud can then
be used to generate a 3D mesh or a digital elevation model (DEM).

Classification is based on the American Society for Photogrammetry and Remote Sensing (ASPRS) standard classification codes for point cloud data:

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

In the following tutorial, we will download publicly available lidar data, visualize the point cloud, and
share the data online. Here are examples of point cloud data available online:

[Palenque](https://pointcloud.ucsd.edu/published/Palenque_3D_Atlas.html)  

[Cedar Key Point Cloud on Potree](https://whitschroder.github.io/cedarkey)  