# Sea Ice Area Fraction

In this example we will see how a fraction can be represented in CovJSON. For that we use the sea ice area fraction.

Fractions in CovJSON are stored as a decimal number which is typically between 0 and 1. Percentages are fractions comparing a number to 100, which means they simply have a unit of `1/100`, which is often symbolized with the percentage sign `%`. Depending on how data values are stored, those two cases have to be distinguished.

First, we look at the case where the sea ice area fraction is stored as a decimal between 0 and 1:
```js
{
  "type" : "Parameter",
  "unit" : {
    "label": {
      "en": "Ratio"
    },
    "symbol": {
      "value": "1",
      "type": "http://www.opengis.net/def/uom/UCUM/"
    }
  },
  "observedProperty" : {
    "id" : "http://vocab.nerc.ac.uk/standard_name/sea_ice_area_fraction/",
    "label" : {
      "en": "Sea ice area fraction"
    },
    "description": {
      "en": "Sea ice area fraction is the area of the sea surface occupied by sea ice. It is also called 'sea ice concentration'."
    }
  }
}
```

When the fraction is stored as a percentage, the unit has to be changed:
```js
{
  "type" : "Parameter",
  "unit" : {
    "label": {
      "en": "Percent"
    },
    "symbol": {
      "value": "%",
      "type": "http://www.opengis.net/def/uom/UCUM/"
    }
  },
  "observedProperty" : {
    "id" : "http://vocab.nerc.ac.uk/standard_name/sea_ice_area_fraction/",
    "label" : {
      "en": "Sea ice area fraction"
    },
    "description": {
      "en": "Sea ice area fraction is the area of the sea surface occupied by sea ice. It is also called 'sea ice concentration'."
    }
  }
}
```
An equivalent to `"%"` for `unit.symbol.value` is `"1/100"`, both represent the same unit. However, for the sake of easier processing and increased readability the percentage sign should be used in that case. 
