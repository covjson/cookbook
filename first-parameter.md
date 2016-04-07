# Step 2: Temperature Parameter

Describing what our data values represent is fairly simple in CoverageJSON and is done with a *Parameter*:
```js
{
  "type" : "Parameter",
  "unit" : {
    "symbol" : "°C"
  },
  "observedProperty" : {
    "label" : {
      "en": "Air temperature"
    }
  }
}
```
There are two information in here:
- `unit.symbol` is an informal textual notation of the units of measurement, here degrees Celsius.
- `observedProperty` describes the abstract concept that is measured or modelled, independent of what units are used.

If data values have no units, then `unit` would be omitted. `observedProperty.label` however is always required.

While the above is enough for humans to get a basic understanding, CoverageJSON allows to describe a parameter in more detail, partially to make it easier for machines to identify related datasets and also to compare them with each other:
```js
{
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
      "en": "Air temperature"
    },
    "description": {
      "en": "Air temperature is the bulk temperature of the air, not the surface (skin) temperature."
    }
  }
}
```
There are two additions in there which are specifically meant for machines:
- Units are now expressed using a standardised syntax scheme, in this case the [Unified Code for Units of Measure](http://unitsofmeasure.org/ucum.html) (UCUM). The scheme is referenced by its global identifier http://www.opengis.net/def/uom/UCUM/. Machines are now able to understand the units and do transformations on them.
- The observed property now references a global identifier that uniquely identifies the concept and lets machines match it up with other datasets.

It is important to note that the `observedProperty` is typically reused across many datasets, while the rest of the parameter is often customized for a given dataset. This is why a parameter itself often does not have a global identifier.

Next stop, data values!
