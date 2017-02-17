## Initial Importer Config

<pre><code data-trim data-noescape>
id: my_importer
label: Import articles
migration_groups:
  - ACME import

source:
  plugin: csv
  path: '/path/to/file/acme_articles.csv'
  header_row_count: 1
  keys:
    - Id2

process:
  title: title
  body: body
  type:
    plugin: default_value
    default_value: article

destination:
  plugin: entity:node
</code></pre>
