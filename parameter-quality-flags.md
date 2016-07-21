{% from "macros.md" import playgroundLink %}

# Quality Flags

Quality flags in CovJSON are represented with a categorical parameter. In this example we use the [Argo quality flags](http://mmisw.org/ont/argo/qualityFlag):

URI                                        | Description
-------------------------------------------|---------------------------------
<http://mmisw.org/ont/argo/qualityFlag/_0> | No quality control was performed
<http://mmisw.org/ont/argo/qualityFlag/_1> | QC was performed good data
<http://mmisw.org/ont/argo/qualityFlag/_2> | Probably good data but value may be inconsistent with statistics (differ from climatology)
<http://mmisw.org/ont/argo/qualityFlag/_3> | Probably bad data (spike-gradient- if other tests passed)
<http://mmisw.org/ont/argo/qualityFlag/_4> | Bad data
<http://mmisw.org/ont/argo/qualityFlag/_5> | Value modified during quality control
<http://mmisw.org/ont/argo/qualityFlag/_8> | Interpolated value
<http://mmisw.org/ont/argo/qualityFlag/_9> | Missing value

The corresponding categorical parameter then looks like that:
```js
{
  "type" : "Parameter",
  "observedProperty" : {
    "id": "http://mmisw.org/ont/argo/qualityFlag",
    "label" : {
      "en": "Argo Quality Control Flag"
    },
    "categories": [{
      "id": "http://mmisw.org/ont/argo/qualityFlag/_0",
      "label": {
        "en": "No QC was performed"
      },
      "description": {
        "en": "No quality control was performed"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_1",
      "label": {
        "en": "Good data"
      },
      "description": {
        "en": "QC was performed good data"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_2",
      "label": {
        "en": "Probably good data"
      },
      "description": {
        "en": "Probably good data but value may be inconsistent with statistics (differ from climatology)"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_3",
      "label": {
        "en": "Probably bad data"
      },
      "description": {
        "en": "Probably bad data (spike-gradient- if other tests passed)"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_4",
      "label": {
        "en": "Bad data"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_5",
      "label": {
        "en": "Value modified"
      },
      "description": {
        "en": "Value modified during quality control"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_8",
      "label": {
        "en": "Interpolated value"
      }
    }, {
      "id": "http://mmisw.org/ont/argo/qualityFlag/_9",
      "label": {
        "en": "Missing value"
      }
    }]
  },
  "categoryEncoding": {
    "http://mmisw.org/ont/argo/qualityFlag/_0": 0,
    "http://mmisw.org/ont/argo/qualityFlag/_1": 1,
    "http://mmisw.org/ont/argo/qualityFlag/_2": 2,
    "http://mmisw.org/ont/argo/qualityFlag/_3": 3,
    "http://mmisw.org/ont/argo/qualityFlag/_4": 4,
    "http://mmisw.org/ont/argo/qualityFlag/_5": 5,
    "http://mmisw.org/ont/argo/qualityFlag/_8": 8,
    "http://mmisw.org/ont/argo/qualityFlag/_9": 9
  }
}
```
{{ playgroundLink('coverages/point-argo-quality-flags.covjson', title='Open in Playground (Point coverage)') }}

Notes:
- We added our own short labels for each category to make visualization in clients more convenient.
- The "Missing value" category is not strictly necessary in CovJSON as this is also represented by `null` in range values.
  If however there would be specific distinguished reasons for a missing value (e.g. instrument failure, data corruption) then
  such categories are indeed useful.
- Since there are official URIs for all the Argo quality flags the above translation was straightforward.
  If this was not the case then such URIs should be created first. Otherwise, a simple arbitrary string may be used for `"id"` as well, e.g. `"bad"` and `"good"`. The advantage of using URIs is that clients have a better chance of understanding and working with the flags. The data becomes more interoperable.
