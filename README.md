Events plugin
=============

This plugin allows you to put events in your content via metadata. An
iCal file is generated containing all events.

This plugin is based on the events plugin hosted at the official [pelican-plugins](https://github.com/getpelican/pelican-plugins/tree/master/events) repository.

Customizing Makerspace Esslingen
--------------------------------
We have done some modifications on the official version of the plugin
    - introduced a new setting `metadata_field_for_summary` to control which metadata field should be used as event summary text for events in the ics file
    - calendar.ics file and events_list.html do not include events from draft pages anymore
    - added an upcoming_events field to the context data of a page template for rendering current and future events only


Dependencies
------------

This plugin depends on the `icalendar` package, which can be installed
using APT, DNF/YUM or pip:

```sh
pip install icalendar
```


Settings
--------

You can define settings with the `PLUGIN_EVENTS` variable:

```python
PLUGIN_EVENTS = {
    'metadata_field_for_summary': 'summary'
    'ics_fname': 'calendar.ics',
}
```

Settings:
- `ics_fname`: Where the iCal file is written
- `metadata_field_for_summary`: Metadata field from articles to be used as summary text for events in the ics file. Default: 'summary'


Usage
-----

You can use the following metadata in your content:
- `event-start`: When the event will start in "YYYY-MM-DD hh:mm"
- `event-end`: When the event will stop in "YYYY-MM-DD hh:mm"
- `event-duration`: The duration of the event [1]
- `event-location`: Where the event takes place

[1] To specify the event duration, use a number followed by a time unit:
- `w`: weeks
- `d`: days
- `h`: hours
- `m`: minutes
- `s`: seconds


Examples
--------

Example in reST format:
```reST
:event-start: 2015-01-21 10:30
:event-duration: 2h
:event-location: somewhere
```

Example in Markdown format:
```markdown
Event-start: 2015-01-21 10:30
Event-duration: 2h
Event-location: somewhere
```


Dedicated events overview 
-------------------------

###

### Events overview

To generate a single overview webpage for displaying a sorted list of events:

- change pelicanconf.py
  - add the 'events_list' template to DIRECT_TEMPLATES=

    ```DIRECT_TEMPLATES = ['index', 'tags', 'categories', 'authors', 'archives', 'events_list']```

  - (optional) set the name of the target html file that should be generated. Default: 'events_list.html'

    ```EVENTS_LIST_SAVE_AS = 'my_great_list_of_events.html'```

### Upcoming events overview

To generate a single overview webpage for displaying a sorted list of current and upcoming events only:

- change pelicanconf.py
    - add the 'upcoming_events_list' template to DIRECT_TEMPLATES=

        ```DIRECT_TEMPLATES = ['index', 'tags', 'categories', 'authors', 'archives', 'upcoming_events_list']```

    - (optional) set the name of the target html file that should be generated. Default: 'upcoming_events_list.html'

        ```UPCOMING_EVENTS_LIST_SAVE_AS = 'my_great_list_of_upcoming_events.html'```

### List of events on pages

To be able to display a sorted overview of events within one or more pelican pages:

- Copy the `events_list_page.html` template under the templates directory of your theme
- Create one or more pages using this template, for example in `content/pages/events_list.rst`
- Include the following metadata in your content:
```reST
Title of events list page
###########
:slug: events-list
:summary:
:template: events_list_page
```

Title, slug and content of the renered pages is controlled by the various files located in the content/pages/ directory.

### List of upcoming events on pages

To be able to display a sorted overview of current and upcoming events within one or more pelican pages:

- Copy the `upcoming_events_list_page.html` template under the templates directory of your theme
- Create one or more pages using this template, for example in `content/pages/events_list.rst`
- Include the following metadata in your content:
```reST
Title of upcoming events list page
###########
:slug: upcoming-events-list
:summary:
:template: upcoming_events_list_page
```

Title, slug and content of the renered pages is controlled by the various files located in the content/pages/ directory.
