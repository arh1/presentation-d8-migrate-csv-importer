### Migration Import

* _drush mi_
 * _--update_ (vs track_changes: true)
 * _--force_
* _console migrate:execute_

~Notes:

* --update is like `track_changes: true` but former updates ALL rows, where latter just updates where hashes differ


### Migration Import

After running first importer

<pre><code data-trim data-noescape>
ahieb@ahieb-pc:~/develop/my_project$ drush @my_project.local ms
 Group: my_group               Status  Total  Imported  Unprocessed  Last imported       
 my_importer                   Idle    101    101       0            2017-02-24 00:18:37
 my_other_importer             Idle    101    0         101          
ahieb@ahieb-pc:~/develop/my_project$
</code></pre>

~Notes:

*


### Migration Import

After running second importer

<pre><code data-trim data-noescape>
ahieb@ahieb-pc:~/develop/my_project$ drush @my_project.local ms
 Group: my_group               Status  Total  Imported  Unprocessed  Last imported       
 my_importer                   Idle    101    101       0            2017-02-24 00:18:37
 my_other_importer             Idle    101    101       0            2017-02-24 00:19:54
ahieb@ahieb-pc:~/develop/my_project$
</code></pre>

~Notes:

*


### Migration Import

After uploading a new CSV. Oops...

<pre><code data-trim data-noescape>
ahieb@ahieb-pc:~/develop/my_project$ drush @my_project.local ms
 Group: my_group               Status  Total  Imported  Unprocessed  Last imported       
 my_importer                   Idle    67     101       -34          2017-02-24 00:18:37
 my_other_importer             Idle    67     101       -34          2017-02-24 00:19:54
ahieb@ahieb-pc:~/develop/my_project$
</code></pre>

~Notes:

* Total = rows in new CSV
* Imported = total entities imported (rows in migrate_map_my_importer)
* Unprocessed = delta
* by design...
