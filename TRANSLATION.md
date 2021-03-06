# How to manage translations of wallabag

This guide will describe procedure of translation management of wallabag web application.

All translation are made using [gettext](http://en.wikipedia.org/wiki/Gettext) system and tools. 

You will need [Poedit](http://www.poedit.net/download.php) editor to update, edit and create your translation files comfortably. In general, you can handle translations also without it: all can be done using gettext tools and your favorite plain text editor only. This guide, however, describes editing with Poedit. If you want to use gettext only, pls refer to xgettext manual page to update po files from sources (see also how it is used by Poedit below) and use msgunfmt tool to compile .mo files manually.  

You need to know, that translation phrases are stored in **".po"** files (for example: `locale/pl_PL.utf8/LC_MESSAGES/pl_PL.utf8.po`), which are then complied in **".mo"** files using **msgfmt** gettext tool or by Poedit, which will run msgfmt for you in background. 

**It's assumed, that you have wallabag installed locally on your computer or on the server you have access to.**

## To change existing translation you will need to do:

### 1. Clear cache
You can do this using **http://your-wallabag-host.com/?empty-cache** link (replace http://your-wallabag-host.com/ with real url of your wallabag application)

OR

from command line:
go to root of your installation of wallabag project and run next command:

`rm -rf ./cache/*`

(this may require root privileges if you run, for example Apatche web server with mod_php)

### 2. Generate php files from all twig templates
Do this using next command:

`php ./locale/tools/fillCache.php`

OR

from your browser: **http://your-wallabag-host.com/locale/tools/fillCache.php** (this may require removal of .htacces file in locale/ directory).

### 3. Configure your Poedit
Open Poedit editor, open Edit->Preferences. Go to "Parsers" tab, click on PHP and press "Edit" button. Make sure your "Parser command:" looks like

`xgettext --no-location --force-po -o %o %C %K %F`

Usualy it is required to add "--no-location" to default value. 

### 4. Open .po file you want to edit in Poedit and change it's settings
Open, for example `locale/pl_PL.utf8/LC_MESSAGES/pl_PL.utf8.po` file in your Poedit.

Go to "Catalog"->"Settings..." menu. Go to "Path" tab and add path to wallabag installaion in your local file system. This step can't be ommited as you will not be able to update phrases otherwise.

You can also check "project into" tab to be sure, that "Language" is set correctly (this will allow you to spell check your translation).

### 5. Update opened .po file from sources
Once you have set your path correctly, you are able to update phrases from sources. Press "Update catalog - synchronize it with sources" button or go to "Catalog"->"Update from sources" menu.

As a result you will see confirmation popup with two tabs: "New strings" and "Obsolete strings". Pls review and accept changes (or press "Undo" if you see too many obsolete strings, as Poedit will remove them all - in this case please make sure all previous steps are performed w/o errors).

### 6. Translate and save your .po file
If you have any dificulties on this step, please consult with Poedit manual.
Every time you save your .po file, Poedit will also comple appropriate .mo file by default (of course, if not disabled in preferences).

So, you are almost done.

### 7. Clear cache again
This step may be required if your web server runs php scripts in name of, say, www user (i.e. Apache with mod_php, not cgi).


##To create new translation 
Please simple create appropriate directories in locale folder and perform all steps, described above. Instead of opening an existing file just create new one.

