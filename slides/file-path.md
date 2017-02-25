### Overriding the File Path

settings.php

<pre><code data-trim data-noescape>
$config['my_importer']['source']['path']
  = '/path/to/my_articles.csv';
</code></pre>

Console

<pre><code data-trim data-noescape>
console config:override migrate_plus.migration.basics
  source.path /path/to/my_articles.csv
</code></pre>

~Notes:

*
