{% macro playgroundLink(filename, title='Go to playground') -%}
  [{{ title }}]({{ book.playgroundBaseUrl }}{{ book.exampleBaseUrl }}{{ filename }})
{%- endmacro %}