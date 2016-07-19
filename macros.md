{% macro playgroundLink(filename, title='Open in Playground') -%}
  <a href="https://covjson.org/playground/#https://raw.githubusercontent.com/covjson/cookbook/master/examples/{{ filename }}" target="_blank">{{ title }}</a>
{%- endmacro %}

{% macro exampleCode(filename) -%}
```js
{% include 'examples/' ~ filename %}
```
{%- endmacro %}