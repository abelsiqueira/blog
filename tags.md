---
layout: page
title: Tags
permalink: /tags/
---

{% assign tags = site.data.tags | sort: 'count' | reverse %}

<div style="height: 300px;" id="tagcloud"> </div>

<hr>

<div id="taglist">
<h3 id="taglisth3"></h3>
</div>

<script>
var words = [
	{% for tag in tags %}
		{text: "{{ tag.name }}",
		weight: {{ tag.count }},
    html: { class: "cloud-word" },
		handlers: {click: function() {
document.getElementById('taglist').innerHTML = '<h3 id="taglisth3">{{ tag.name }} posts</h3>\
<ul class="post-list-compact">\
{% for post in site.posts %} {% for t in post.tags %} {% if t == tag.key %}\
<li> <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">\
{{ post.title }} </a> <span class="post-list-date">\
{{ post.date | date: "%d %b, %Y" }}</span> </li>\
{% endif %} {% endfor %} {% endfor %} </ul>';
		}},
		link: "#taglisth3"
	},
	{% endfor %}
];
$(function() {
	$('#tagcloud').jQCloud(words, {
		autoResize: true,
    classPattern: null,
    colors: ["#000", "#111", "#222", "#333", "#444", "#555", "#666", "#777",
    "#888", "#999", "#aaa"],
    fontSize: { from: 0.1, to: 0.02 }
	});
});

</script>