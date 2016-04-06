{% from "macros.md" import playgroundLink, exampleCode %}

# Step 1: Spatial Domain

```js
{
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
}
```

{{ playgroundLink('domains/grid.covjson') }}