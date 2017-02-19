### Custom Process Plugin to Normalize Strings

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
  location/country_code:
    plugin: country_normalization
    source: 'Working Location Country'</mark>
destination:
  plugin: entity:node
</code></pre>

~Notes:

*
