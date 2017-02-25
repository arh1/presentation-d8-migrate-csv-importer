### Look up NID from Title String

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
process:
  title: Title
  body: Body
  my_entityref_field:
    plugin: lookup_title
    source: 'Referenced Entity Title'
  type:
    plugin: default_value
    default_value: article
</code></pre>

~Notes:

* key = Dest field name
* plugin key = new plugin (per annotation)
* source = csv column


### Look up NID from Title String

my_module/src/Plugin/migrate/process/Lookup.php

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
}
</code></pre>

~Notes:

* id from annotation matches id in plugin configuration
* here we extend ProcessPluginBase
* (CSV class for source plugin extends SourcePluginBase)


### Look up NID from Title String

Entity query in transform method to find nid

<pre><code class="php" data-trim data-noescape>
public function transform(
  $value,
  MigrateExecutableInterface $migrate_executable,
  Row $row,
  $destination_property
  ) {

  $result = \Drupal::entityQuery('node')
    ->condition('type', 'my_referenced_bundle')
    ->condition('title', '%' . db_like($value) . '%', 'LIKE')
    ->execute();

  return $result[0];
}
</code></pre>

~Notes:

* Only need transform method
* $value = source field string; return nid
* Entity query service -> array of matching nids
* We're hard-coding ref'd bundle
* $destination_property = field we're importing into
* Deeper dive: Typically abstract further (1 plugin regardless of ref'd bundle on destination)
* Could: inspect properties of destination field; pass in bundle as plugin config
* plugin would implement ContainerFactoryPluginInterface (allow to, among other things, pass in config)


### Look up NID from Title String

Error-handling

<pre><code class="php" data-trim data-noescape>
public function transform(...) {
  [...]

  if (!empty($result)) {
    return $result[0];
  }
  else {
    throw new MigrateException(
      sprintf(
        'Failed to lookup by Title, field name: %s.',
        $destination_property
      )
    );
  }
}
</code></pre>

~Notes:

* Let's add error-handling
* MigrateException class writes exceptions to db
