### Migrate Background

* Core module (yay!)
* D6, D7 -> D8
* Importers as well

~Notes:

* The workhorse Migrate module was moved into core for Drupal 8 with great fanfare, and much attention has been paid to its use as a way to migrate a site to D8 from earlier versions of Drupal. In addition to one-time migrations, Migrate is an excellent tool for recurring data imports as well, and its inclusion in core gives us that much stronger of a foundation on which to build importers moving forward. In this post we'll walk through building a CSV importer in Drupal 8, touching on many powerful aspects of Migrate in core along the way.
