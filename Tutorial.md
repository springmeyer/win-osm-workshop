# An introduction to QGIS, PostGIS, and TileMill for Windows

This guide is intended to demonstrate basic usage of Natural Earth data and OpenStreetMap data within QuantumGIS (QGIS), PostGIS, and TileMill.

QGIS is a free desktop GIS program with features similar to ArcMap.

PostGIS adds GIS functions to the PostgreSQL database. Will get OSM data into it using the osm2pgsql.

TileMill is a cartography design studio.

We choose these tools mainly because they have easy installers for windows. But, for details more on the "why" of these tools see: http://sproke.blogspot.com/2012/02/game-changer-open-source-mapping-in.html


# Table of Contents

1. Installing the Tools
1. Using Natural Earth shapefiles
1. Importing, filtering, and mapping with OSM data
1. Appendices
1. References


# Installing the Tools

Note: all installers and data referenced below as "local" are mirrored online at http://osgis-windows.s3.amazonaws.com

These are designed to be downloaded and packaged locally by instructors of this workshop by doing:

```
mkdir installers
mkdir data
cd installers
wget http://osgis-windows.s3.amazonaws.com/installers/7z920.exe
wget http://osgis-windows.s3.amazonaws.com/installers/HOT_Installer.exe
wget http://osgis-windows.s3.amazonaws.com/installers/QGIS-OSGeo4W-1.7.4-d211b16-Setup.exe
wget http://osgis-windows.s3.amazonaws.com/installers/TileMill-v0.9.1-Setup.exe
wget http://osgis-windows.s3.amazonaws.com/installers/postgis_2_0_pg91.exe
wget http://osgis-windows.s3.amazonaws.com/installers/postgresql-9.1.3-2-windows.exe
cd ../data
wget http://osgis-windows.s3.amazonaws.com/data/10m-admin-0-countries.zip
wget http://osgis-windows.s3.amazonaws.com/data/washington.osm.bz2
wget http://osgis-windows.s3.amazonaws.com/data/900913.sql
wget http://osgis-windows.s3.amazonaws.com/data/legacy.sql
wget http://osgis-windows.s3.amazonaws.com/data/gistfix.sql
```

## Step 1: Install 7-Zip

This tool will be needed to uncompress bz2 files (like compressed OSM data).

Install from local copy:

1. `installers/7z920.exe`

**Or** install from the web:

1. http://downloads.sourceforge.net/sevenzip/7z920.exe

### Setup file extensions

1. Go the Start Menu > 7-Zip > 7-Zip File Manager
1. Within the 7-Zip File Manager choose Tools > Options
1. Under the system tab choose 'bz2' (or Select all')
1. Press OK: now any bz2 files should automatically open in 7-Zip

## Step 2: Install QuantumGIS

Install from local copy:

1. `installers/QGIS-OSGeo4W-1.7.4-d211b16-Setup.exe`

**Or** install from the web:

1. Google for “QGIS” to find http://www.qgis.org/
1. Click Download, then choose Current Version/Software
1. Find the [Windows "Standalone” installer](http://www.qgis.org/downloads/QGIS-OSGeo4W-1.7.4-d211b16-Setup.exe)
1. Right click the installer and choose "Run as Administrator"
1. QGIS should then appear in your program menu

### Customize QuantumGIS (Optional)

1. Go to Plugins > Fetch Python Plugins...
1. Wait for Python repositories to be fetched.
1. Go to the Options Tab
1. Check the box next to "Check for updates on startup"
1. Change the drop down-menu to "every time QGIS starts"
1. Click "Close"
1. Go to Settings > Options
1. "General" tab, "Application" section: change the "Icon theme" dropdown menu from "default" to "gis"
1. "Rendering" tab, "Rendering quality" section: make sure "Make lines appear less jagged at the expense..." is checked.
1. "CRS" tab, Coordinate Reference System..." section: make sure "Prompt for CRS" is checked
1. Click "OK"


## Step 3: Install TileMill

Install from local copy:

1. `installers/TileMill-v0.9.1-Setup.exe`

**Or** install from the web:

Grab the latest version from http://mapbox.com/tilemill

Run the installer as an administrator. It will put a TileMill start shortcut in your Start Menu.


## Step 4: Install PostgreSQL and PostGIS

Install from local copy:

1. First install PostgresSQL via: `installers/postgresql-9.1.3-2-windows.exe`
1. Next, install PostGIS via: `installers/postgis_2_0_pg91.exe`

Then see set-up details below.

**Or** install from the web:

1. Go to http://www.postgresql.org/download/windows
1. Click on the link to "Download the one click installer," which will take you to: http://www.enterprisedb.com/products-services-training/pgdownload#windows. **Note:** this is a different site from the postgres site, but that's ok.
1. Click on the Version 9.1.3 (or whatever is latest in the 9.1.x series) download button for your version of Windows.
1. Click "Save" (or whatever you browser supports)
1. Navigate to where the installation file (named something like `postgresql-9.1.3-1-windows.exe`) is located and double-click on it to launch the installer.

Set-up Details

1. Click "Next" through the first few Setup wizard steps.
1. On the "Password" screen, type "osm". **Note:** PostgreSQL has its own users and superusers, which are separate and distinct from Windows users and administrators. As a default, PostgreSQL installation sets up **both** a PostgreSQL superuser named "postgres" and a Windows system user account named "postgres" that will use the same password. Confused yet? Who's on first? 
1. Click "Next" through the rest of the Setup wizard steps, leaving all values as their defaults.
1. The last step of the Setup wizard should ask if you want to launch something called "Stack Builder." If you are online, you do! If you are offline, you will want to use the standalone installer identified above to install PostGIS.
1. Make sure that the check box is checked.
1. Click "Finish", which both finishes PostgreSQL installation and launches the Stack Builder.
1. On the first page of the "Stack Builder 3.1.0" window, in the drop down, select "PostgreSQL on port 5432"
1. Click "Next"
1. On the next page, click on the "+" sign next to "Spatial Extensions"
1. Check the box next to "PostGIS 2.0 for PostgreSQL 9.1 v2.0.0
1. Click "Next" until presented with the "PostGIS 2.0.0" setup window.

PostGIS Install Details

1. Start the installer through the Stack Builder or the standalone installer.
1. Click "I Agree"
1. Click "Next" until you get to the "Database Connection" window
1. In the "Password" field, type "osm"
1. Click "Next"
1. On the "Database Name" window, in the "Database Name:" field, type "osm"
1. Click "Install"
1. Click "Yes" to the "Would you like us to register the GDAL_DATA environment variable (see Appendix C), click "Yes"
1. Click "Close" on the "Installation Complete" window.
1. If you're in the Stack Builder, click "Finish." If using the standalone installer, you won't need this step.


Verify PostgreSQL and PostGIS installation success:

1. Find the "pgAdmin III" application in your Start menu.
1. This should bring up an administrative window, with an "Object Browser" on the left side of the window.
1. In the Object browser, double click on the icon with the red "X" labeled "PostgreSQL (localhost:5432)"
1. Enter your password, "osm"
1. The red "X" should disappear and a set of items should be listed below the "PostgresSQL" label.
1. Click on the "+" sign next to the "Databases" icon
1. There should be an icon with a red X labeled "osm"
1. Click on the "+" sign next to the "osm" icon
1. There should be an icon labeled "Extensions" below "osm"
1. Click on the "+" sign next to the "Extensions" icon
1. If you see the items "postgis" and "postgis_topology" listed under the extensions, congrats! PostGIS 2.0 is installed.

**Troubleshooting**
If on Windows Vista or Windows 7, and your local account is not an administrator, you may need to give the "postgres" user administration privileges
Otherwise you will may see errors about "permission denied" when trying to start the server.

1. Windows 7: Start > Control Panel > User Accounts
1. Manage another account, Pick Postgres
1. Change Account Type, make administrator
1. Go back to User Accounts view
1. Change User Account Control Settings
1. Lower the UAV settings to the lowest setting
1. Restart your machine, login as your normal user
1. Now the PostgreSQL server should be automatically running
1. Now you may need to restart your machine to trigger the PostgreSQL Server to restart.

If you get an error about access denied, then go back and repeat the above user account steps

### Connect to your (empty) PostGIS database from within QGIS

This step is just to test PostGIS is functioning okay for QGIS.

1. Open QGIS
1. Go to Layers > Add PostGIS Layers...
1. Click "New"
1. Then in the connections window type:
```
Name: OSM
Service: leave blank
Host: leave blank
Port: 5432
Database: osm
SSL mode: leave as "disable"
Username: postgres
Password: osm
```
1. Check "Save Username"
1. Check "Save Password"
1. Click "Test Connect" and you should should get a message that the connection was successful
1. Click "OK" to return you to the previous menu
1. Click "Close" to leave the "Add PostGIS Layers..." menu

Note: again, there is no data yet in this database so it is okay if you see a message from QGIS complaining about there being no accessible tables.

## Step 6: Configure the "osm" PostGIS database

Now we need to do a few customizations to our postgis database to ensure that osm2pgsql works with PostGIS 2.0.

These workarounds are needed largely because the osm2pgsql version available for windows is quite old (and hopefully in the future these will not be needed).

### Initialize the database with a custom projection

The reason for this step is to workaround this bug: http://trac.osgeo.org/postgis/ticket/1805

A file containing this custom projection can be found locally:

1. `data/900913.sql`

**Or** downloaded from:

1. Download http://svn.openstreetmap.org/applications/utils/export/osm2pgsql/900913.sql

To add to your database do:

1. Go to pgAdmin III
1. Drill down into the Object Browser until you reach the "osm" database. You may need to login to the database again.
1. Select the "osm" database
1. Click on the "Execute arbitrary SQL queries" button (it looks like a magnifying glass)
1. File > Open
1. Browse to the `data/900913.sql` file and select it
1. Click "Open"
1. Click on the "Execute Query" button (it looks like a green triangle pointed to the right or a green "Play" icon)
1. The "Output pnae" should display a message that reads "Query returned succesfully...."
1. Close the "Query" window


### Initialize the database with legacy sql functions

The reason for this step is that the osm2pgsql build for windows is very old and still uses functions that have been removed from PostGIS 2.0 by default.

A file containing these legacy functions can be found locally:

`data/legacy.sql`

**Or** downloaded from:

http://trac.osgeo.org/postgis/browser/trunk/postgis/legacy_minimal.sql.in.c?format=txt

To add to your database do:

1. Go to pgAdmin III
1. Drill down into the Object Browser until you reach the "osm" database
1. Select the "osm" database
1. Click on the "Execute arbitrary SQL queries" button (it looks like a magnifying glass)
1. File > Open
1. Browse to the `data/legacy.sql` file and select it
1. Click "Open"
1. Click on the "Execute Query" button (it looks like a green triangle pointed to the right or a green "Play" icon)
1. The "Output pnae" should display a message that reads "Query returned succesfully...."
1. Close the "Query" window


### Initialize the databse with legacy spatial indexing keyword

A file containing this hotfix can be found locally:

`data/gistfix.sql`

**Or** can be downloaded from:

http://trac.osgeo.org/postgis/ticket/1287#comment:8

To add to your database do:

1. Go to pgAdmin III
1. Drill down into the Object Browser until you reach the "osm" database
1. Select the "osm" database
1. Click on the "Execute arbitrary SQL queries" button (it looks like a magnifying glass)
1. File > Open
1. Browse to the `data/gist.sql` file and select it
1. Click "Open"
1. Click on the "Execute Query" button (it looks like a green triangle pointed to the right or a green "Play" icon)
1. The "Output pnae" should display a message that reads "Query returned succesfully...."
1. Close the "Query" window



## Step 7: Install osm2pgsql

Osm2pgsql is included in the "HOTOSM Installer"

Install from local copy:

`installers/HOT_Installer.exe`

**Or** install from the web:

Download the "HOT_Installer" from: https://github.com/hotosm/installer/downloads

1. Navigate to the folder where you've stored `HOT_Installer.exe` and click on it.
1. When prompted, reboot your machine.

For downloading and installing osm2pgsql manually see Appendix F.


## Step 8: Install the OSM Tools Plugin for QGIS

If online, use the following steps.
If offline skip to the offline installation section below.

Online Installation

1. Open QGIS
1. Plugins > Fetch Python Plugins
1. Click “Repositories” tab
1. Click Add...
1. Then type:
```
Name: dbsgeo.com plugins
URL: http://qgis.dbsgeo.com
```
1. Check "Enabled"
1. Click "OK"
1. Click on the “Plugins” tab and you should should see “OSM Tools” available to install
1. Highlight “OSM Tools” 
1. Click “Install Plugin”
1. You should see a message that the "Plugin installed successfully"
1. Click "OK"
1. Click "Close"
1. You should now have a menu item called "OSM Tools" in your top-level QGIS menu bar.

Offline Installation

A file containing the OSM Tools plugin functions can be found locally:

`data/osm_tools.zip`

1. Extract the .zip file to a local directory named `osm_tools`
1. Copy the entire osm_tools directory to `c:\Users\[your_username]\.qgis\python\plugins\` (You may need to create the "python" and "plugins" subdirectories)
1. Open QGIS
1. Plugins -> Manage Plugins
1. In the "Filter" field, type `osm`
1. Check the box next to "OSM Tools (Version 0.1.7)"
1. Click "OK"
1. You should now have a menu item called "OSM Tools" in your top-level QGIS menu bar.












TODO, below…..










## Step 7: Load an OSM file into PostGIS
1. Open QGIS
1. OSM Tools > Import into PostGIS (osm2pgsql)
1. This will create another panel on the right-hand side of your GQIS window.
1. Click "Input" to choose an .osm file (of your choosing)
1. `data\san-juans.osm.bz2`  _**??? where should these osm files be located? Should I have downloaded anything yet?**_
1. IGNORE the "Style" option for now.
1. In the "Database" section, make sure "osm" is selected in the drop-down menu.
1. Keep all other defaults
1. Click "Run"
1. You may see lots of output in the bottom window
1. There should be a green "Finished!" in the bottom window of the "Import OSM data..." panel.
1. Unless you see an error, then the data should now be inside PostGIS  

Optional: import data on the command line (see Appendix H)

**Note:** This is a new plugin written by Dane (dane@dbsgeo.com), if you have any problems email me!

## Step 8: View the PostGIS layers in the map
1. Open QGIS
1. Go to Layers > Add PostGIS Layer...
1. Select "isn" from the drop down menu
1. Click Connect      
1. Then select each table that is listed, for example: planet_osm_line, planet_osm_road, planet_osm_point, and planet_osm_polygon
1. Click "Add"
1. Close the window
1. The layers should be viewable in the main QGIS map window
1. If you get a prompt for the Projection of each layer, keep the default of WGS 84
1. Now you should be able to browse and query these tables of osm data just as if they were shapefiles or other tabular GIS data

## Step 9: Using a custom osm2pgsql style file for Humanitarian Data Model tags
This has not been implemented yet. Contact Dane for help (dane@dbsgeo.com) or Nicolas Chavent (nicolas.chavent@gmail.com). Essentially you will need a custom 'style' file for osm2pgsql. We have plans to provide a sample but it is not quite ready yet. We may just bundle it with the plugin so you can soon update the plugin to get a custom style file










## Step 5: Loading OSM data into QGIS

### Option A: Download Data from OpenStreetMap
In your QGIS display window, 

1. Zoom into a small area with background data as a reference
1. (If you are already looking at Haiti in the window, you can use the scale selector in the lower-right hand corner of the QGIS window and select 1:25000)   
1. [[do you want to get into planet.osm here? A lot of these regions have quite a few nodes....]]
1. Click the “Download OSM Data” button (it has a blue arrow pointed down) **Note:** this will be in the OSM menu bar buttons on QGIS and not in the right-side OSM panel.
1. In the "Download OSM data" window, click "Download"
1. The OSM data should appear in left side “Layers” window and look something like this:
```
download points
download lines
download polygons
```
1. Right click on each layer and select “Save As...”
1. In the "Save vector layer as..." window, enter the file name in the "Save as" form field
1. Hit the "Browse" button to make sure you are saving this file in the proper location. **Note:** If you skip this step, QGIS tends to try to save to a system folder where it does not have write permission and you will get an error message.
1. Click "Save"
1. Click "OK"

[[This is already set - should this be mentioned? --> Choose the default “WGS84” projection. Should they select to add saved layer to the map?]]

### Option B: load an osm file from the filesystem
1. Download the haiti extract from geofabrik: http://labs.geofabrik.de/haiti/
1. You want the 'latest.osm.bz2'
1. To uncompress the .bz2 file, see Appendix B.

Or

1. Get sample OSM data from the HOT KIT: /data/haiti/00_Haiti_Donnees-OSM_OSM-Data-OSM
1. Open QGIS
1. Go to Plugins > OpenStreetMap > Load Osm from file (or click icon on menu bar)
1. Navigate to the file to load and:
* Check all tags to add
* Uncheck "use custom renderer"
1. Click okay, then the layers should load into QGIS as line, points, and polygons

## Step 6: Export OSM data to a shapefile
[[aren't the first 3 steps already accomplished in some of the above steps? At least, they seem to be in "Option A" above.]]

1. Now you should have osm files inside QGIS as lines, points, and polygons.
1. Right click on each of the layers and choose "Save as Shapefile"
1. Save each shapefile as:
* points.shp
* lines.shp
* polygons.shp
1. Go to File > New Project 
1. When prompted in the "Save?" window, click "Discard"
1. Then, reload the exported shapefiles
1. Go through the steps at Layers > Add Vector Layer (or drag and drop from windows explorer) for the three shapefiles
1. getting osm poly-line-points into thematic shp using the query builder from the shapefiles generated in the above step
attributes: you only see default attributes set up by QGIS [[not sure what this step means]]
1. [[Note: what I'm seeing on my QGIS display is pretty crazy looking at this stage...]]

# Step 7: Style the data
1. Right click (or double click) on the shapefile layer [[which one?]] to get access to the properties
1. Go to the "Labels" tab:
1. Check "Display labels"
1. On the "Label Properties" sub-tab, in the "Basic label options" section, set "Field containing label" to "name"
1. Click "OK"
1. Experiment with changing the display of lines, points, or polygons with the "Symbology Tab" [[not sure what this has migrated into - no longer a vector layer tab]]

For advanced symbolization ideas see Appendix F [[not sure this adds anything to the discussion above]]

## Step 8: Save to a QGIS project file
1. Go to File > Save project as..
1. Save to a file name and location that are easy to remember


















# Appendices

## Appendix A: Enable showing file extensions
Windows 7:

1. Start > Control Panel > Folder Options
1. Click View Tab
1. Check “Show hidden files, folders, and drives”
1. Check "Uncheck Hide extensions for known file types."

## Appendix B: Working with OSM Extracts - Handling osm.bz2 files
1. Download bzip2 windows installer from: http://gnuwin32.sourceforge.net/packages/bzip2.htm
1. Click on “Complete package, except sources”
1. Run the installer
1. Then right-click on an osm.bz2 file and choose “Open With... > Choose default Program”
1. Navigate and choose: `C:\Program Files (x86)\GnuWin32\bin`
1. Now you should be able to double click any osm.bz2 file and it will uncompress to a file without the bz2 extension, which makes it possible to open directly by QGIS


## Appendix C: How to edit system Path environment settings
Windows 7:

1. Start > Control Panel > System
1. Click Advanced System Settings
1. On the "Advanced" Tab, at the bottom of the tab, click the "Environment Variables" buttons.
1. In the "System variables" section - NOT the "User variables" section - select the "Path" variable
1. Click Edit
1. Put your cursor in the "Variable Value" input area
1. Move the cursor to the far right and add a `;` if the line does not already end with one
1. Then add the custom path to a directory needed like "C:\Program Files (x86)\GnuWin32\bin"
1. Click "OK"
1. Click "OK" again.
1. You should be done

## Appendix D: Working with the command prompt on Windows
Windows 7:

1. Navigate to a directory using Windows Explorer
1. Then press shift and right-click on white space
1. Choose "Open Command window here"

Other Windows:

1. Install http://www.microsoft.com/windowsxp/Downloads/powertoys/Xppowertoys.mspx and follow above recommendations

Or:

1. Open the start menu
1. In the search bar, type "cmd"
1. To move into a new directory, type: `cd <dir name>`
1. To list items in a directory type: `dir`

## Appendix F: Installing osm2pgsql manually
Download osm2pgsql:

1. Download osm2pgsql windows binary from: http://tile.openstreetmap.org/osm2pgsql.zip
1. Move the file to the root of the C drive, so the file will be C:\osm2pgsql.zip. **Note:** Moving a file to the root directory of your c: drive will require Administrator privileges.
1. Unzip with 7-zip: Right click on the .zip file and choose 7-zip > Extract here

Fix "Path" environment settings (see Appendix C) to include the following: 
```
C:\osm2pgsql
C:\Program Files\PostgreSQL\9.1\bin
```
**Note:** If you have a 64 bit OS and installed the 32 bit version of PostgreSQL, you may need to use `C:\Program Files (x86)\PostgreSQL\9.1\bin` instead of the path listed above.

You should now test that the "Path" setting is working:

1. Open a command prompt (See Appendix E)
1. Type into the command prompt: `osm2pgsql`
1. You should receive a usage error stating the osm2pgsql version, which is good. If not, go back and re-confirm your Path settings.

## Appendix H: Using osm2pgsql on the command line
Open a command prompt in the directory of an osm file (See Appendix E).

Then, assuming the osm file is called 'latest.osm', type:

`osm2pgsql -U postgres -W -d osm -S C:\osm2pgsql\default.style latest.osm`


## Appendix I: create a new postgis-enabled database via the psql shell
1. Open the PostgreSQL shell, aka pqsl:
1. Go to Start > Programs > PostgreSQL > SQL Shell (psql)
1. You will get a command prompt asking for input of connection parameters
1. Hit return to accept the default for all items, until you get to the password where you should type the password "osm"
1. Now, you should be inside the postgres shell
1. Type (note, make sure to finish any commands you see below with the ";" !!!)
```
CREATE DATABASE osm WITH TEMPLATE postgis;
```
1. While we are inside the shell lets learn a few commands:
1. Switch into this new database called "osm": `\c osm`     
1. List the tables inside this database: `\d`
1. Get details about a specific table: `\d geometry_columns`
1. Exit the database and shell: `\q`


# References

## General:
* https://github.com/nvkelso/geo-how-to

## QGIS:
* http://wiki.openstreetmap.org/wiki/QGIS
* http://linfiniti.com/dla/AGentleIntroductionToGIS.pdf

## PostGIS:
* http://www.bostongis.org/PrinterFriendly.aspx?content_name=postgis_tut01
* http://www.postgresonline.com/