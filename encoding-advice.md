# Encoding Advice

The following is a list of advices that should be followed when creating CoverageJSON documents in order to minimize storage and network data volume, reduce client-side parsing time, and increase human-readability.

## Enable gzip

If your server supports it, enable gzip for serving CoverageJSON documents.
Especially for range data arrays this can dramatically reduce the resulting data volume and will lead to much lower loading times in clients.

## Serve pre-gzipped static files

If your CoverageJSON documents are not dynamically generated but instead stored on a static server, then, if your server supports that, consider transparently serving pre-gzipped files to reduce both server storage and processing power. As an example, in [nginx](http://nginx.org/), this can be done with the [gzip_static](http://nginx.org/en/docs/http/ngx_http_gzip_static_module.html) module.  

## Indent and order

Although indentation and field ordering is irrelevant for machine clients, it is important for humans.
Therefore, use indentation (see next advice for an exception to this), and order fields as in the examples of the specification/cookbook.

## Remove whitespace in data arrays

The `"values"` arrays in domain and range data can contain large numbers of elements.
By default, many JSON serializers add whitespaces (including newlines) between elements.
If gzip is used then the difference in data volume compared to having whitespace or not is minimal.
However, after decompression, each of those whitespaces has to be parsed by the client, and this can lead to increased loading time. Therefore, if possible, the `"values"` arrays, especially within the ranges, should have any whitespace omitted while serializing the JSON.

## Avoid spurious digits

When transforming from one data format to another it may happen that spurious digits get added to floating-point numbers. For example, a number may be stored on disk as exactly `0.01` (for example by storing it as an integer `1` together with a scaling factor `1e-2`). When reading this value back into a 32-bit floating point variable, the result is something like `0.0099999998`. Serializing this number in JSON would increases data volume and reduces compressibility because additional data in the form of spurious digits were added. Care should therefore be taken to avoid these issues if possible. The following strategies may help in doing that:

- Use the floating-point data type with the highest precision available and hope for the best.
- Apply rounding while serializing to JSON.
- Read numbers into an arbitrary-precision decimal data type. 

