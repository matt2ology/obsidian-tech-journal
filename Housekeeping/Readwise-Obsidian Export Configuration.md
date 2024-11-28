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

> RDWSE: Readwise

```plaintext
RDWSE - {{author}} - {{title}}
```

## Page Title

```plaintext
## {{ full_title }}
```

## Page Metadata

```plaintext
{% if image_url -%}

![rw-book-cover]({{image_url}})

{% endif -%}
{% if url -%}
- URL: {{url}}
{% endif -%}
```

## Highlights Header

```plaintext
{% if is_new_page %}
## Highlights
{% elif has_new_highlights -%}
## New highlights added {{date|date('F j, Y')}} at {{time}}
{% endif -%}
```

## Highlight

```plaintext
### {% if highlight_location != "View Highlight" and highlight_location != "View Tweet" %}{{highlight_location}}{% else %}id{{highlight_id}}{% endif %}

> {{ highlight_text }}
{% if highlight_note %}
- \[note\]: {{ highlight_note }}
{% endif %}
{% if highlight_location and highlight_location_url %} * [{{highlight_location}}]({{highlight_location_url}}){% elif highlight_location %} ({{highlight_location}}){% endif %}
```

Alternate Prototype

```plaintext
### {% if highlight_location != "View Highlight" and highlight_location != "View Tweet" %}{{highlight_location}}{% else %}id{{highlight_id}}{% endif %}
{% if highlight_note %}
- \[Initial thoughts\]: {{ highlight_note }}
{% endif %}

> {{ highlight_text }} {% if highlight_location and highlight_location_url %}
> \- {{author}} [({{highlight_location}})]({{highlight_location_url}}){% elif highlight_location %} ({{highlight_location}}){% endif %}


{% if category == "books" %}
    {% if authors|length == 1 %}
        [({{ authors[0].last_name }} {{ highlight_location }})]({{ highlight_location_url }})
    {% elif authors|length == 2 %}
        [({{ authors[0].last_name }} and {{ authors[1].last_name }} {{ highlight_location }})]({{ highlight_location_url }})
    {% elif authors|length > 2 %}
        [({{ authors[0].last_name }} et al. {{ highlight_location }})]({{ highlight_location_url }})
    {% else %}
        [("{{ shortened_title }}" {{ highlight_location }})]({{ highlight_location_url }})
    {% endif %}
{% elif category == "articles" %}
    {% if authors|length == 1 %}
        [({{ authors[0].last_name }})]({{ highlight_location_url }})
    {% else %}
        [("{{ shortened_title }}")]({{ highlight_location_url }})
    {% endif %}
{% elif "youtube.com" in document.domain %}
    {% if author_mentioned %}
        {{ author_last_name }} argues that the key to a perfect omelette is low heat ({{ timestamp }})
    {% else %}
        "{{ shortened_title }}" suggests using unsalted butter ({{ timestamp }})
    {% endif %}
{% endif %}
```

## YAML front matter

```plaintext
title: {{title}}
note-type: Reference
note-created-on: {{date}}
{% if url -%}
source: <{{url}}>
{% else %}
source: {{source}}
{% endif -%}
author: {{author}}
published-date: {{published_date}}
tags: readwise, inbox-review-later/{{category}}
```
