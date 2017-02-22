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

* All migration config can be tracked by core CM (or Features)
* For simple migrations, you'll just need the config/yml and no custom code
* Here's a simple migration of articles from a D6 to D8 site
* Source is nodes from a D6 db (node_type is optional config)
* Destination is nodes on target D8 site


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
destination:
  plugin: entity:node
</code></pre>

~Notes:

* Here's how our migration config looks for the importer
* Main change here is our source plugin
* This plugin does require add'l config
