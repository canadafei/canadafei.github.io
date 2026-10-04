---
layout: default
---

<style>
.home-post {
  margin-bottom: 55px;
  padding-bottom: 40px;
  border-bottom: 1px solid #e5e5e5;
}

.home-post h2 {
  margin-bottom: 6px;
}

.home-post h2 a {
  text-decoration: none;
  color: inherit;
}

.post-date {
  color: #888;
  font-size: 14px;
  margin-bottom: 18px;
}

.post-content {
  font-size: 17px;
  line-height: 1.9;
}

.post-content img {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  margin: 8px 0;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0,0,0,0.12);
}

.post-photos {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 14px;
  margin: 20px 0;
}

.post-photos img {
  width: 100%;
  height: 260px;
  object-fit: cover;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.2s;
}

.post-photos img:hover {
  transform: scale(1.02);
}

.read-more {
  display: inline-block;
  margin-top: 15px;
  font-weight: bold;
  text-decoration: none;
}

.photo-lightbox {
  display: none;
  position: fixed;
  z-index: 9999;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.9);
  align-items: center;
  justify-content: center;
  padding: 20px;
  box-sizing: border-box;
}

.photo-lightbox img {
  max-width: 95%;
  max-height: 90%;
  object-fit: contain;
}

.photo-lightbox-close {
  position: absolute;
  top: 20px;
  right: 30px;
  color: white;
  font-size: 40px;
  cursor: pointer;
}

@media (max-width: 600px) {
  .post-content {
    font-size: 16px;
  }

  .post-photos {
    grid-template-columns: 1fr;
  }

  .post-photos img {
    height: auto;
  }
}
</style>

# 我的生活记录

欢迎来到我的小天地。

这里记录生活、旅行、照片和一些随想。

---

{% for post in site.posts %}

<article class="home-post">

<h2>
<a href="{{ post.url | relative_url }}">{{ post.title }}</a>
</h2>

<div class="post-date">
{{ post.date | date: "%Y年%m月%d日" }}
</div>

<div class="post-content">

{{ post.content }}

</div>

<p>
<a class="read-more" href="{{ post.url | relative_url }}">
阅读全文 →
</a>
</p>

</article>

{% endfor %}

<div class="photo-lightbox" id="photoLightbox">
  <span class="photo-lightbox-close" onclick="closePhoto()">×</span>
  <img id="lightboxImage" src="" alt="">
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {

  const images = document.querySelectorAll(".post-content img");

  images.forEach(function(img) {
    img.addEventListener("click", function() {
      document.getElementById("lightboxImage").src = this.src;
      document.getElementById("photoLightbox").style.display = "flex";
    });
  });

});

function closePhoto() {
  document.getElementById("photoLightbox").style.display = "none";
}

document.getElementById("photoLightbox").addEventListener("click", function(e) {
  if (e.target === this) {
    closePhoto();
  }
});
</script>

---

## 关于我

一个生活在加拿大的普通人。

喜欢记录生活，也喜欢保存一些值得回忆的东西。

欢迎常来看看。
