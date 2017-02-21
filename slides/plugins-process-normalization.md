### Normalize Country Name

config/migrate_plus.migration.my_importer.yml

<pre><code data-trim data-noescape>
process:
  title: title
  body: body
  location/country_code:
    plugin: country_normalization
    source: 'Country Name'
  type:
    plugin: default_value
    default_value: article
</code></pre>


### Normalize Country Name

modules/custom/my_module/src/Plugin/migrate/process/normalize.php

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
...
}
</code></pre>

~Notes:

*


### Normalize Country Name

modules/custom/my_module/src/Plugin/migrate/source/normalize.php

<pre><code class="php" data-trim data-noescape>
private $alt_country_names = array (
  'US' => array (
    'USA',
    'United States of America',
    'merica',
  ),
);

public function transform($value, MigrateExecutableInterface $migrate_executable, Row $row, $destination_property) {
  if (empty($value)) {
    return;
  }

  $existing_countries = CountryManager::getStandardList();
  $value = ucwords(strtolower(trim($value)));

  foreach ($existing_countries as $country_key => $country){
    if ($country->render() == $value) {
      return $country_key;
    }
  }

  foreach($this->alt_country_names as $country_key => $country_names) {
    if (in_array(strtolower($value), array_map('strtolower', $country_names))) {
      return $country_key;
    }
  }
  throw new MigrateException(sprintf('Failed to find ISO Country Code for field : %s. Value: %s', $field, $value));

}
</code></pre>
