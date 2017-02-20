### Custom Process Plugin to Lookup Node IDs

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
    default_value: article<mark>
  my_entityref_field:
    plugin: lookup_title
    source: 'Title Column Name'</mark>
destination:
  plugin: entity:node
</code></pre>

~Notes:

*
