# Custom Types

CoverageJSON has several extension points where it allows you to use a custom *type* of something.
In the following we walk through each of those extension points using simple examples.
At the end you should feel comfortable inventing your own types.

As for custom fields (see previous page), if you don't care much about interoperability or type name clashes with future versions of the format, then the easiest way to use custom types is to use a new simple name (e.g. replacing `"Grid"` by `"MyGrid"`).
This is fine if you don't intend to share your data more widely and you have control over all clients that make use of the data.

In the following we focus on how to use custom types in a future-proof and interoperable way.
This is done by using type names of the form `"prefix:suffix"` (a compact URI) or as absolute URIs.
The CoverageJSON specification will never define a type with `"prefix:suffix"` form, and only uses absolute URIs if the URI is normative, therefore avoiding any conflicts with extensions as the format evolves.

In order to establish a common understanding of extensions and to be able to easily combine them in one document, prefixes should be registered.
Registration is not bound to any restrictions or obligations. The site <https://covjson.org/prefixes/> shows already registered prefixes and has instructions on how to add a new one (which amounts to a simple GitHub pull request).

If you're into linked data and RDF, then consider having a look at the [JSON-LD section](https://covjson.org/spec/#json-ld) of the spec. 

## Custom domain type

CoverageJSON has several [domain types](https://covjson.org/domain-types/) already built-in, for example, Grid, Trajectory, and VerticalProfile.
If those types don't match your data, then you have two choices: either omit the `"domainType"` field, or invent a custom domain type. A custom domain type has the advantage that it associates a named concept to the implicit domain structure and its constraints. Sometimes it may also be used to establish additional semantics to it which clients then can make use of, for example to apply more specific visualization.

Example:

```json
{
  "type": "Domain",
  "domainType": "ex:Transect",
  "axes": {
    "composite": {
      "dataType": "tuple",
      "coordinates": ["x","y","z"],      
      "values": [
        [1.112, 20.001, 0.35],
        [1.113, 20.002, 0.45],
        [1.114, 20.003, 0.55]
      ]
    }
  },
  "referencing": [{
    "coordinates": ["y","x","z"],
    "system": {
      "type": "GeodeticCRS",
      "id": "http://www.opengis.net/def/crs/EPSG/0/4979"        
    }
  }]
}
```

Instead of the compact URI `ex:Transect` we could also have used an absolute URI, like `http://example.com/covjson-Transect`. This can make sense if there is no namespace as such and the concept is not part of a set of concepts. Publishers should decide for one variant and then stick to it - this makes client development easier.

## Custom axis value data type

CoverageJSON has support for three types of axis values: primitive (number or string), tuple (array of primitives), and polygon (the "coordinates" part of a GeoJSON Polygon). Those types should cover the majority of use cases, so before inventing your own type, make sure that the existing ones are really not suitable.

Example:

```json
{
  "type": "Domain",
  "axes": {
    "composite": {
      "dataType": "ex:multiPolygon",
      "coordinates": ["x","y"],
      "values": [
        [
          [[[102.0, 2.0], [103.0, 2.0], [103.0, 3.0], [102.0, 3.0], [102.0, 2.0]]],
          [[[100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0]],
           [[100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2]]]
        ]
      ]
    }
  },
  "referencing": [{
    "coordinates": ["x","y"],
    "system": {
      "type": "GeodeticCRS",
      "id": "http://www.opengis.net/def/crs/OGC/1.3/CRS84"
    }
  }]
}
```

Here, `ex:multiPolygon` defines that each axis value is a GeoJSON MultiPolygon (the `"coordinates"` field of it).
Instead of the compact URI `ex:multiPolygon` we could also have used an absolute URI, like `http://example.com/covjson-multiPolygon`. This can make sense if there is no namespace as such and the concept is not part of a set of concepts. Publishers should decide for one variant and then stick to it - this makes client development easier.

## Custom reference system type

CoverageJSON supports several common reference system types: spatial (geodetic, projected, vertical), temporal, and identifier-based. A custom type is typically accompanied by custom fields as well.

Example:

```json
{
  "type": "Domain",
  "axes": {
    "hp": { "start": 0, "stop": 99, "num": 100 }
  },
  "referencing": [{
    "coordinates": ["hp"],
    "system": {
      "type": "ex:HEALPixRS",
      "ex:h": 3,
      "ex:k": 3,
      "ex:ordering": "nested"
    }
  }]
}
```

In the example above, `ex:HEALPixRS` refers to [HEALPix](http://healpix.jpl.nasa.gov/) which is a type of [geodesic discrete global grid system](https://en.wikipedia.org/wiki/Discrete_Global_Grid) (sometimes just called geodesic grid). Different to longitude/latitude or projected systems, grid cell indexing works in a 1D space. Also note that three additional custom fields are used to fully define the reference system.

Instead of the compact URI `ex:HEALPixRS` we could also have used an absolute URI, like `http://example.com/healpix`. This can make sense if there is no namespace as such and the concept is not part of a set of concepts. Publishers should decide for one variant and then stick to it - this makes client development easier.

## Custom unit symbol type

CoverageJSON defines how to use [UCUM](http://unitsofmeasure.org/ucum.html) as a unit coding scheme. Sometimes, different systems are needed though.

Example:

```json
{
  "type" : "Parameter",
  "unit" : {
    "label": {
      "en": "Degree Celsius"
    },
    "symbol": {
      "value": "degreeC",
      "type": "ex:UDUNITS"
    }
  },
  "observedProperty" : {
    "label" : {
      "en": "Air temperature",
    }
  }
}
```

Here, `ex:UDUNITS` refers to the coding scheme of the [UDUNITS](http://www.unidata.ucar.edu/software/udunits/) software package. This scheme is also the official one used by the popular [CF Conventions](http://cfconventions.org/).

Instead of the compact URI `ex:UDUNITS` we could also have used an absolute URI, like `http://example.com/udunits`. This can make sense if there is no namespace as such and the concept is not part of a set of concepts. Publishers should decide for one variant and then stick to it - this makes client development easier.

## Custom range type (or: Custom type in custom fields)

CoverageJSON enforces a canonical JSON encoding of range data in the `"ranges"` field which generic implementations support. Alternative range encodings can be added under the `"rangeAlternates"` field. Whether the canonical JSON range data (in this case typically linked from within the `"ranges"` field) is omitted or not depends on the specific use case and has to be carefully evaluated.

Example:

```json
{
  "type" : "Coverage",
  "domain" : { ... },
  "parameters" : { ... },
  "ranges" : {
    "temperature" : "http://example.com/temperature.covjson"
  },
  "rangeAlternates": {
    "ex:dap2": {
      "temperature": {
        "type": "ex:DAP2NdArray",
        "dataType": "float",
        "axisNames": ["y","x"],
        "shape": [180, 360],
        "ex:offset": 40,
        "ex:factor": 100,
        "ex:missingValue": 999,
        "urlTemplate": "http://my.opendap.server/data.dods?air_temp{y}{x}"
      }
    },
    "ex:tiff": {
      "temperature": {
        "type": "ex:TIFF2DArray",
        "dataType": "float",
        "axisNames": ["y","x"],
        "shape": [180, 360],
        "ex:channel": 0,
        "ex:url": "http://example.com/data.tiff"
      }
    }
  }
}
```

In the example above, two alternative range encodings are provided, one based on a [DAP 2](http://opendap.org/documentation) endpoint, the other on TIFF images.
The `ex:dap` and `ex:tiff` fields provide a convenient entry point to the alternative encodings. Within those custom fields, the `ex:DAP2NdArray` and `ex:TIFF2DArray` types define the actual range type, of which there may be more than one for a given entry point (similar to the built-in `NdArray` and `TiledNdArray` types).

Instead of the compact URIs `ex:DAP2NdArray` and `ex:TIFF2DArray` we could also have used absolute URIs, like `http://example.com/covjson-DAP2NdArray`. This can make sense if there is no namespace as such and the concept is not part of a set of concepts. Publishers should decide for one variant and then stick to it - this makes client development easier. In the examples above, compact URIs make more sense though, as there are custom fields which likely would belong to the same namespace.
