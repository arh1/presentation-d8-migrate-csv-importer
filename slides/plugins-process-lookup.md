### Derive Node ID from Title String

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
process:
  title: title
  body: body
  my_entityref_field:
    plugin: lookup_title
    source: 'Referenced Entity Title'
  type:
    plugin: default_value
    default_value: article
</code></pre>

~Notes:

* CSV often has string titles for referenced entities...


### Derive Node ID from Title String

modules/custom/my_module/src/Plugin/migrate/process/lookup.php

<pre><code class="php" data-trim data-noescape>
namespace Drupal\my_module\Plugin\migrate\process;

use Drupal\migrate\MigrateException;
use Drupal\migrate\MigrateExecutableInterface;
use Drupal\migrate\ProcessPluginBase;
use Drupal\migrate\Row;
use Drupal\Core\Database\Database;

/**
 * @MigrateProcessPlugin(
 *   id = "lookup_title"
 * )
 */
class LookupTitle extends ProcessPluginBase {
...
}
</code></pre>

~Notes:

*


### Derive Node ID from Title String

modules/custom/my_module/src/Plugin/migrate/source/lookup.php

<pre><code class="php" data-trim data-noescape>
public function transform($value, MigrateExecutableInterface $migrate_executable, Row $row, $destination_property) {
  if (empty($value)) {
    return;
  }

  $result = \Drupal::entityQuery('node')
    ->condition('type', $destination_property)
    ->condition('title', '%' . db_like($value) . '%', 'LIKE')
    ->execute();

  if (!empty($result)) {
    return array_shift($result);
  }
  else {
    throw new MigrateException(sprintf('Failed to lookup by Title, field name: %s.', $destination_property));
  }
}
</code></pre>

~Notes:

* Process plugin class only needs one method: transform
* @todo: destination_property ...
