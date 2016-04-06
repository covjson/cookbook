{% from "macros.md" import playgroundLink, exampleCode %}

# Step 4: Putting it Together

```js
{
  "type" : "Coverage",
  "profile" : "GridCoverage",
  "domain" : {
    "type" : "Domain",
    "profile" : "Grid",
    "axes": {
      "x" : { "start": 7, "stop": 14, "num": 4 },
      "y" : { "start": 54, "stop": 48, "num": 4 }
    },
    "rangeAxisOrder": ["y","x"],
    "referencing": [{
      "components": ["x","y"],
      "system": {
        "type": "GeodeticCRS",
        "id": "http://www.opengis.net/def/crs/OGC/1.3/CRS84"
      }
    }]
  },
  "parameters" : {
    "TEMP": {
      "type" : "Parameter",
      "unit" : {
        "symbol" : "°C"
      },
      "observedProperty" : {
        "label" : {
          "en": "Temperature"
        }
      }
    }
  },
  "ranges" : {
    "TEMP" : {
      "type" : "Range",
      "dataType": "float",
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
