---
layout: default
---

# 我的生活记录

欢迎来到我的小天地。

这里记录生活、旅行、照片和一些随想。

---

## 最新文章

{% for post in site.posts %}
### {{ post.title }}

{{ post.date | date: "%Y年%m月%d日" }}

{{ post.excerpt }}

[阅读全文 →]({{ post.url | relative_url }})

---

{% endfor %}

## 关于我

一个生活在加拿大的普通人。

喜欢记录生活，也喜欢保存一些值得回忆的东西。

欢迎常来看看。
