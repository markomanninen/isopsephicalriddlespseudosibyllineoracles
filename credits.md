# Credits

### About pictures

I have published all my own photos and illustrations with the Creative Commons license<!-- cite author="wikipedia.org" title="Creative Commons license" date="" location="" type="website" href="http://en.wikipedia.org/wiki/Creative_Commons_license" -->. I believe that is the best way to keep creative work and research hassle free and to be able to be enjoyed by everyone. The pictures and the figures below that have no copyright notice are my own and they are free to be used with a mention *&copy; Marko Manninen* accompanied by a reference to the original work.

<ul class="pictures">
{% for picture in book.pictures %}<li>{{ picture }}</li>{% endfor %}
</ul>

{% include 'footnotes.md' %}
