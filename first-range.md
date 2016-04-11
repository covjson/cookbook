# Step 3: Range Values

![Temperature values overlaid on grid](images/playground_temperature_coverage_with_values.png)

We know the temperature of each grid cell from the image above.
In CoverageJSON data values are associated to domain objects (here grid cells) with the help of a multi-dimensional array that is encoded as a flat one-dimensional array, here called NdArray. In general Coverage terminology, the set of values of a parameter are also called the Range. NdArray is one particular encoding scheme for Range values. Let's have a look at the code first:
```js
{
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
```
We can see that the values (by the way, missing values would become `null`) appear in the same layout as in the image above.
There are two reasons for that:

1. NdArrays always use [row-major order](https://en.wikipedia.org/wiki/Row-major_order).
The first array axis is `y` (latitude) and the second axis `x` (longitude), as given in `axisNames`.
With row-major order, the indices of the rightmost axis, here `x`, vary fastest.
This means that you start with `y=0` and iterate through `x=0..3`, then `y=1` and again `x=0..3`, until `y=3`.
2. The connection between NdArray axis indices and Domain axis coordinates is established by the ordering of the Domain axis.
There is a difference between an axis going from 54° to 48° and one going from 48° to 54°.

If we had switched the NdArray axis order around from y-x to x-y, then our array would look like that:
```js
{
  "type" : "NdArray",
  "dataType": "float",
  "axisNames": ["x", "y"],
  "shape": [4, 4],
  "values" : [
    17.3, 18.1, 19.2, 21.1,
    18.2, 19.4, 20.4, 21.3,
    16.5, 17.2, 21.1, 20.5,
    18.7, 18.6, 20.7, 19.2
  ]
}
```
Columns became rows, and rows became columns.

In general, clients will access values through an abstraction layer where axis names can be used, ignoring any underlying ordering or encoding of the array. For example, `value = ndarr.get({x:0, y:2})`. The indices then directly correspond to the domain axis coordinates at those indices, for example `longitude = domain.x.get(0)` and `latitude = domain.y.get(2)`.

However, to get started easily in an implementation that tries to read such arrays there is an advantage if the axis order is known and fixed.
For that reason, CoverageJSON defines several built-in profiles that guarantee a given ordering and make implementations that target those profiles easier to develop. More on that on the next page!
