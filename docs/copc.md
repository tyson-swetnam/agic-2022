[Jump to :material-hand-clap: hands-on lesson :material-school: ](#hands-on)

## Overview of :material-file-cloud: Cloud Optimized Point Cloud (COPC)

A [Cloud Optimized Point Cloud](https://copc.io/){target=_blank} is a `.laz` file `v1.4` that stores point data organized in a clustered [octree](https://en.wikipedia.org/wiki/Octree){target=_blank}. 

[COPC Specification](https://copc.io/copc-specification-1.0.pdf){target=_blank}

[LAS Standard](https://www.asprs.org/a/society/committees/standards/LAS_1_4_r13.pdf){target=_blank}

A COPC contains a [variable length record (VLR)](https://pdal.io/en/stable/tutorial/las.html?highlight=VLR#variable-length-records){target=_blank} that describe the octree organization of data that arestored in LAZ 1.4 chunks

COPC would not be possible without the Open Source compression file format, `*.LAZ`, which was developed by Martin Isenburg ([RIP](https://lidarmag.com/2021/10/30/in-memoriam-martin-isenburg-1972-2021/){target=_blank}) and is licensed by his company [RapidLASso](https://rapidlasso.de/){target=_blank} 

<a href="https://rapidlasso.de/" target="blank" rel="rapidlasso">![rapidlasso](https://rapidlasso.de/wp-content/uploads/rapidlasso_square_256x2561.png){ width="100" } </a>

### Background on COPC

 <a href="https://hobu.co" target="blank" rel="hobu">![hobu](https://hobu.co/theme/images/hobulogo.png){ width="100" } </a>

[HoBu Inc.](https://hobu.co/){target=_blank} open source license their software for working with a wide variety of lidar data types. Hobu's portfolio now includes:

<a href="https://pdal.io" target="blank" rel="pdal">![pdal](https://pdal.io/_images/pdal_logo.png){ width="100" } </a>

[Point Data Abstraction Library (PDAL)](https://pdal.io){target=_blank} is a C++ library for translating and manipulating point cloud data.

<a href="https://entwine.io" target="blank" rel="entwine">![entwine](https://entwine.io/_images/entwine_logo_2-color.png){ width="100" } </a>

[Entwine](https://entwine.io){target=_blank} is a data organization library for massive point clouds, designed to conquer datasets of trillions of points as well as desktop-scale point clouds.

HoBu was contracted by the USGS to process all of the 3DEP lidar data, these are now hosted on commercial cloud in both reqestor pays buckets and FOR FREE as Entwine Point Tiles: [https://usgs.entwine.io/](https://usgs.entwine.io/)

* More information about these datasets can be found at https://registry.opendata.aws/usgs-lidar/ and at its GitHub page at https://github.com/hobu/usgs-lidar/

* [USGS National Datasets Downloads](https://www.usgs.gov/faqs/can-national-map-data-be-downloaded-direct-links){target=_blank}

<a href="https://copc.io" target="blank" rel="copc">![copc](https://copc.io/COPC_IO-Logo-2color.png){ width="100" } </a>

??? Tip "Installing Open Source Lidar tools"

    [LASTools](https://rapidlasso.com/lastools/){target=_blank} is available for both open source and a paid licensed version

    [PDAL.io](https://pdal.io/en/stable/download.html#current-release-s){target=_blank} - suggest using a Binary install using a package manager like `conda`.

# Hands On

## **Step 1** Go to [COPC.io Viewer](https://viewer.copc.io/){target=_blank}

The [viewer.copc.io](https://viewer.copc.io/){target=_blank} is an experimental Viewer for EPT and COPC point clouds hosted over `https://`

The COPC viewer can dynamically view COPC processed `.laz` that are stored on the internet. 

[COPC Viewer Example of 3DEP lidar over Prescott AZ from USGS](https://viewer.copc.io/?copc=https://data.cyverse.org/dav-anon/iplant/home/tswetnam/agic-2022/USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019.copc.laz)

These data were converted from USGS 3DEP EPT data using PDAL `pipeline` 

??? Tip "processing AWS EPT with PDAL

    USGS 3DEP data are all freely available over `https://` using the Entwine protocol. 

    These data can be re-processed to become COPC using PDAL's `writers.copc` function.

    Example [`ept2copc.json`](../assets/json/ept2copc.json) script for running directly from the internet to your computer or local host

    **Warning** you must have a fast internet connection and a large amount of RAM on your machine to process large datasets (spatial extent / dense point clouds)

    ``` bash
    conda activate pdal
    ```

    ??? abstract "ept2copc.json"

        Contents of [`ept2copc.json`](../assets/json/ept2copc.json)

        ```
            {
                "pipeline": [
                    {
            "bounds": "([-12521659, -12513587], [4099398, 4107470], [1500, 3200])",
            "filename": "https://s3-us-west-2.amazonaws.com/usgs-lidar-public/USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019/ept.json",
            "type": "readers.ept",
            "requests": 128,
            "tag": "readdata"
                    },
                    {
                        "type":"filters.outlier",
                        "method":"statistical",
                        "mean_k":12,
                        "multiplier":2.2
                    },
                    {
                        "type":"filters.smrf",
                        "scalar":1.2,
                        "slope":0.2,
                        "threshold":0.45,
                        "window":16.0
                    },
                    {
                        "type": "filters.range",
                        "limits": "Classification![7:7],Z[2000:2700]"
                    },
                    {
                        "type":"filters.hag_delaunay"
                    },
                    {
                        "in_srs": "EPSG:3857",
                        "out_srs": "EPSG:26912",
                        "tag": "reprojectUTM",
                        "type": "filters.reprojection"
                    },
                    {
                        "filename": "USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019.copc.laz",
                        "inputs": [ "reprojectUTM" ],
                        "tag": "writerscopc",
                        "type": "writers.copc"
                    },
                    {
                        "filename": "USGS_LPC_AZ_VerdeKaibab_B2_TL_2018_LAS_2019_dem.tif",
                        "gdalopts": "tiled=yes,     compress=deflate",
                        "inputs": [ "writerscopc" ],
                        "nodata": -9999,
                        "output_type": "min",
                        "resolution": 1.0,
                        "type": "writers.gdal",
                        "window_size": 6
                    }
                ]
            }
        ```


    ```
    pdal -v 5 pipeline ept2copc.json
    ```


## COPC Creation

[Planetary Computer 3DEP Jupyter Notebook](https://github.com/microsoft/PlanetaryComputerExamples/blob/main/datasets/3dep-lidar/3dep-lidar-copc-example.ipynb){target=_blank}

## Reference Material

[Library of Congress LAS definition](https://www.loc.gov/preservation/digital/formats/fdd/fdd000418.shtml){target=_blank}

[OGC LAS Standard](https://www.ogc.org/standards/LAS){target=_blank}

[USGS NGS Lidar Base Specification](https://www.usgs.gov/ngp-standards-and-specifications/lidar-base-specification-online){target=_blank}

