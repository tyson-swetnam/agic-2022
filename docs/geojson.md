# GeoJSON (Geo+JSON)

[JavaScript Object Notation (JSON)](https://www.json.org/json-en.html){target=_blank} is a lightweight, text-based, language-independent data interchange format. 

* [JSON syntax](https://www.w3schools.com/js/js_json_syntax.asp){target=_blank}
* [rfc7159](https://datatracker.ietf.org/doc/html/rfc7159){target=_blank}

??? Info "JSON Schema"
  
    ```
    {
      "$id": "https://example.com/geographical-location.schema.json",
      "$schema": "https://json-schema.org/draft/2020-12/schema",
      "title": "Longitude and Latitude Values",
      "description": "A geographical coordinate.",
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
    
    Data
    
    ```
    {
      "latitude": 34.550,
      "longitude": -112.447
    }
    ```

[GeoJSON](https://geojson.org/){target=_blank} is a format for encoding a variety of geographic data structures.

* [geojson.io](https://geojson.io){target=_blank}
* [rfc7946](https://datatracker.ietf.org/doc/html/rfc7946){target=_blank}

??? Info "GeoJSON Schema"
  
    Point
    
    ```
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [-112.447, 34.550]
      },
      "properties": {
        "name": "Prescott Arizona"
      }
    }
    ```
  
    Line
    
    ```
    
    ```
    
    Polygon
    
    ```
    
    
    ```
    

[TopoJSON](https://github.com/topojson/topojson){target=_blank} is an extension of GeoJSON that encodes topology and is more efficient than GeoJSON.

??? Info "TopoJSON Schema"
  
    ```
    
    ```
