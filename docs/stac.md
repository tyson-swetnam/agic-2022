## What is a STAC

The [SpatioTemporal Asset Catalog (STAC)](https://stacspec.org/en){target=_blank} specification provides a common structure for describing and cataloging spatiotemporal assets on the internet. 

A [STAC Browser](https://radiantearth.github.io/stac-browser/#/){target=_blank} allows users to search, preview, and access these massive geospatial assets hosted over conventional `https://` endpoints and cloud-base object stores (i.e., `s3://` buckets).

There are four components to making a given STAC run. They can be used independently of one another, but most often they are all used together:

| Component | Definition | Format |
|-----------|------------|--------|
| `item` | core atomic unit, representing a single spatiotemporal `asset` | `GeoJSON` |
| `catalogs` | a file of links that provides a structure to organize and browse STAC Items | `JSON` |
| `collections` | additional information such as the extents, license, keywords, providers, etc that describe STAC Items | `JSON` |
| `API` | a RESTful endpoint that enables search of STAC Items, specified in [OpenAPI](https://spec.openapis.org/oas/v3.1.0){target=_blank}, following [OGC Web Feature Service 3.0](https://svn.osgeo.org/gdal/trunk/gdal/ogr/ogrsf_frmts/wfs/drv_wfs3.html){target=_blank} | Web Service |

### `asset`

The `assets` are the actual datasets being presented through the STAC. 

These are typically stored in [cloud optimized GeoTIFF (COG)](./cog.md) (`.tif`), [cloud optimized point cloud (COPC)](./copc.md) (`.laz`), or [datacubes](./zarr.md) like HDF5, NetCDF, Zarr, (`.hdf`, `.nc`, `.zarr`).

within the `assets`, the `"href": "https://storage.googleapis.com/open-cogs/stac-examples/20201211_223832_CS2.tif",` points directly to the file on the internet.

Example `assets` block in an `item`:

``` json
"assets": {
    "visual": {
        "href": "https://storage.googleapis.com/open-cogs/stac-examples/20201211_223832_CS2.tif",
        "type": "image/tiff; application=geotiff; profile=cloud-optimized",
        "title": "3-Band Visual",
        "roles": [
            "visual"
        ]
    },
    "thumbnail": {
        "href": "https://storage.googleapis.com/open-cogs/stac-examples/20201211_223832_CS2.jpg",
        "title": "Thumbnail",
        "type": "image/jpeg",
        "roles": [
            "thumbnail"
        ]
    }
}
```

### `items` 

An `item` is described by [GeoJSON]() with metadata which describe an `asset` and links to the actual data hosted on the internet. 

[`item` specification](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md){target=_blank}

`items` enable the client (a STAC Browser) to scan a `catalog` and present the metadata and to preview the `asset`.

[Example simple-item.json](https://raw.githubusercontent.com/radiantearth/stac-spec/master/examples/simple-item.json){target=_blank}

``` json
{
    "stac_version": "1.0.0",
    "stac_extensions": [],
    "type": "Feature",
    "id": "20201211_223832_CS2",
    "bbox": [
        172.91173669923782,
        1.3438851951615003,
        172.95469614953714,
        1.3690476620161975
        ],
    "geometry": {
        "type": "Polygon",
        "coordinates": [
            [
                [
                    172.91173669923782,
                    1.3438851951615003
                ],
                [
                    172.95469614953714,
                    1.3438851951615003
                ],
                [
                    172.95469614953714,
                    1.3690476620161975
                ],
                [
                    172.91173669923782,
                    1.3690476620161975
                ],
                [
                    172.91173669923782,
                    1.3438851951615003
                ]
            ]
        ]
    },
    "properties": {
    "datetime": "2020-12-11T22:38:32.125000Z"
    },
    "collection": "simple-collection",
    "links": [
        {
            "rel": "collection",
            "href": "./collection.json",
            "type": "application/json",
            "title": "Simple Example Collection"
        },
        {   
            "rel": "root",
            "href": "./collection.json",
            "type": "application/json",
            "title": "Simple Example Collection"
        },
        {
            "rel": "parent",
            "href": "./collection.json",
            "type": "application/json",
            "title": "Simple Example Collection"
        }
    ],
    "assets": {
        "visual": {
            "href": "https://storage.googleapis.com/open-cogs/stac-examples/20201211_223832_CS2.tif",
            "type": "image/tiff; application=geotiff; profile=cloud-optimized",
            "title": "3-Band Visual",
            "roles": [
                "visual"
            ]
        },
        "thumbnail": {
            "href": "https://storage.googleapis.com/open-cogs/stac-examples/20201211_223832_CS2.jpg",
            "title": "Thumbnail",
            "type": "image/jpeg",
            "roles": [
                "thumbnail"
            ]
        }
    }
}
```

### `catalogs` 

A `catalog` is a simple, flexible JSON file with links that provides the structure to organize and browse STAC `items`. 

[`catalog` specification](https://github.com/radiantearth/stac-spec/blob/master/catalog-spec/catalog-spec.md){target=_blank}

```

```

**STAC Catalog Relation and Media Types**

`Self`: Absolute URL to the JSON file

`Root`: URL to root `catalog` or `collection`

`Parent`: URL to a Parent STAC Specification (could be an `item`, `catalog`, or `collection`)

`Child`: URL to a Child STAC Specification (`item`, `catalog`, or `collection`)

```

```

### `collections`

[`collection specification](https://github.com/radiantearth/stac-spec/blob/master/collection-spec/collection-spec.md){target=_blank}

```

```

### API 

The STAC API 

[`API` specification](){target=_blank}

## Creating your own STACs

Generating your own STACs can be done manually, programmatically, or using a templated editor. 

[Create a Catalog with PyStac](https://developers.planet.com/docs/planetschool/){target=_blank}introduction-to-stac-part-2-creating-an-example-stac-catalog-of-planet-imagery-with-pystac/){target=_blank}


## Examples of STAC Browser

Radiant Earth maintains the [STAC Browser](https://radiantearth.github.io/stac-browser/#/){target=_blank}

[QGIS STAC Browser Plugin](https://github.com/stac-utils/qgis-stac-plugin){target=_blank}

[Scene Explorer ESRI](https://www.esri.com/en-us/arcgis-marketplace/listing/products/b1689f3ddcf742de988e0d5a070b31c4){target=_blank}

## STAC Major Sponsors & Contributors

Microsoft

Radiant Earth

Planet