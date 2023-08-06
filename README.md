piwigo_import_tree
==================

This is a script that can be run to import a tree structure of albums of images into Piwigo. Starting with a specified directory, this and all the sub-directories in the tree structure are written as albums in Piwigo with all their JPEG images and Descriptions.

Fork of original script which can be found on Piwigo extensions page: http://piwigo.org/ext/extension_view.php?eid=606

Version history
---------------

v0.1
  - Initial version

v1.0
  - Compatible with Piwigo 2.6
  - Write a local cache in `.piwigo_import_tree.txt` files
  - new options: `--only_write_cache`, `--reload_properties`, `--debug`, `--short_lines`

v1.1
  - Github fork
  - for albums containing many images hitting the page limit all images are now read (via pagination)

Requirements
------------

The script is run using Perl. It requires perl-JSON extension

Usage
-----

The script is run with variables supplied as follows:

```
 perl piwigo_import_tree.pl
         --base_url=http://address/of/your/piwigo
         --user=admin_username
         --password=??
         --directory="my photos directory"
         [--parent_album_id=NN]
         [--quiet]
         [--only_write_cache]
         [--reload_properties]
         [--debug]
         [--short_lines]
```

Where:

* `--user=admin_username` is an administrator on your gallery
* `--directory="my photos directory"` is the full or relative Path Name to the top of the Album Tree. (If the top directory contains spaces, surround it in double quotes)  
* `--parent_album_id=NN` is the internal Piwigo Album ID of the parent album. This parameter is optional: if there is no parent album for the albums being loaded, omit this parameter

Photo titles
------------

In addition, if there is a record named *descript.ion present in the directory, (such as that produced from Fotopic), this is read and the Caption for each Image is used as the Piwigo Image Title. These entries consist of lines containing the Image Filename and Caption, separated by a Tab. The default name of this record can be changed to another text file name.

Run many times to synchronize
-----------------------------

The most useful part of this facility is that you can add more albums, images and descriptions to the tree structure and then re-run the script when just the new images will be transferred.

Šemík's notes
-------------
Modified for importing data from My Photo Gallery 4.0 by fuzzymonkey.org, which is looong time unsuported. 

Usage:
```
cd foto
find . -maxdepth 1 -mindepth 1 -type d -exec perl ~/proj/piwigo-import-tree/piwigo_import_tree.pl -base_url=https://piwigo.galery.somewhere/ --user=admin --password=password --directory="{}" --reload_properties \;
```

To support some HTML tags i did [a few modifications to API](import.patch) which should be reverted after import.
