
[Jump to :material-hand-clap: hands-on lesson :material-school: ](#hands-on)

## Overview of :material-code-json: GeoJSON (Geo+JSON)

To begin with, [JavaScript Object Notation (JSON)](https://www.json.org/json-en.html){target=_blank} is a lightweight, text-based, language-independent data interchange format. 

* [JSON syntax](https://www.w3schools.com/js/js_json_syntax.asp){target=_blank}
* [rfc7159](https://datatracker.ietf.org/doc/html/rfc7159){target=_blank}

??? Info "an old style example the JSON Schema for a geospatial object"
  
    ``` json
    {
      "$id": "https://example.com/geographical-location.schema.json",
      "$schema": "https://json-schema.org/draft/2020-12/schema",
      "title": "AGIC Venue",
      "description": "A geographical coordinate where this workshop is being taught",
      "required": [ "latitude", "longitude" ],
      "type": "object",
      "properties": {
        "latitude": {
          "type": "number",
          "minimum": -90,
          "maximum": 90
        },
        "longitude": {
          "type": "number",
          "minimum": -180,
          "maximum": 180
        }
      }
    }
    ```
    The location **data** section of the JSON later describes a point:
    
    ``` json
    {
      "latitude": 34.5510,
      "longitude": -112.4471
    }
    ```

[:material-code-json: GeoJSON](https://geojson.org/){target=_blank} is a format for encoding a variety of geographic data structures.

* [GeoJSON Specification](https://geojson.org){target=_blank}

* [rfc7946](https://datatracker.ietf.org/doc/html/rfc7946){target=_blank}

A GeoJSON Object may represent a region of space: a **Geometry**, a **Feature**, or a list of Features called a **FeatureCollection**.

### :material-angle-acute: Geometry

There are seven types of geometric shapes which can be defined in GeoJSON. Where the "type" can be any of the following:

| Type | Geometry |
| :--: | :--:     |
|Point   |  ![Point](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c2/SFA_Point.svg/51px-SFA_Point.svg.png)|
| LineString   |  ![Linestring](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/SFA_LineString.svg/51px-SFA_LineString.svg.png)|
|Polygon   |   ![Polygon](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/SFA_Polygon.svg/51px-SFA_Polygon.svg.png) |
|MultiPoint|  ![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d6/SFA_MultiPoint.svg/51px-SFA_MultiPoint.svg.png)  |
| MultiLineString  |    ![MultiLineString](https://upload.wikimedia.org/wikipedia/commons/thumb/8/86/SFA_MultiLineString.svg/51px-SFA_MultiLineString.svg.png)|
|MultiPolygon   |  ![MultiPolygon](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/SFA_MultiPolygon_with_hole.svg/51px-SFA_MultiPolygon_with_hole.svg.png)
| GeometryCollection | ![GeometryCollection](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1d/SFA_GeometryCollection.svg/51px-SFA_GeometryCollection.svg.png) |

* Point, LineString and Polygon are *single type geometry objects* 

* MultiPoint, MultiLineString, and MultiPolygon are *multipart geometry objects*

Each of the examples below represents a valid and complete GeoJSON object:

#### :material-map-marker: Point

??? Info ":material-code-json: GeoJSON Point Schema"

    ``` json
    { 
      "type": "Point",
      "coordinates": [-112.4471, 34.5510]
    }
    ```

    A `Point` geometry is represented by a single set of longitude then latitude coordinates, optionally elevation (above mean sea level) can also be included for a third axis.  


#### :material-vector-polyline: LineString 

??? Info ":material-code-json: GeoJSON LineString Schema"

    ``` json
    {
      "type": "LineString",
      "coordinates": [ 
          [-112.4470, 34.5510], [-112.4695,  34.541]  
        ]
    }
    ```

    A `Line` geometry uses two or more sets of coordinate pairs to create a line or multi-line.

#### :material-vector-polygon: Polygon

??? Info ":material-code-json: GeoJSON Polygon Schema"

    ``` json
    {
      "type": "Polygon",
      "coordinates": [
          [[-112.485, 34.529], [-112.445, 34.529], [-112.445, 34.559], [-112.485, 34.559], [-112.485, 34.529]]
        ]
    }
    ```

    A `Polygon` has at least three sets of coordinate pairs which close the shape.

#### :material-map-marker-multiple: MultiPoint

??? Info ":material-code-json: GeoJSON MultiPoint Schema"

    ``` json
    {
      "type": "MultiPoint",
      "coordinates": [
          [-112.4470, 34.5510],
          [-112.4695,  34.541] 
        ]
    }
    ```

    A `MultiPoint` geometry is represented by multiple coordinate point pairs

#### :material-vector-polyline::material-vector-line: MultiLineString

??? Info ":material-code-json: GeoJSON MultiLineString Schema"

    ``` json
    {
      "type": "MultiLineString",
      "coordinates": [
          [[-112.44708, 34.5510], [-112.46953, 34.540924]], 
          [[-112.4471, 34.5510], [-112.4541,34.54447], [-112.46953, 34.540924]]
        ]    
    }
    ```

    A `MultiLineString` uses multiple lines which are not connected.

#### :material-vector-combine: MultiPolygon

??? Info ":material-code-json: GeoJSON MultiPolygon Schema"

    ``` json
    {
      "type": "MultiPolygon",
      "coordinates": [
        [
          [[-112.0, 35.0], [-112.0, 34.0],  [-113.0, 34.0],  [-113.0, 35.0],  [-112.0, 35.0]]
        ],
        [
          [[-112.50, 35.50], [-112.50, 34.50], [-113.50, 34.50],  [-113.50, 35.50], [-112.50, 35.50]]
        ],
        [
          [[-111.50, 34.50], [-111.50, 33.50], [-112.50, 33.50],  [-112.50, 34.50], [-111.50, 34.50]]
        ]
      ]
    }
    ```

    A `MultiPolygon` uses multiple lines to provide more than one set of polygons.

#### :material-layers-triple-outline: GeometryCollection

??? Info ":material-code-json: GeoJSON GeometryCollection"

    ``` json
    {
      "type": "GeometryCollection",
      "geometries": [{
          "type": "Point",
          "coordinates": [-112.4471, 34.5510]
      }, {
          "type": "LineString",
          "coordinates": [
              [-112.4470, 34.5510], [-112.4695,  34.541]  
            ]
      }]
    }
    ```

    The `GeometryCollection` introduces a new set of braces `{}` which separate different geometries.

### :material-layers-outline: Feature

??? Info ":material-code-json: GeoJSON Feature"

    ``` json
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [-112.4470, 34.5510]
      },
      "properties": {
        "name": "AGIC Venue"
      }
    }
    ```

    A `Feature` provides a new set of `properties:` which allow metadata and annotation of the geometry.

### :material-layers-triple-outline: FeatureCollection

??? Info ":material-code-json: GeoJSON FeatureCollection Point"

    ``` json
    {
      "type": "FeatureCollection",
      "features": [
        {
          "type": "Feature",
          "properties": {
            "Location Name" : "Prescott Resort and Conference Center"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [
              -112.44677424430846,
              34.55109119815299
            ]
          }
        }
      ]
    }
    ```

    A full `FeatureCollection` provides us with the ability to create multiple `Features`

??? Info ":material-code-json: GeoJSON FeatureCollection with multiple attributes"

    ``` json
    {
      "type": "FeatureCollection",
      "features": [
        {
          "type": "Feature",
          "properties": {},
          "geometry": {
            "type": "LineString",
            "coordinates": [
              [
                -112.44717121124268,
                34.551069106918945
              ],
              [
                -112.45414495468138,
                34.54447682068866
              ],
              [
                -112.46953010559082,
                34.540924192549795
              ]
            ]
          }
        },
        {
          "type": "Feature",
          "properties": {},
          "geometry": {
            "type": "Point",
            "coordinates": [
              -112.44691371917723,
              34.551210490715455
            ]
          }
        }
      ]
    }
    ```

## Related JSON types

### TopoJSON

[TopoJSON](https://github.com/topojson/topojson){target=_blank} is an extension of GeoJSON that encodes topology and is more efficient than GeoJSON.

TopoJSON use "arcs" as a way of connecting coordinate pairs, reducing the size of the file, removing duplicate coordinates, and improving performance in the browser.

??? Info "TopoJSON Schema"
  
    ``` json
    {
      "type": "Topology",
      "objects": 
      {
        "collection": 
        {
          "type": "Polygon",
          "arcs":[[0]]
        }
      },
      "arcs": [[[0,0],[9999,0],[0,9999],[-9999,0],[0,-9999]]],
      "transform":
      {
        "scale":[0.000004000400040004626,0.0000030003000300024037],
        "translate": [-112.485,34.529]
      },
      "bbox":[-112.485,34.529,-112.445,34.559]
    }
    ```

### Newline-delimited GeoJSON

[Newline Delimited GeoJSON](https://stevage.github.io/ndgeojson/){target=_blank} is particularly convenient for transformation and processing. Each line can be read independently, parsed, and processed, without the entire file ever having to be parsed in memory, which is great for huge files.

NLD GeoJSON remove "FeatureCollection"

??? Info "NLD GeoJSON Schema"

    ``` json
    {"type":"Feature","properties":{},"geometry":{"type":"Point","coordinates":[-112.44691371917723,34.551210490715455]}}
    {"type":"Feature","properties":{},"geometry":{"type":"LineString","coordinates":[[-112.4470,34.5510],[-112.4695,34.541]]}}
    {"type":"Feature","properties":{},"geometry":{"type":"Polygon","coordinates":[[[-112.485,34.529],[-112.445,34.529],[-112.445,34.559],[-112.485,34.559],[-112.485,34.529]]]}}
    ```

## GeoJSON Webpages

[geojson.io](https://geojson.io/){target=_blank} - create, view, edit GeoJSON in your browser

[python-geojson](https://python-geojson.readthedocs.io/en/latest/){target=_blank}

[GeoJSON in ArcGIS Online](https://doc.arcgis.com/en/arcgis-online/reference/geojson.htm){target=_blank}

[GeoJSON in BigQuery](https://cloud.google.com/blog/topics/developers-practitioners/using-geojson-bigquery-geospatial-analytics){target=_blank}

[JSON Formatter Chrome Plugin](https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa?hl=en){target=_blank}

[shp2json](https://github.com/mbostock/shapefile){target=_blank} cross-platform streaming parser for the ESRI Shapefile spatial data format.

??? Question "Is GeoJSON really 'cloud native'?"

    Not really. NLD GeoJSON is closer to being cloud-native format than GeoJSON, but both have their short-comings.
    
    The ubiquity of JSON on web and its recommended use in cloud-native formats is why we're teaching it. You'll learn in the later sections GeoJSON is the most common vector for querying cloud optimized data formats. 

    [Chris Holmes recent Blog Post on 'Cloud Native Vectors'](https://cholmes.medium.com/an-overview-of-cloud-native-vector-c223845638e0){target=_blank}

    [Chris Holmes older blog post on 'Towards a Cloud-Native Geospatial standards baseline'](https://www.ogc.org/blog/4609){target=_blank}

# Hands-On

## **Step 1** Go to [GeoJSON.io](https://geojson.io/#)

Play around creating different GeoJSON Geometries and Feature Collections

* Zoom into an area of interest (suggest selecting the geographic area around Prescott, AZ)

<figure markdown>
  <a href="https://geojson.io" target="blank" rel="geojson.io">![geojson.io](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geojsonio_1.png){ width="700" } </a>
    <figcaption>[GeoJSON.io](https://geojson.io){target=_blank} features a map with either OpenStreetMap or Satellite Base Layer (left), and an example GeoJSON (right) that can be edited & copy/pasted.</figcaption>
</figure>

* Practice creating points, lines, polygon, and a multi-polygons.

<figure markdown>
  <a href="https://geojson.io" target="blank" rel="geojson.io">![geojson.io](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geojsonio_2.png){ width="700" } </a>
    <figcaption>A Polygon Feature Collection</figcaption>
</figure>

* Add additional metadata to the "properties"

<figure markdown>
  <a href="https://geojson.io" target="blank" rel="geojson.io">![geojson.io](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geojsonio_3.png){ width="700" } </a>
    <figcaption> Create new metadata </figcaption>
</figure>

In the `"properties" : {}` field, add additional metadata:

``` json
"type": "Feature",
      "properties": {
        "city name" : "Prescott",
        "state" : "Arizona"
      },
```

!!! Note ":material-code-json: JSON formatting"

    JSON is very specific when it comes to line spacing, braces `{}`, quotations `""` for strings, and commas `,` at the end of a line inside a feature.

    * Try to use a text editor with JSON formatting turned on, this will help you to debug hand-written or edited JSON and GeoJSON files that have errors.

    * Spaces between the colons `:` are optional but may help improve readability.

    * When you add more than one new line, you must use a comma at the end. 

## **Step 2** Export a GeoJSON 

* Click on "Save" on the GeoJSON.io website

* Select the `GeoJSON` Format option.

* Download to your local computer in an easy to relocate folder

<figure markdown>
  <a href="https://geojson.io" target="blank" rel="geojson.io">![geojson.io](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/geojsonio_4.png){ width="700" } </a>
    <figcaption> Create new metadata </figcaption>
</figure>

## **Step 3** Option 1: Open the GeoJSON in QGIS

* Open QGIS

* In the "Layers" then "Add Layer" and then "Add Vector Layer" 

* Choose the "**Source Type** and select "File" for a file on your computer

* Navigate to your downloads folder and select a downloaded `.geojson` in the "**Source**" "*Vector Dataset(s)*" field.

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_geojson_1.png" target="blank" rel="qgis_geojson_1">![qgis_geojson_1](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_geojson_1.png){ width="700" } </a>
    <figcaption> Loading a Layer Vector from the localhost in QGIS Layers</figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_geojson_2.png" target="blank" rel="qgis_geojson_2">![qgis_geojson_2](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_geojson_2.png){ width="700" } </a>
    <figcaption> You can select which feature collection you want to load
</figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_geojson_3.png" target="blank" rel="qgis_geojson_3">![qgis_geojson_3](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_geojson_3.png){ width="700" } </a>
    <figcaption> After the GeoJSON is loaded you can view it in the display</figcaption>
</figure>

### Loading GeoJSON from HTTP(S)

GeoJSON can be read directly from the web, without downloading them.

Here we're going to use the [USGS 3DEP lidar boundaries](https://github.com/hobuinc/usgs-lidar/blob/master/boundaries/resources.geojson){target=_blank} layer which is hosted on GitHub:

https://github.com/hobuinc/usgs-lidar/raw/master/boundaries/resources.geojson 

??? Tip "Using GitHub to view GeoJSON"

    Note how [`resources.geojson`](https://github.com/hobuinc/usgs-lidar/blob/master/boundaries/resources.geojson){target=_blank} is visible as a leaflet map directly in GitHub.

    GeJSON can also be visualized in [VS Code and Jupyter Lab](#open-the-geojson-in-an-ide-like-vs-code-or-jupyter) the same way using map extensions for Folium and Leaflet.

<figure markdown>
  <a href="https://github.com/hobuinc/usgs-lidar/raw/master/boundaries/resources.geojson" target="blank" rel="qgis_3dep_1">![qgis_3dep_1](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_3dep_1.png){ width="700" } </a>
    <figcaption> Loading a Layer Vector from an HTTP(s) in QGIS Layers</figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/hobuinc/usgs-lidar/raw/master/boundaries/resources.geojson" target="blank" rel="qgis_3dep_2">![qgis_3dep_2](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_3dep_2.png){ width="700" } </a>
    <figcaption> QGIS can open the GeoJSON without downloading first. </figcaption>
</figure>


??? Tip "Troubleshooting import HTTPS GeoJSON layers in QGIS"

      **Change The Environmental Setting Variables In QGIS**
      
      1. Go to **Setting Menu** >> **Options**

        In the **Options** window:

          Go to **System**

      2. Expand **Environment**: 
        
        Check the box to Use custom vairables

      3. Then add the following variables

          variable 1: `GDAL_HTTP_USERAGENT`

          variable value 1: `Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2228.0 Safari/537.36`

          variable 2: `GDAL_HTTP_UNSAFESSL`

          variable value 2: `YES`

      4. Restart QGIS and them try to add the GeoJSON file link again.


## **Step 3** Option 2: Open the GeoJSON in ArcGIS Online

Log into ArcGIS Online and select the MapViewer

https://ua-gisug.maps.arcgis.com/apps/mapviewer/index.html

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/arcgis_3dep_1.png" target="blank" rel="arcgis_3dep_2">![arcgis_3dep_2](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/arcgis_3dep_1.png){ width="700" } </a>
    <figcaption> ArcGIS Online can load GeoJSONs from an HTTP(s) </figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/arcgis_3dep_2.png" target="blank" rel="arcgis_3dep_2">![arcgis_3dep_2](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/arcgis_3dep_2.png){ width="700" } </a>
    <figcaption> The same USGS 3DEP Boundaries in ArcGIS Online Map Viewer</figcaption>
</figure>

### Open the GeoJSON in an IDE (like VS Code or Jupyter)

VS Code can be used to view and edit JSON and GeoJSON

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/vscode_geojson_1.png" target="blank" rel="vscode_geojson_1">![vscode_geojson_1](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/vscode_geojson_1.png){ width="700" } </a>
    <figcaption> VS Code can be used to view and edit JSON and GeoJSON</figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/vscode_geojson_2.png" target="blank" rel="vscode_geojson_2">![vscode_geojson_2](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/vscode_geojson_2.png){ width="700" } </a>
    <figcaption> VS Code Extensions can be used to render the GeoJSON</figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/vscode_geojson_3.png" target="blank" rel="vscode_geojson_3">![vscode_geojson_3](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/vscode_geojson_3.png){ width="700" } </a>
    <figcaption> There are a variety of extensions for both GeoJSON and Leaflet</figcaption>
</figure>

## Step 4 (Optional): Convert a SHP file to GeoJSON

QGIS can export `.shp` as `.geojson` directly.

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_export_1.png" target="blank" rel="qgis_export_1">![qgis_export_1](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_export_1.png){ width="700" } </a>
    <figcaption> "Export" and "Save Feature As"</figcaption>
</figure>

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_export_2.png" target="blank" rel="qgis_export_2">![qgis_export_2](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/qgis_export_2.png){ width="700" } </a>
    <figcaption> If you plan to use your `.geojson` in a web map, set the CRS to `EPSG:4326 - WGS84` and the `COORDINATE_PRECISION` down to 4-6 decimals (<1-4 ft GSD).
</figcaption>
</figure>

# Additional Reading

[Applied Use of JSON, GeoJSON, JSON-LD, SPARQL, and IPython Notebooks for Representing and Interacting with Small Datasets - by Sebastian Heath](http://dlib.nyu.edu/awdl/isaw/isaw-papers/20-13/){target=_blank}