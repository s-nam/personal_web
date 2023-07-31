<!-- ---
layout: page
title: Thoughts (Written in Korean)
parent: About me2
nav_order: 2
--- -->
Contents

{% assign thoughts_collection = site.collections | where: 'label', 'thoughts' | first %}
{% assign categories_order = thoughts_collection.categories-order %}

{% assign groups_by_category = site.thoughts | group_by: "category" %}
{% for cate in categories_order %}
    {% assign currentCate = groups_by_category | where: 'name', cate | first %}
<div class="category_wrapper">
    <div class="category">{{ currentCate.name }}</div>
    <ul>
    {% assign items_in_currentCate = currentCate.items | sort: "date" | reverse %}
    {% for item in items_in_currentCate %}
        <li class="collaped">
            <a href="{{ site.baseurl }}{{ item.url }}">
            {% if item.url == navurl %}
                <u>{{ item.title }}</u>
            {% else %}
                {{ item.title }}
            {% endif %}
            </a>
        </li>
    {% endfor %}
    </ul>
</div>
{% endfor %}