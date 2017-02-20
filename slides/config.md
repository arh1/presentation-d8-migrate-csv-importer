### Migration Config

config/migrate_plus.migration.my_migration.yml

<pre><code data-trim data-noescape>
id: my_migration
label: Migrate articles
migration_groups:
  - My migration group
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

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
id: my_importer
label: Import articles
migration_groups:
  - My migration group
source:
  plugin: csv
  path: '/path/to/file/my_articles.csv'
  header_row_count: 1
  keys:
    - ID
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
