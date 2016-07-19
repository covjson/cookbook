# Custom Fields

Custom fields are typically used to add information that it is not (yet) covered by the CoverageJSON specification.
An example would be to add fields for the publisher, license, and publication date.

If you don't care much about interoperability or field name clashes with future versions of the format,
then the easiest way is to just add custom fields as you would normally do to the JSON document.
This is fine if you don't intend to share your data more widely and you have control over all clients that make use of the data.

In the following we focus on how to add custom fields in a future-proof and interoperable way.
The first thing to do is to use field names of the form `"prefix:suffix"`.
The CoverageJSON specification will never define a field name with a colon, effectively avoiding name collisions with extensions as the format evolves.

Example of adding a custom field:
```js
{
  "type" : "Coverage",
  "dct:license": "https://creativecommons.org/licenses/by/4.0/",
  ...
}
```

In order to establish a common understanding of extensions and to be able to easily combine them in one document, prefixes should be registered.
Registration is not bound to any restrictions or obligations. The site <https://covjson.org/prefixes/> shows already registered prefixes and has instructions on how to add a new one (which amounts to a simple GitHub pull request).

If you're into linked data and RDF, then consider having a look at the [JSON-LD section](http://covjson.org/spec/#json-ld) of the spec. 

