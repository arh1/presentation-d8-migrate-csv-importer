### Pipeline

Multiple process plugins

<pre><code data-trim data-noescape>
[...]
process:
  my_field:
    -
      plugin: substr
      source: 'My Field Name'
      start: 6
      length: 10
    -
      plugin: machine_name
[...]
</code></pre>

~Notes:

* Can chain multiple process plugins together in a pipeline
* Output of one plugin passed on as input to the next
* Source key only needed on first plugin
