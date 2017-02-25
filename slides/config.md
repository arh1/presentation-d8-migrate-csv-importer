### Migration Config

config/migrate_plus.migration.my_migration.yml

<pre><code data-trim data-noescape>
id: my_migration
label: Migrate articles
migration_groups:
  - 'My migration group'
source:
  plugin: d6_node
  node_type: article
process:
  title: Title
  body: Body
  type:
    plugin: default_value
    default_value: article
destination:
  plugin: entity:node
</code></pre>

~Notes:

* Tracked by core CM (or Features)
* Stored w/ other site config (randomly-named /public dir or per path in settings.php)
* Simple = just config/yml; no custom PHP
* Here's simple D6 -> D8 migration
* Source = nodes from D6 db (node_type optional)
* Destination = nodes on target D8 site
* key-value pairs
* process: key = dest field; value = source field/column


### Importer Config

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
id: my_importer
label: Import articles
migration_groups:
  - 'My migration group'
source:
  plugin: csv
  path: '/path/to/my_articles.csv'
  header_row_count: 1
  keys:
    - ID
  process:
    title: Title
    body: Body
    type:
      plugin: default_value
      default_value: article
[...]
</code></pre>

~Notes:

* Here's importer config
* Main change = source plugin
* Plugin does req add'l config: path, header_row_count, keys
* keys = array of col names uniquely identify CSV rows
* header_row_count = num non-data rows at top of csv
* col names: header row, or column_names config
* other config: delimiter, enclosure, escape, fields (explicit field name overrides? @todo)
