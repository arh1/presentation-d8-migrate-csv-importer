### Overriding the File Path

settings.php

<pre><code class="php">
$config['my_importer']['source']['path'] = '/my/path/my_articles.csv';
</code></pre>

Console

<pre><code class="bash">
console config:override migrate_plus.migration.basics source.path /my/path/my_articles.csv
</code></pre>

~Notes:

*
