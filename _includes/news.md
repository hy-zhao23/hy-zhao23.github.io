## News
{% assign news_items = site.data.news %}

{% assign all_years = '' | split: '' %}
{% for item in news_items %}
  {% assign year = item.date | date: "%Y" %}
  {% assign all_years = all_years | push: year %}
{% endfor %}
{% assign sorted_years = all_years | uniq | sort | reverse %}

<div class="news-container{% if news_items.size > 10 %} scrollable{% endif %}">
  <ul>
  {% for year in sorted_years %}
    {% assign year_items = '' | split: '' %}
    {% for item in news_items %}
      {% assign item_year = item.date | date: "%Y" %}
      {% if item_year == year %}
        {% assign year_items = year_items | push: item %}
      {% endif %}
    {% endfor %}
    {% assign sorted_year_items = year_items | sort: "date" | reverse %}
    {% for item in sorted_year_items %}
      <li><strong>[{{ item.date | date: "%m/%Y" }}]</strong> {{ item.content }}</li>
    {% endfor %}
  {% endfor %}
  </ul>
</div>

<style>
  .news-container {
    margin-bottom: 40px;
  }
  .news-container.scrollable {
    max-height: 270px;
    overflow-y: auto;
  }
  .news-container.scrollable::-webkit-scrollbar {
    width: 6px;
  }
  .news-container.scrollable::-webkit-scrollbar-track {
    background: #f1f1f1;
  }
  .news-container.scrollable::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 3px;
  }
  .news-container.scrollable::-webkit-scrollbar-thumb:hover {
    background: #555;
  }
</style>