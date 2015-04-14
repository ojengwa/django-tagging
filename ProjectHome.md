A generic tagging application for Django projects, which allows association of a number of tags with any `Model` instance and makes retrieval of tags simple.

The [CHANGELOG](http://django-tagging.googlecode.com/svn/trunk/CHANGELOG.txt) is kept up to date with notable commits and the latest version of this application's documentation, in [reStructuredText](http://docutils.sourceforge.net/rst.html) format, is always available in its [overview.txt](http://django-tagging.googlecode.com/svn/trunk/docs/overview.txt) file or [rendered nicely](http://api.rst2a.com/1.0/rst2/html?uri=http://django-tagging.googlecode.com/svn/trunk/docs/overview.txt). **Note:** this documentation is for the SVN trunk version - it may differ from the documentation for the packaged release.

## Version 0.3 Features ##

Version 0.3 was released on 22nd August 2009, packages from [revision 158](https://code.google.com/p/django-tagging/source/detail?r=158) in Subversion.

Works on 1.0 and other fixes. This release was made to provide a 1.0 compatible release (since one hasn't been made in over a year). More fixes will come in 0.4.

## Version 0.2 Features ##

Version 0.2 was released on 12th January 2008, packaged from [revision 122](https://code.google.com/p/django-tagging/source/detail?r=122) in Subversion.

Version 0.2.1, a bugfix release, was released on 16th January 2008 - this fixes a bug with space-delimited tag input. Duplicates were not being removed and the resulting list of tag names was not sorted.

If you're upgrading from version 0.1, please see the BackwardsIncompatibleChanges wiki page.

Requires a recent SVN checkout of Django's trunk.

  * Multi-word tags, which adapt to the tag input given - a string of tags which doesn't contain any loose commas is treated as a simple space-delimited list. Otherwise, if a comma is present, tag input will be comma delimited, which allows for easy entry of multi-word tags. Phrases may also be quoted with "double quotes", which may contain commas as part of the tag names they define.
  * Retrieval of instances of a particular `Model` based on their tags - supports lookups for single tags, intersections (tag1 AND tag2 AND tag3) and unions (tag1 OR tag2 OR tag 3).
  * Retrieval of tags and their usage counts for a particular `Model`, or a subset of it , specified using Django's [field lookups](http://www.djangoproject.com/documentation/db-api/#field-lookups).
  * Find related tags based on their usage for a particular `Model`, [del.icio.us style](http://del.icio.us/insin/webdev%2Baccessibility).
  * Restriction of tags returned from tag usage and related tag methods to those which have been used a minimum number of times.
  * Retrieval of instances of any `Model` which share tags with a given instance of any other `Model`.
  * Flexible specification of lists of tags for manager method  - names, lists of names, lists of ids, `Tag` `QuerySet`s, and list of `Tag` objects are all accepted.
  * Calculation of tag clouds with logarithmic or linear distribution over any number of font sizes, given any list of tags which have `count` attributes.
  * Templatetags for working with tags - retrieve tags for a given object or model, tag clouds for a given model and objects tagged with a given tag.
  * A custom `TagField` field for your Models which makes tagging more natural and allows easy editing and validation of tags in the `django.contrib.admin` application - contributed by Jacob Kaplan-Moss
  * A `TagField` for use with Django's [newforms library](http://www.djangoproject.com/documentation/newforms/) which validates tag input - this will automatically be used on any forms auto-generated from models which have a `TagField` field
  * A generic view for displaying paginated lists of objects for a given model which have a given tag, and optionally related tags too.
  * Tag names can be forced to lowercase before they are saved to the database by adding the appropriate `FORCE_LOWERCASE_TAGS` setting to your project's settings module. This feature defaults to being off.
  * Valid tag name lengths can be reduced from the default (`50`) using the `MAX_TAG_LENGTH` setting

See the [version 0.2 HTML documentation](http://django-tagging.googlecode.com/files/tagging-0.2-overview.html) for more details.

## Download and installation ##

You can install django-tagging with easy\_install or pip:

```
pip install django-tagging
```

or

```
easy_install django-tagging
```

It can also be installed from inside the package using the setup.py script:

```
python setup.py install
```

...and the package will install automatically.

A Windows installer is also available - just download and launch to install the application.

Alternatively, source code can be accessed by performing a [Subversion](http://subversion.tigris.org/) checkout. For example, the following command will check the application's source code out to a `tagging-trunk` directory:

```
svn checkout http://django-tagging.googlecode.com/svn/trunk/ tagging-trunk
```

Add the resulting folder to your [PYTHONPATH](http://docs.python.org/tut/node8.html#SECTION008110000000000000000) or symlink ([junction](http://www.microsoft.com/technet/sysinternals/FileAndDisk/Junction.mspx), if you're on Windows) the `tagging` directory _inside_ it into a directory which is on your PYTHONPATH, such as your Python installation's `site-packages` directory.

You can verify that the application is available on your PYTHONPATH by opening a Python interpreter and entering the following commands:

```
>>> import tagging
>>> tagging.VERSION
(0, 3, None)
```

Keep in mind that the current code in SVN trunk may be different from the packaged release, and may contain bugs and backwards-incompatible changes, as well as new goodies to play with.