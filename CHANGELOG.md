Changelog
=========

### 0.2.1 12th May 2014

Major improvements in the ItemList class.

* All ItemList methods have the option to either return a new ItemList
  instance or edit the current list. The default is to return a new
  instance to reduce side effects.
* Adding a MutableItemList that changes the current list by default.
* Adding ItemList takeRandom().
* Adding ItemList shuffle().

### 0.2.0 31st December 2013

* Adding the Bitmask class for working with a bitwise value system (e.g. user permissions).
* Adding the DotArray merge() function().

### 0.1.2 27th November 2013

* Some small additions to the Inflector/EN word base.
* Adding the locale function to Inflector.

### 0.1.1 27th November 2013

Internal release, adding the RMT build tool.

### 0.1.0 27th November 2013

Initial release. Included classes are:

* Inflector for plurals (currently the only locale is EN).
* DotArray for easy access to nested array values.
* ItemList for manipulating lists.