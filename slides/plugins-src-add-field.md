### Add Source Field

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


### Add Source Field

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


### Add Source Field

Override initializeIterator method to add column

<pre><code data-trim data-noescape>
public function initializeIterator() {
  [...]

  // Add column we will derive programmatically.
  $column_names[] =
    ['My Derived Field' => 'My Derived Field'];

  $file->setColumnNames($column_names);

  [...]
  return $file;
}
</code></pre>

~Notes:

* To add a field: override initializeIterator method from CSV plugin class
* Add column to $column_names array
* (Presumably could achieve same w/ column_names config)


### Add Source Field

Set the value of the new field

<pre><code data-trim data-noescape>
public function prepareRow(Row $row) {
  $pieces = [
    $row->getSourceProperty('My First Field'),
    $row->getSourceProperty('My Second Field')
  ];
  $row->setSourceProperty(
    'My Derived Field',
    implode('_', $pieces)
  );

  return parent::prepareRow($row);
}
</code></pre>

~Notes:

* Trivial example: new field concatenates two other fields
* Override prepareRow method from SourcePluginBase class (which CSV class extends)
* Add source property and return parent's implementation
* Can now use 'My Derived Field' elsewhere in migration config
