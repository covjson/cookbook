{% macro playgroundLink(filename, title='Go to playground') -%}
  [{{ title }}](http://reading-escience-centre.github.io/covjson-playground/#https://raw.githubusercontent.com/reading-escience-centre/coveragejson-cookbook/master/examples/{{ filename }})
{%- endmacro %}