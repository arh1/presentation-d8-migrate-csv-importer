### Migration Config

config/migrate_plus.migration.my_migration.yml

<pre><code data-trim data-noescape>
id: my_migration
label: Migrate articles
migration_groups:
  - My migration group
source:
  plugin: d6_node
  node_type: article
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

* All config can be tracked by core CM (or Features)
* Config stored w/ other site config (randomly-named /public dir or per path in settings.php)
* Simple migrations, you'll just need the config/yml and no custom PHP
* Here's simple articles migration D6 -> D8
* Source is nodes from a D6 db (node_type is optional config)
* Destination is nodes on target D8 site
* key-value pairs
* process: key = dest field; value = source field/column


### Importer Config

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
id: my_importer
label: Import articles
migration_groups:
  - My migration group
source:
  plugin: csv
  path: '/path/to/my_articles.csv'
  header_row_count: 1
  keys:
    - ID
  process:
    title: title
    body: body
    type:
      plugin: default_value
      default_value: article
[...]
</code></pre>

~Notes:

* Here's how our migration config looks for the importer
* Main change = source plugin
* This plugin does require add'l config: path, header_row_count, keys
* keys = array of column names that uniquely identify rows in csv
* header_row_count = number of non-data rows at the top of the csv
* col names come from header row, or column_names config
* other config: delimiter, enclosure, escape, fields (explicit field name overrides? @todo)
