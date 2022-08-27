[Jump to :material-hand-clap: hands-on lesson :material-school: ](#hands-on)

## :material-file-cloud: Cloud Optimized Point Cloud (COPC)

 <a href="https://hobu.co" target="blank" rel="hobu">![hobu](https://hobu.co/theme/images/hobulogo.png){ width="100" } </a>

[HoBu Inc.](https://hobu.co/){target=_blank} open source license their software for working with a wide variety of lidar data types. Hobu's portfolio now includes:

<a href="https://pdal.io" target="blank" rel="pdal">![pdal](https://pdal.io/_images/pdal_logo.png){ width="100" } </a>

[Point Data Abstraction Library (PDAL)](https://pdal.io){target=_blank} is a C++ library for translating and manipulating point cloud data.

<a href="https://entwine.io" target="blank" rel="entwine">![entwine](https://entwine.io/_images/entwine_logo_2-color.png){ width="100" } </a>

[Entwine](https://entwine.io){target=_blank} is a data organization library for massive point clouds, designed to conquer datasets of trillions of points as well as desktop-scale point clouds.

HoBu was contracted by the USGS to process all of the 3DEP lidar data, these are now hosted on commercial cloud in both reqestor pays buckets and FOR FREE as Entwine Point Tiles 

https://usgs.entwine.io/

More information about these datasets can be found at https://registry.opendata.aws/usgs-lidar/ and at its GitHub page at https://github.com/hobu/usgs-lidar/

<a href="https://copc.io" target="blank" rel="copc">![copc](https://copc.io/COPC_IO-Logo-2color.png){ width="100" } </a>

A [Cloud Optimized Point Cloud](https://copc.io/){target=_blank} is a LAZ 1.4 file that stores point data organized in a clustered octree. 

A COPC contains a variable length record (VLR) that describe the octree organization of data that arestored in LAZ 1.4 chunks

COPC would not be possible without the Open Source compression file format, `*.LAZ`, which was developed by Martin Isenburg ([RIP](https://lidarmag.com/2021/10/30/in-memoriam-martin-isenburg-1972-2021/){target=_blank}) and is licensed by his company [RapidLASso](https://rapidlasso.de/){target=_blank} 

<a href="https://rapidlasso.de/" target="blank" rel="rapidlasso">![rapidlasso](https://rapidlasso.de/wp-content/uploads/rapidlasso_square_256x2561.png){ width="100" } </a>

## The COPC Format

## COPC Creation

## COPC Viewer

[viewer.copc.io](https://viewer.copc.io/){target=_blank} - experimental Viewer for EPT and COPC point clouds hosted over `https://`

## Reference Material

[Library of Congress LAS definition](https://www.loc.gov/preservation/digital/formats/fdd/fdd000418.shtml)

[OGC LAS Standard](https://www.ogc.org/standards/LAS){target=_blank}

[USGS NGS Lidar Base Specification](https://www.usgs.gov/ngp-standards-and-specifications/lidar-base-specification-online){target=_blank}

