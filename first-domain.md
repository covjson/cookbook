{% from "macros.md" import playgroundLink %}

# Step 1: Spatial Domain

```js
{
  "type" : "Domain",
  "profile" : "Grid",
  "axes": {
    "x" : { "values": [-10,-5,0] },
    "y" : { "values": [40,50] }
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