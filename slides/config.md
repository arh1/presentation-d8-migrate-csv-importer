### Migration Config

<pre><code data-trim data-noescape>
id: my_migration
label: Migrate articles
migration_groups:
  - ACME migration
source:
  plugin: my_other_db
process:
  title: title
  body: body
  type:
    plugin: default_value
    default_value: article
destination:
  plugin: entity:node
</code></pre>


### Importer Config

<pre><code data-trim data-noescape>
id: my_importer
label: Import articles
migration_groups:
  - ACME import
source:<mark>
  plugin: csv
  path: '/path/to/file/acme_articles.csv'
  header_row_count: 1</mark>
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

~Notes:

* Configuration for our migrations -- whether from core, contributed, or our custom modules -- can of course be captured and tracked using D8 core's configuration management system. Just adapting quickly from the Migrate Source CSV docs as a starting point, our initial migration configuration using a csv source might look like this:
