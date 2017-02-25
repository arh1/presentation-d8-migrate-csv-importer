### Pipeline

Multiple, chained process plugins

<pre><code data-trim data-noescape>
process:
  my_field:
    -
      plugin: substr
      source: 'My Field Title'
      start: 6
      length: 10
    -
      plugin: machine_name
</code></pre>

~Notes:

* All fields pass through process pipeline
* Can chain multiple process plugins together
* Each plugin should do only one thing
* Output of one plugin passed on as input to the next
* Source key only needed on first plugin
