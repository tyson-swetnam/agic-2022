[Jump to :material-hand-clap: hands-on lesson :material-school: ](#hands-on)

## :material-layers: Cloud Optimized GeoTIFF (COG)

Cloud Optimized GeoTIFFs (COGs) are just like regular [GeoTIFF](https://www.ogc.org/standards/geotiff){target=_blank}

COGs have three major features: internal tiling, internal overview structures, and HTTP:// `GET` range requests

[COG Specification](https://github.com/cogeotiff/cog-spec/blob/master/spec.md){target=_blank}

### Tiling

Internal **Tiling** GeoTIFFs (typically into 128x128, 256x256, or 512x512 pixel tiles).  

#### Virtual Raster Tiles (VRT)

Virtual Raster Tiles (VRT) are virtual datasets using XML format. 

GDAL uses VRTs to create mosaic datasets which improve performance for loading and viewing COG data.

[`gdalbuildvrt`](https://gdal.org/programs/gdalbuildvrt.html?highlight=gdalbuildvrt)

### Overviews 

**Overviews** are downsampled thumbnail images of the tile. A COG will have many overviews matched to each [Zoom Level](https://wiki.openstreetmap.org/wiki/Zoom_levels){target=_blank}.

### HTTP(s) GET Range Request

The [HTTP GET Range Request](https://www.rfc-editor.org/rfc/rfc7233){target=_blank} allows a client to request specific chunks of the COG.

## GDAL

The lastest versions of [GDAL](https://gdal.org){target=_blank} (>v3.1) have [COG generator](https://gdal.org/drivers/raster/cog.html){target=_blank} installed by default.

[Most GIS software](https://gdal.org/software_using_gdal.html#software-using-gdal){target=_blank} use GDAL.

``` bash
gdal_translate example.tif example_webmerc_cog.tif -of COG -co TILING_SCHEME=GoogleMapsCompatible -co COMPRESS=JPEG
```

??? Tip "Installing GDAL locally"

    GDAL installation can be difficult. When different python environments are installed on a desktop or laptop GDAL can become broken or incompatiblity issues can come up.

    [USGS Windows GDAL Installation Guide](https://apps.nationalmap.gov/raster-conversion/gdal-installation-and-setup-guide.html){target=_blank} 

    [Official GDAL Install Guide](https://gdal.org/download.html){target=_blank} 

    [QGIS](https://www.qgis.org/en/site/){target=_blank} installs GDAL by default

    [Anaconda](https://anaconda.org/conda-forge/gdal){target=_blank} and its package management `conda`

    [Docker `osgeo/gdal`](https://hub.docker.com/r/osgeo/gdal) images are maintained on the Docker Hub

## Example COGs

[Open Layers COGs](https://openlayers.org/en/latest/examples/cog.html){target=_blank}

# Hands On

## **Step 1** Finding COGs on the internet

There are numerous cloud based data stores hosting COGs, take a look through a few of these:

### CyberGIS with COG support

[Google Earth Engine](https://developers.google.com/earth-engine/guides/image_overview){target=_blank} supports Image Collections in COG format.

[Microsoft Planetary Computer Catalog](https://planetarycomputer.microsoft.com/catalog){target=_blank} - most of the imagery datasets in Planetary Computer are hosted as COGs

### Public Datasets

[NASA](https://www.earthdata.nasa.gov/engage/cloud-optimized-geotiffs){target=_blank}

[ESA Sentinel-2 COGs](https://registry.opendata.aws/sentinel-2-l2a-cogs/){target=_blank}

[AWS STAC Search](https://radiantearth.github.io/stac-browser/#/external/earth-search.aws.element84.com/v0){target=_blank}

## **Step 2** Open the [COG Viewer](https://www.cogeo.org/map/){target=_blank}

Open in your browser the [COG Viewer](https://www.cogeo.org/map/)

Try adding the `https://` URL of the COG that you found on the internet into the viewer.

## 

[COG-Explorer](https://geotiffjs.github.io/cog-explorer/#long=-112.370&lat=35.210&zoom=5&scene=&bands=&pipeline=)

[COGEO.xyz](https://cogeo.xyz/){target=_blank}

# Additional Reading

[GeoTIFF Compression for Dummies](https://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html){target=_blank} - suggests the best version is "a GeoTIFF, with JPEG compression, internally tiled, in the YCBCR color space, with internal overviews."

[COGS in Production blog post by Sean Rennie](https://sean-rennie.medium.com/cogs-in-production-e9a42c7f54e4){target=_blank}