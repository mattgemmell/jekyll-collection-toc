---
permalink: /YOUR-COLLECTION-URL/collated/
title: "YOUR COLLECTION TITLE — Collated"
---

{% include collection_toc.html collection_label="YOUR COLLECTION" collated=true %}

{% assign the_collection = site.collections | where: "label", "YOUR COLLECTION" | first %}
{% assign the_content = "" %}
{% for doc in the_collection.docs %}
	{% capture doc_content %}
<h1 id="{{ doc.url | slugify }}">{{ doc.title }}</h1>

{{ doc.content | markdownify }}

<hr />
	{% endcapture %}
	{% assign the_content = the_content | append: doc_content %}
{% endfor %}

{% assign all_urls = the_collection.docs | map: "url" %}
{% for the_url in all_urls %}
	{% capture url_href %}href="{{ the_url }}"{% endcapture %}
	{% capture anchor_href %}href="#{{ the_url | slugify }}"{% endcapture %}
	{% assign the_content = the_content | replace: url_href, anchor_href %}
{% endfor %}

{{ the_content }}
