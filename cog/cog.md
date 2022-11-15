[Jump to :material-hand-clap: hands-on lesson :material-school: ](#hands-on)

## Overview of :material-layers: Cloud Optimized GeoTIFF (COG)

### Background

The [TIFF file format (Tagged Image File Format)](https://en.wikipedia.org/wiki/TIFF){target=_blank} is an old format dating back to 1992. TIFF are great for high-resolution verbatim [raster images](https://en.wikipedia.org/wiki/Raster_graphics){target=_blank}. TIFF are still used a bit in high-end photography, but where it has really grown a second life is in digital cartography. The variation called [GeoTIFF](https://en.wikipedia.org/wiki/GeoTIFF){target=_blank} has been widely adopted as a way to share satellite images and other satellite data.

While the GeoTIFF file format has long been thought of as only suitable for raw data: if you wanted to display it on a map, you’d convert it into tiles. If you wanted a static image, you’d render it into a PNG or JPEG. But [Cloud-Optimized GeoTIFF](https://en.wikipedia.org/wiki/GeoTIFF#Cloud_Optimised_GeoTIFF){target=_blank} means that GeoTIFFs can be a bit more accessible than they used to be.

??? Info "Relationship of COGs to other cloud native formats"

    Much of the material in this workshop is recursive - you need to know about `GeoJSON` to understand STACs and to work with tools which query COGs, COPC, Zarr, and Xarray data.

    Built to support efficient tile-by-tile access to large collections of geospatial imagery, the COG has provided an excellent template for the development of other cloud-optimized data formats (e.g. [Zarr](https://zarr.readthedocs.io/en/stable/index.html){target=_blank}).

    Like many open source projects, the development and production of COGs has lead to innovation in other areas as well. One example of such innovation is the development of the [SpatioTemporal Asset Catalog (STAC)](stac.md).

    The SpatioTemporal Asset Catalog (STAC) specification provides a common language to describe a range of geospatial information, so it can more easily be indexed and discovered. A ‘spatiotemporal asset' is any file that represents information about the earth captured in a certain space and time.

    COGs and STAC provide the building blocks for a flexible and accessible system for geospatial data analysis (geospatial imagery). STAC provides a system for describing large collections of geospatial data stored in cloud object store and COG provide efficient access to pieces of those collections without the need to download the data first.  

A [Cloud Optimized GeoTIFF (COG)](https://www.cogeo.org/){target=_blank} is a regular [GeoTIFF file](https://en.wikipedia.org/wiki/GeoTIFF){target=_blank}, aimed at being hosted on a HTTP file server, with an internal organization that enables more efficient workflows on the cloud. It does this by leveraging the ability of clients issuing ​HTTP GET range requests to ask for just the parts of a file they need.

Cloud Optimized GeoTIFFs (COGs) are just like regular [GeoTIFF](https://www.ogc.org/standards/geotiff){target=_blank}

[COG Specification](https://github.com/cogeotiff/cog-spec/blob/master/spec.md){target=_blank}

COGs have three major features: internal tiling, internal overview structures, and HTTP GET Range Requests

### Tiling

Internal Tiling GeoTIFFs (typically into 128x128, 256x256, or 512x512 pixel tiles).  

COGs leverage Virtual Raster Tiles (VRT) which are virtual datasets using XML format. GDAL uses VRTs to create mosaic datasets which improve performance for loading and viewing COG data, e.g., [`gdalbuildvrt`](https://gdal.org/programs/gdalbuildvrt.html?highlight=gdalbuildvrt){target=_blank}

### Overviews 

Overviews are downsampled thumbnail images of the tile. A COG will have many overviews matched to each [Zoom Level](https://wiki.openstreetmap.org/wiki/Zoom_levels){target=_blank}.

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geotiff_pyramid.png" target="blank" rel="geotiff_pyramid">![geotiff_pyramid](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geotiff_pyramid.png){ width="700" } </a>
    <figcaption>GeoTIFF pyramid by Zoom Level</figcaption>
</figure>

### HTTP(s) GET Range Request

The [HTTP GET Range Request](https://www.rfc-editor.org/rfc/rfc7233){target=_blank} allows a client to request specific chunks of the COG.

## GDAL

The lastest versions of [GDAL](https://gdal.org){target=_blank} (>v3.1) have [COG generator](https://gdal.org/drivers/raster/cog.html){target=_blank} installed by default.

[Most GIS software](https://gdal.org/software_using_gdal.html#software-using-gdal){target=_blank} use GDAL.

??? Tip "Install GDAL"

    GDAL installation can at times be difficult. When different older python environments are installed on a desktop or laptop GDAL can become broken or incompatiblity issues can come up when installing it.

    [USGS Windows GDAL Installation Guide](https://apps.nationalmap.gov/raster-conversion/gdal-installation-and-setup-guide.html){target=_blank} 

    [Official GDAL Install Guide](https://gdal.org/download.html){target=_blank} 

    [QGIS](https://www.qgis.org/en/site/){target=_blank} installs GDAL by default

    [Anaconda](https://anaconda.org/conda-forge/gdal){target=_blank} and its package management `conda`

    [Docker `osgeo/gdal`](https://hub.docker.com/r/osgeo/gdal){target=_blank} images are maintained on the Docker Hub

* [`cogger`](https://github.com/airbusgeo/cogger){target=_blank} is a rapid COG generator from GeoTIFF

## Example COGs in WebGL

[Open Layers COGs](https://openlayers.org/en/latest/examples/cog.html){target=_blank}

[Open Layers WebGLTile Pyramid from COG](https://openlayers.org/en/latest/examples/cog-pyramid.html){target=_blank}

# Hands On

## **Step 1** Finding COGs on the internet

There are numerous cloud based data stores hosting COGs, take a look through a few of these:

### CyberGIS with COG support

[Google Earth Engine](https://developers.google.com/earth-engine/guides/image_overview){target=_blank} supports Image Collections in COG format.

[Microsoft Planetary Computer Catalog](https://planetarycomputer.microsoft.com/catalog){target=_blank} - most of the imagery datasets in Planetary Computer are hosted as COGs

[OpenAerialMap](https://openaerialmap.org/){target=_blank} hosts drone imagery

### Public Datasets

[NASA](https://www.earthdata.nasa.gov/engage/cloud-optimized-geotiffs){target=_blank}

[ESA Sentinel-2 COGs](https://registry.opendata.aws/sentinel-2-l2a-cogs/){target=_blank}

[AWS STAC Search](https://radiantearth.github.io/stac-browser/#/external/earth-search.aws.element84.com/v0){target=_blank}

## **Step 2** Open the [COG Viewer](https://www.cogeo.org/map/){target=_blank}

Open in your browser the [COG Viewer](https://www.cogeo.org/map/)

Alternate viewers: 

[COGEO.xyz](https://cogeo.xyz/){target=_blank}

Try adding the `https://` URL of the COG that you found on the internet into the viewer.

## **Step 3** Option 1: open a COG in QGIS

* Open QGIS

* In the "Layers" then "Add Layer" and then "Add Raster Layer" 

* Choose the Source Type and select "Protocol: HTTP(s), cloud, etc" for a file on your computer

* Enter a valid `https://` in the `URl` field for a COG you found online

## **Step 4** Optional - create a COG from a GeoTIFF

Open a console and check your `gdal` installation

``` bash
gdalinfo --version
```

Make sure that you're operating on at least `v3.1` of GDAL (current latest `v3.5.1`)

[Sample USGS GeoTIFFs](https://pubs.usgs.gov/ds/121/prescott/prescott.html){target=_blank}

``` bash
gdal_translate p_ndvi_cor.tif p_ndvi_cor_cog.tif \
-b 1 -b 2 -b 3  \
-of COG \
-co TILING_SCHEME=GoogleMapsCompatible \
-co COMPRESS=JPEG \
-co OVERVIEW_QUALITY=100 \
-co QUALITY=100
```

Check the file size of your example file and your output file. Which is larger?

Now, if we want to add overviews to the output `p_ndvi_cor_cog.tif`:

``` bash
gdaladdo \
  --config COMPRESS_OVERVIEW JPEG \
  --config JPEG_QUALITY_OVERVIEW 100 \
  --config PHOTOMETRIC_OVERVIEW YCBCR \
  --config INTERLEAVE_OVERVIEW PIXEL \
  -r average \
  p_ndvi_cor_cog.tif \
  2 4 8 16
```

## **Step 5** Optional: upload the file to a public `https://` endpoint

If you have your own web server, or public cloud bucket, you can upload your new COG and view it using one of the example viewers, or try loading it using QGIS.

Here is an [example using the CyVerse Data Store and the CoGEO viewer](https://www.cogeo.org/map/#/url/https%3A%2F%2Fdata.cyverse.org%2Fdav-anon%2Fiplant%2Fhome%2Ftswetnam%2Fagic-2022%2Fp_ndvi_cor_cog.tif/center/-112.9834,34.4884/zoom/14){target=_blank}

# Additional Reading

[GeoTIFF Compression for Dummies](https://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html){target=_blank} - suggests the best version is "a GeoTIFF, with JPEG compression, internally tiled, in the YCBCR color space, with internal overviews."

[COGS in Production blog post by Sean Rennie](https://sean-rennie.medium.com/cogs-in-production-e9a42c7f54e4){target=_blank}

