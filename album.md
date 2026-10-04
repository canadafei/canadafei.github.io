---
layout: page
title: "我的相册"
permalink: /album/
---

# 📷 我的相册

记录生活，保存记忆。

<style>
.photo-wall {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 18px;
  margin-top: 30px;
}

.photo-wall img {
  width: 100%;
  height: 220px;
  object-fit: cover;
  border-radius: 10px;
  display: block;
  box-shadow: 0 2px 10px rgba(0,0,0,0.12);
}

.photo-wall img:hover {
  transform: scale(1.02);
  transition: 0.2s;
}
</style>

## 🍁 加拿大生活

<div class="photo-wall">

<img src="/images/autumn.jpg" alt="加拿大秋天">

</div>
