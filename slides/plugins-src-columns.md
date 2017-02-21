### Manipulate Source Columns

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
source:
  plugin: my_altered_csv
  path: '/path/to/my_articles.csv'
  header_row_count: 1
  keys:
    - ID
</code></pre>


### Manipulate Source Columns

modules/custom/my_module/src/Plugin/migrate/source/altered.php

<pre><code data-trim data-noescape>
namespace Drupal\my_module\Plugin\migrate\source;

use Drupal\migrate\MigrateException;
use Drupal\migrate\Row;
use Drupal\migrate_source_csv\Plugin\migrate\source\CSV;
use Drupal\migrate_source_csv\CSVFileObject;
use Drupal\Core\Database\Database;

/**
 * @MigrateSource(
 *   id = "my_altered_csv"
 * )
 */
class AlteredCSV extends CSV {
...
}
</code></pre>


### Manipulate Source Columns

modules/custom/my_module/src/Plugin/migrate/source/altered.php

<pre><code data-trim data-noescape>
</code></pre>

~Notes:

*
