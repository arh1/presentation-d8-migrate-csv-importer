### Normalize Country Name

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
process:
  title: Title
  body: Body
  my_address_field/country_code:
    plugin: country_normalization
    source: 'Country Name'
  type:
    plugin: default_value
    default_value: article
</code></pre>

~Notes:

* Note nested key for addressfield
* (our field name is 'my_address_field', 'country_code' is component/subfield)


### Normalize Country Name

my_module/src/Plugin/migrate/process/normalize.php

<pre><code class="php" data-trim data-noescape>
namespace Drupal\my_module\Plugin\migrate\process;

use Drupal\migrate\MigrateException;
use Drupal\migrate\MigrateExecutableInterface;
use Drupal\migrate\ProcessPluginBase;
use Drupal\migrate\Row;
use Drupal\Core\Locale\CountryManager;

/**
 * @MigrateProcessPlugin(
 *   id = "country_normalization"
 * )
 */
class countryNormalization extends ProcessPluginBase {
}
</code></pre>

~Notes:

* Again, note id from annotation...
* And extending ProcessPluginBase
* Include CountryManager class


### Normalize Country Name

Define alternate country names

<pre><code class="php" data-trim data-noescape>
private $alt_country_names = array (
  'US' => array (
    'USA',
    'United States of America',
    'merica',
  ),
);
</code></pre>

~Notes:

* Array of matching strings


### Normalize Country Name

Match defined countries or try alternates

<pre><code class="php" data-trim data-noescape>
public function transform(...) {
  $existing_countries = CountryManager::getStandardList();

  foreach ($existing_countries as $country_key => $country){
    if ($country->render() == $value) {
      return $country_key;
    }
  }
  foreach($this->alt_country_names
    as $country_key => $country_names) {
    if (in_array($value, $country_names)) {
      return $country_key;
    }
  }
}
</code></pre>

~Notes:

* Get list of existing countries from CountryManager class
* Check against that list, then our alternate country names
* Probably need to be careful about case-sensitivity, trimming whitespace, etc


### Normalize Country Name

Error-handling

<pre><code class="php" data-trim data-noescape>
public function transform(...) {
  [...]

  foreach($this->alt_country_names
    as $country_key => $country_names) {
    if (in_array($value, $country_names)) {
      return $country_key;
    }
  }
  throw new MigrateException(
    sprintf(
      'Failed to find ISO Country Code for field: %s. Value: %s',
      $this->configuration['source'], $value)
    );
}
</code></pre>

~Notes:

* If we failed to match, be sure to throw exception
* Note we can get source from migration's configuration property
* abstract class ProcessPluginBase extends PluginBase implements MigrateProcessInterface
* class countryNormalization extends ProcessPluginBase
