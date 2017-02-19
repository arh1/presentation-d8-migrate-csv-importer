### Custom Plugin to Manipulate Source Columns

<pre><code data-trim data-noescape>
...
</code></pre>


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

~Notes:

*
