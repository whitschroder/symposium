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

In the following tutorials, we will be viewing data from Cedar Key, Rosewood, and Shell Mound, Florida:

<iframe src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d78817.76733381792!2d-83.05155165717139!3d29.185702416257122!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x88e9a86e34bf85ab%3A0xccb1a32e3fa7829f!2sShell%20Mound%20Trl%2C%20Florida%2032625!5e0!3m2!1sen!2sus!4v1708021704284!5m2!1sen!2sus" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>