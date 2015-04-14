# Useful Tips #

## Simplifying Tagging With Properties ##

Thanks to [ubernostrum](http://code.google.com/u/ubernostrum/) for this tip.

When using tags on a model, it's fairly easy to create a simple interface for retrieving and setting  them by putting a property on the model:

```
def _get_tags(self):
    return Tag.objects.get_for_object(self)

def _set_tags(self, tag_list):
    Tag.objects.update_tags(self, tag_list)

tags = property(_get_tags, _set_tags)
```

So suppose you have a blog entry model with tags, and you add the above to it; now you could do:

```
e = Entry.objects.get(pk=12)
e.tags # prints the tag list
e.tags = 'foo bar' # now the Entry is tagged with 'foo' and 'bar'
```