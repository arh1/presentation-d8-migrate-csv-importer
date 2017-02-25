### Alter Source Field

my_module/src/Plugin/migrate/source/altered.php

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

* Same steps to create plugin
* Don't need to override initializeIterator here (not adding cols), just need prepareRow method
* Alter existing field and return parent's implementation
