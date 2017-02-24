### Migration Status

* _drush ms_
* _console migrate:debug_
* UI: Structure -> Migrations

~Notes:

* UI = drush ms output w/ links to messages


### Migration Status

Before we've run either importer

<pre><code data-trim data-noescape>
ahieb@ahieb-pc:~/develop/my_project$ drush @my_project.local ms
 Group: my_group               Status  Total  Imported  Unprocessed  Last imported       
 my_importer                   Idle    101    0         101           
 my_other_importer             Idle    101    0         101          
ahieb@ahieb-pc:~/develop/my_project$
</code></pre>

~Notes:

*
