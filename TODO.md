* make note about passwords and security  - how tutorial is intentionally not secure and some machines may have a security policy that makes it impossible to use short passwords, and that users should be able to use whatever password they wish.

* note that updated java is apparently required to run the postgres stackbuilder

* edit tutorial to describe the creation of an osm_template db (with all the patched stuff for osm2pgsql), and the instructions for how to create new import database from that, as a template.

* add details about whether installers upgrade, overwrite, or install standalone when other versions exist. Also add details about what to do with two postgres versions on different ports.

* add details to tutorial to troubleshoot/avoid the common problem of a user trying to connect to a database in QGIS that does not exist (because they did not realize QGIS cannot create them, and rather they need to create in pgadminIII first)

* fix the OSM Tools plugin to catch the condition of a QGIS database being requested that does not actually exist yet (right now the osm2pgsql tool simply fails because an empty name is passed on the command line)

* add a sub-tutorial about how to handle windows defender issues (svhost.exe using all CPU scanning new installers added and locking up the system) - how to detect and disable/kill to allow the machine to not be sluggish.

* add a sub-tutorial
* test using normal user for running postgres (rather than postgres user) - update docs if it works

* tutorial needs writeup: tilemill csv tutorial

* tutorial needs writeup: using postgis 2.0 shape importer

* tutorial needs editing/cleanup: importing osm data with postgis

* tutorial on basic text/code editor, html page, javascript mapbox embed

* document how to allow trust config in pg_hba.conf via pgadmin (pg admin > tools > server configuration)

* document how to restart postgres via pgadmin (stop service/start service)

* document using PGPASS env variable with osm2pgsql

### longer term

* get latest osm2pgsql compiled on windows 

* get osmosis version updated in QGIS "Osm Tools" plugin to work with Java 7