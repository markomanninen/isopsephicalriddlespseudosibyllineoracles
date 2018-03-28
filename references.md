# References

### Websites

 I have used Wikipedia extensively so that people interested in the different topics can easily find more information and relevant resources by following provided links. Wikipedia pages are not meant as an evidence for my theories, but purely for additional information.

* [wikipedia.org](http://wikipedia.org)
* [wikimedia.org](http://wikimedia.org)
* [wiktionary.org](http://wiktionary.org)
* [etymonline.com](http://etymonline.com)

{% if book.citations %}

### Citations

<ul class="references">
{% for cite in book.citations %}<li>{{ cite.replace('.md', '.html') }}</li>{% endfor %}
</ul>
{% endif %}
