## Backwards-incompatible changes since version 0.1 ([Revision 79](https://code.google.com/p/django-tagging/source/detail?r=79)) ##

### [Revision 114](https://code.google.com/p/django-tagging/source/detail?r=114) (12th January, 2008) ###

Flexible multi-word tags landed in SVN trunk - this was used as an opportunity to clean up some long-standing untidiness. Other backwards-incompatible changes:

  * The `Tag` and `TaggedItem` models **no longer set the `db_table` properties** in their inner `Meta` class - this means that unless you put the override back in yourself, **you'll have to rename your database tables** to `tagging_tag` and `tagging_taggeditem`, respectively. These were a hangover from when SQL queries were originally being written by hand - the appropriate table names are now plugged in to queries using each model's `Options` (`_meta`).

  * `tagging.utils.get_tag_name_list` has been removed, as have all regular expressions related to tag input/validation.

## Backwards-incompatible changes since version 0.2 ([Revision 122](https://code.google.com/p/django-tagging/source/detail?r=122)) ##

### [Revision 130](https://code.google.com/p/django-tagging/source/detail?r=130) (21st January, 2008) ###

`TaggedItemManager`'s methods now accept a `queryset_or_model` argument instead of a `model` argument, so you'll need to change your code if you were using `model` as a keyword argument.

The `tagged_object_list` generic view's `model` argument has also been renamed to `queryset_or_model`.