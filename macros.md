{% macro playgroundLink(filename, title='Open in Playground') -%}
  [{{ title }}](http://reading-escience-centre.github.io/covjson-playground/#https://raw.githubusercontent.com/reading-escience-centre/coveragejson-cookbook/master/examples/{{ filename }})
{%- endmacro %}

{% macro exampleCode(filename) -%}
```js
{% include 'examples/' ~ filename %}
```
{%- endmacro %}