---
layout: default
---

<h1>测试</h1>

<p>文章总数：{{ site.posts.size }}</p>

<p>分页文章数：{{ paginator.posts.size }}</p>

<p>总页数：{{ paginator.total_pages }}</p>

{% for post in site.posts %}
<article>
    <h2>
        <a href="{{ post.url | relative_url }}">
            {{ post.title }}
        </a>
    </h2>

    <p>{{ post.date | date: "%Y-%m-%d" }}</p>
</article>
{% endfor %}
