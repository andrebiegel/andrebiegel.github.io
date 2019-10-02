---
layout: page
title: Projects
permalink: /projects/
---
<ul class="post-list">
{%- for category in site.categories -%}
    {%- if category[0] == 'Projects' -%}
        {% for post in category[1] %}
        <li>
            {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
            <span class="post-meta"> Tags: {{ post.tags | join: ' | ' }}</span>
            <h4>
            <a class="post-link" href="{{ post.url | relative_url }}">
                {{ post.title | escape }}
            </a>
            </h4>
            {%- if site.show_excerpts -%}
            {{ post.excerpt }}
            {%- endif -%}
        </li>
        {%- endfor -%}
    {%- endif -%}
{%- endfor -%}
</ul>