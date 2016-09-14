{% from "macros.md" import playgroundLink, exampleCode %}

# Step 4: Putting it Together

![Visualization of finished Coverage](images/playground_temperature_coverage.png)

Assembling the individual parts to a CoverageJSON Coverage is very straight-forward:
```js
{
  "type" : "Coverage",
  "domain" : {
    "type" : "Domain",
    "domainType" : "Grid",
    "axes": {
      "x" : { "start": 7, "stop": 14, "num": 4 },
      "y" : { "start": 54, "stop": 48, "num": 4 }
    },
    "referencing": [{
      "coordinates": ["x","y"],
      "system": {
        "type": "GeographicCRS",
        "id": "http://www.opengis.net/def/crs/OGC/1.3/CRS84"
      }
    }]
  },
  "parameters" : {
    "temperature": {
      "type" : "Parameter",
      "description": {
        "en": "Air temperature measured in degrees Celsius."
      },
      "unit" : {
        "label": {
          "en": "Degree Celsius"
        },
        "symbol": {
          "value": "Cel",
          "type": "http://www.opengis.net/def/uom/UCUM/"
        }
      },
      "observedProperty" : {
        "id": "http://vocab.nerc.ac.uk/standard_name/air_temperature/",
        "label" : {
          "en": "Air temperature",
          "de": "Lufttemperatur"
        },
        "description": {
          "en": "Air temperature is the bulk temperature of the air, not the surface (skin) temperature."
        }
      }
    }
  },
  "ranges" : {
    "temperature" : {
      "type" : "NdArray",
      "dataType": "float",
      "axisNames": ["y", "x"],
      "shape": [4, 4],
      "values" : [
        17.3, 18.2, 16.5, 18.7,
        18.1, 19.4, 17.2, 18.6,
        19.2, 20.4, 21.1, 20.7,
        21.1, 21.3, 20.5, 19.2
      ]
    }
  }
}
```
{{ playgroundLink('coverages/grid.covjson') }}

This is what happened:

- Since a Coverage can contain multiple parameters, we had to invent a short unique name for our single air temperature parameter, here `temperature`.

And we're done! There is a lot more to explore, however, for the time being just head over to the playground and try to experiment a bit by changing the values and see what happens.
