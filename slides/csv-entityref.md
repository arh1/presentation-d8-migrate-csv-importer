### Add an Entity Reference Field

<pre><code data-trim data-noescape>
ID,title,body,Referenced Entity Title
1,title 1,some body text 1,title of referenced entity A
2,title 2,some body text 2,title of referenced entity B
3,title 3,some body text 3,title of referenced entity C
</code></pre>

~Notes:

* Unlike migration process plugin example, here let's assume ref'd entity already exists
* Ultimately in our dest, need a pointer to nid for referenced entity
