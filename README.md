Constructor-IO Python Client
=====

A Python package for the [Constructor.io API](http://constructor.io/docs).  Constructor.io provides a lightning-fast, typo-tolerant autocomplete service that ranks your users' queries by popularity to let them find what they're looking for as quickly as possible.

Installation
===

With pip:

    pip install constructor-io

Note that you are writing `constructor-io` with a hyphen, as opposed to actually in your code, where you will be writing `constructor_io` with an underscore!

API
===

All of these are basically one step away from the RESTFUL interface and the implementation is dead simple.

Usage
---

Create a new instance with your API token and autocomplete key:

```python
from constructor_io import ConstructorIO
constructor_instance = ConstructorIO(
  apiToken="your API token",
  autocompleteKey="your autocomplete key"
)
# both of these are available at https://constructor.io/dashboard
```

If you ONLY want to query, then you can put in `None` for `apiToken`.

Querying
---

To query the autocomplete from your backend:

(If you are making a website, use our Javascript front-end client, it will be much faster for your users. Like, seriously.)

```python
>>> suggestions = constructor_instance.query("a")
>>> suggestions
{
  "suggestions": [
    {"value": "ambulance"},
    {"value": "aardvark"},
    {"value": "Aachen"}
  ]
}
```

Changing the index
---

All of these methods return `True` if successful and raise an `IOError` with a description of what happened if not successful.

To add an item to your autocomplete index:
    
```python
>>> constructor_instance.add(
>>>    item_name = "boinkamoinka",
>>>    autocomplete_section = "Search Suggestions"
>>> )
True
```

To remove an item from your autocomplete index:
    
```python
>>> constructor_instance.remove(
>>>     item_name = "boinkamoinka",
>>>     autocomplete_section = "Search Suggestions"
>>> )
True
```

To modify an item in your autocomplete index:

```python
>>> constructor_instance.modify(
>>>     item_name = "boinkamoinka",
>>>     new_item_name = "some new name",
>>>     suggested_score = 100,
>>>     autocomplete_section = "Search Suggestions"
>>> )
True
```

Tracking
---

You can also track behavioral data to improve the rankings of your results.  There are three tracking methods for search, click_through, and conversion:

All of these methods return `True` if successful and raise an `IOError` with a description of what happened if not successful.

Tracking a search event:

```python
>>> constructor_instance.track_search(
>>>   term="xyz",
>>>   num_results=302,
>>>   autocomplete_section="products_autocomplete"
>>> )
True
```

Tracking a click-through event:

```python
>>> constructor_instance.track_click_through(
>>>   term="xyz",
>>>   item="alphabet soup",
>>>   autocomplete_section="products_autocomplete"
>>> )
True
```

Tracking a click-through event:

```python    
>>> constructor_instance.track_conversion(
>>>   term="xyz",
>>>   item="alphabet soup",
>>>   autocomplete_section="products_autocomplete"
>>> )
True
```
