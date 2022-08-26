# :material-code-json: GeoJSON (Geo+JSON)

[JavaScript Object Notation (JSON)](https://www.json.org/json-en.html){target=_blank} is a lightweight, text-based, language-independent data interchange format. 

* [JSON syntax](https://www.w3schools.com/js/js_json_syntax.asp){target=_blank}
* [rfc7159](https://datatracker.ietf.org/doc/html/rfc7159){target=_blank}

??? Info "an example JSON Schema for a geospatial object"
  
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
    
    **data**
    
    ``` json
    {
      "latitude": 34.5510,
      "longitude": -112.4471
    }
    ```

[GeoJSON](https://geojson.org/){target=_blank} is a format for encoding a variety of geographic data structures.

* [geojson.org](https://geojson.org){target=_blank}
* [rfc7946](https://datatracker.ietf.org/doc/html/rfc7946){target=_blank}

A GeoJSON Object may represent a region of space: a **Geometry**, a **Feature**, or a list of Features called a **FeatureCollection**.

### :material-angle-acute: Geometry

There are seven types of geometric shapes which can be defined in GeoJSON.

* Point, LineString and Polygon are *single type geometry objects* 
* MultiPoint, MultiLineString, and MultiPolygon are *multipart geometry objects*

Each of the examples below represents a valid and complete GeoJSON object:

#### :material-map-marker: Point

A Point geometry is represented by a single set of latitude and a longitude coordinates, and optionally an elevation value (above mean sea level).  

??? Info ":material-code-json: GeoJSON Point Schema"

    ``` json
    { 
      "type": "Point",
      "coordinates": [-112.4471, 34.5510]
    }
    ```

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


#### :material-map-marker-multiple: MultiPoint

A MultiPoint geometry is represented by multiple coordinates

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

### :material-layers-triple-outline: FeatureCollection

??? Info ":material-code-json: GeoJSON FeatureCollection"

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

# GeoJSON Webpages

[geojson.io](https://geojson.io/){target=_blank} - create, view, edit GeoJSON in your browser

[python-geojson](https://python-geojson.readthedocs.io/en/latest/){target=_blank}

[GeoJSON in ArcGIS Online](https://doc.arcgis.com/en/arcgis-online/reference/geojson.htm)

[GeoJSON in BigQuery](https://cloud.google.com/blog/topics/developers-practitioners/using-geojson-bigquery-geospatial-analytics){target=_blank}

[JSON Formatter Chrome Plugin](https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa?hl=en){target=_blank}

[shp2json](https://github.com/mbostock/shapefile) cross-platform streaming parser for the ESRI Shapefile spatial data format.

??? Question "Is GeoJSON really 'cloud native'?"

    Not really. 
    
    But the ubiquitous of JSON and its recommended use in cloud requires this fundamental primer.

    [Chris Holmes recent Blog Post on 'Cloud Native Vectors'](https://cholmes.medium.com/an-overview-of-cloud-native-vector-c223845638e0){target=_blank}

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
