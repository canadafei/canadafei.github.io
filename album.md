---
layout: default
title: 我的图片集
---

<style>
.album-page {
  margin-top: 30px;
}

.album-page-title {
  margin-bottom: 40px;
}

.album {
  margin-bottom: 60px;
  padding-bottom: 45px;
  border-bottom: 1px solid #e5e5e5;
}

.album h2 {
  margin-bottom: 6px;
}

.album-date {
  color: #888;
  font-size: 14px;
  margin-bottom: 20px;
}

.album-photos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 14px;
}

.album-photos img {
  width: 100%;
  height: 230px;
  object-fit: cover;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0,0,0,0.12);
  transition: transform 0.2s;
}

.album-photos img:hover {
  transform: scale(1.02);
}

.album-empty {
  color: #888;
}


/* 图片放大 */

.photo-lightbox {
  display: none;
  position: fixed;
  z-index: 9999;
  inset: 0;
  background: rgba(0,0,0,0.92);
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
  top: 15px;
  right: 30px;
  color: white;
  font-size: 42px;
  cursor: pointer;
}


/* 手机 */

@media (max-width: 700px) {

  .album-photos {
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }

  .album-photos img {
    height: 170px;
  }

}

@media (max-width: 420px) {

  .album-photos {
    grid-template-columns: 1fr;
  }

  .album-photos img {
    height: auto;
  }

}
</style>


<div class="album-page">

<h1 class="album-page-title">
我的图片集
</h1>


{% assign albums = site.albums | sort: "date" | reverse %}

{% if albums.size > 0 %}

{% for album in albums %}

<article class="album">

<h2>
{{ album.title }}
</h2>

<div class="album-date">
{{ album.date | date: "%Y年%m月%d日" }}
</div>


{% if album.images %}

<div class="album-photos">

{% for photo in album.images %}

{% if photo.image %}

<img
  src="{{ photo.image | relative_url }}"
  alt="{{ album.title }}"
  loading="lazy">

{% endif %}

{% endfor %}

</div>

{% else %}

<div class="album-empty">
这个图片集还没有照片。
</div>

{% endif %}

</article>

{% endfor %}

{% else %}

<p>目前还没有图片集。</p>

{% endif %}

</div>


<!-- 图片放大 -->

<div class="photo-lightbox" id="photoLightbox">

<span
  class="photo-lightbox-close"
  onclick="closePhoto()">
×
</span>

<img id="lightboxImage" src="" alt="">

</div>


<script>

document.addEventListener("DOMContentLoaded", function() {

  const images = document.querySelectorAll(".album-photos img");

  images.forEach(function(img) {

    img.addEventListener("click", function() {

      document.getElementById("lightboxImage").src = this.src;

      document.getElementById("photoLightbox").style.display = "flex";

    });

  });

});


function closePhoto() {

  document.getElementById("photoLightbox").style.display = "none";

  document.getElementById("lightboxImage").src = "";

}


document.getElementById("photoLightbox").addEventListener(
  "click",
  function(e) {

    if (e.target === this) {
      closePhoto();
    }

  }
);


document.addEventListener("keydown", function(e) {

  if (e.key === "Escape") {
    closePhoto();
  }

});

</script>
