### Alter Source Field

modules/custom/my_module/src/Plugin/migrate/source/altered.php

<pre><code data-trim data-noescape>
public function alterMyField($value) {
  $cleaned = str_replace(['_'], [' '], $value);
  return $cleaned;
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

* Same steps to create plugin
* Don't need to override initializeIterator here, just need prepareRow method
* Override prepareRow method from SourcePluginBase class (which CSV class extends)
* Add source property and return parent's implementation
