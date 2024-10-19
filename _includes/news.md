## News

<div class="news-container" style="max-height: 400px; overflow-y: auto;">
{% assign news_items = site.data.news | sort: 'date' | reverse %}
<ul>
{% for item in news_items limit:10 %}
<li><strong>[{{ item.date | date: "%m/%Y" }}]</strong> {{ item.content }}</li>
{% endfor %}
{% if news_items.size > 10 %}
{% for item in news_items offset:10 %}
<li><strong>[{{ item.date | date: "%m/%Y" }}]</strong> {{ item.content }}</li>
{% endfor %}
{% endif %}
</ul>
</div>