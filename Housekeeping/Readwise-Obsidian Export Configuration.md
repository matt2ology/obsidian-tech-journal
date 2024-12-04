---
aliases:
note-created-on: 2024-11-26 (Tuesday) 10:55PM
note-type: Housekeeping
UID: 20241126T2255
tags:
related-notes:
  - "[[Obsidian Tech Journal Dependencies]]"
---

# Readwise-Obsidian Export Configuration

## File name

> Readwise: `RDWSE`

```Jinja2
RDWSE - {{author|truncate(120)}} - {{title|replace(""","")|replace(""","")|replace("'","")|replace("'","")|truncate(127)}}
```

Weird characters or overly-long file names don't break dropbox or git, since Readwise doesn't natively sanitize things. \- An idea taken from [Eleanor's Readwise Settings](https://gist.github.com/eleanorkonik/1f0586fe13d98f1dbf18ec72b00bf37d)

## Page Title

```Jinja2
## {{ full_title }}
```

## Page Metadata

```Jinja2
{% if image_url -%}

![rw-book-cover]({{image_url}})

{% endif -%}
{% if url -%}
**Link:** [{{full_title}}]({{url}})
{% endif -%}
```

## Highlights Header

```Jinja2
{% if is_new_page %}
## Highlights
{% elif has_new_highlights -%}
## New highlights added {{date|date('F j, Y')}} at {{time}}
{% endif -%}
```

## Highlight

```Jinja2
{% if highlight_location == "View Highlight" %}### id{{ highlight_id }}{% elif highlight_location == "View Tweet" %}### id{{ highlight_id }}{% else %}### {{highlight_location}}{% endif %}

> {{ highlight_text }} {% if highlight_location and highlight_location_url %}
> \- [({{highlight_location}})]({{highlight_location_url}}){% elif highlight_location %}({{highlight_location}}){% endif %}{% if highlight_note %}

**Initial thought or note on:** {% if highlight_location and highlight_location_url %}[({{highlight_location}})]({{highlight_location_url}}){% elif highlight_location %}({{highlight_location}}){% endif %}
{{ highlight_note }}
{% endif %}
```

### Readable Breakdown of the Highlights Block

> Display highlight location or a fallback ID if it's a default value
>
> > ```Jinja2
> > {% if highlight_location == "View Highlight" %}
> >     ### id{{ highlight_id }}
> > {% elif highlight_location == "View Tweet" %}
> >     ### id{{ highlight_id }}
> > {% else %}
> >     ### {{ highlight_location }}
> > {% endif %}
> > ```
>
> Display the highlight text, followed by an optional location link or text
>
> > ```Jinja2
> > \> {{ highlight_text }}
> > {% if highlight_location and highlight_location_url %}
> >     \> \- \[({{ highlight_location }})\]({{ highlight_location_url }})
> > {% elif highlight_location %}
> >     \> \- ({{ highlight_location }})
> > {% endif %}
> > ```
>
> Display a note, prefixed by the location link or text if available
>
> > ```Jinja2
> > {% if highlight_note %}
> >     **Initial thought or note on:**
> >     {% if highlight_location and highlight_location_url %}
> >         \[({{ highlight_location }})\]({{ highlight_location_url }})
> >     {% elif highlight_location %}
> >         ({{ highlight_location }})
> >     {% endif %}
> >         {{ highlight_note }}
> > {% endif %}
> > ```

## YAML front matter

```Jinja2
title: {{title}}
note-type: Reference
note-created-on: {{date}}
{% if url -%}
source: {{url}}
{% else %}
source: {{source}}
{% endif -%}
author: {{author}}
published-date: {{published_date}}
tags: readwise, inbox-review-later/{{category}}
processed: false
```

- `processed` means if the reference note has been **processed** into a literature note (i.e. a note on a reference note written in my own words)
