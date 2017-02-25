### Alter Source Field

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
source:
  plugin: my_altered_csv
  path: '/path/to/my_articles.csv'
  header_row_count: 1
  keys:
    - ID
</code></pre>

~Notes:

* Changed source plugin


### Alter Source Field

my_module/src/Plugin/migrate/source/Altered.php

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
}
</code></pre>

~Notes:

* Extend CSV source plugin class
* Annotation matches value for plugin key in config


### Alter Source Field

my_module/src/Plugin/migrate/source/Altered.php

<pre><code data-trim data-noescape>
private function alterMyField($value) {
  $altered = str_replace('_', ' ', $value);
  return $altered;
}

public function prepareRow(Row $row) {
  // Replace underscores with spaces.
  $row->setSourceProperty(
    'My Field',
    $this->alterMyField($row->getSourceProperty('My Field')
  );

  return parent::prepareRow($row);
}
</code></pre>

~Notes:

* Trivial example: string replacement
* Override prepareRow method from SourcePluginBase class (which CSV class extends)
* Alter existing field and return parent's implementation
