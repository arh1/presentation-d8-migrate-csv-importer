### Migration Rollback

* _drush mr_

~Notes:

*


### Migration Rollback

After running both and rolling one back. Oops?

<pre><code data-trim data-noescape>
ahieb@ahieb-pc:~/develop/my_project$ drush @my_project.local ms
 Group: my_group               Status  Total  Imported  Unprocessed  Last imported       
 my_importer                   Idle    67     168       0          2017-02-24 00:18:37
 my_other_importer             Idle    67     0         67           2017-02-24 00:19:54
ahieb@ahieb-pc:~/develop/my_project$
</code></pre>

~Notes:

* Rollback removes all imported entities from all previous CSVs
* by design...
