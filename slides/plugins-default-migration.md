### _migration_ Core Plugin

Maintain relationships across migrations

<pre><code data-trim data-noescape>
process:
  my_field:
    plugin: migration
    migration: my_previous_migration
    source: 'My Field Title'
</code></pre>

~Notes:

* Maintain relationships across multiple migrations
* migration = ID of previous migration
* source = look this up from my_previous_migration mapping to populate value of my_field
* Previous migration should be a dependency of this one
