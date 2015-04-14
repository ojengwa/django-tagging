# What's It All About? #

  * `django-tagging` can't be all things to all people - do we really want del.icio.us-style "do what you want, I'll make quotes part of your actual tags" (which happens to be easier to implement), or a flickr style "no you can't have `___` as a tag"? Is there a happy medium somewhere?

# Tag Synonyms #

Changes required to implement tag synonyms.

## Utilities ##

  * Create a utility function to normalise tag names - remove all non-word characters, strip and lowercase.
  * Simplify `get_tag_name_list`, splitting on a defined separator character, stripping and removing any empty strings from the results. _If the separator character is not the space character, does this give us multiword tags for free?_
  * `get_tag_list` and `get_tag` need to use normalised names for name-based tag lookups.
  * Update validation functions to check normalised tag names - check that normalised tag names are non-zero length.

## Models & Managers ##

  * Add a field to `TaggedItem` to hold the tag entered by the user - how about `user_tag`?
  * Update `TagManager.update_tags` to check against the normalised tag name and add  `user_tag` when creating `TaggedItem`s.
  * Update `TagManager.get_for_object` to also return the `user_tag` which was used - the `extra` method looks like the way to go, since we're already joining onto the `tagged_item` table for `content_type` and `object_id`.
  * Remove the `FORCE_LOWERCASE_TAGS` setting, as normalised tag names should take care of the main reason you'd want to use it.

## Fields ##

  * `tagging.fields.TagField` needs to display user tags for editing, joined with the defined separator character.

## Open Questions ##

  * How could we implement this and still allow nifty things like use of Unicode non-word characters for their graphical fit (e.g. using a musical note character to tag music)?
  * Are we still trying to be too restrictive? This wouldn't allow things like tagging with star ratings. Do we care if someone wants to tag something with 19 underscores?