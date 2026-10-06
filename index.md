<style> .home-post { margin-bottom: 55px; padding-bottom: 40px; border-bottom: 1px solid #e5e5e5; } .home-post h2 { margin-bottom: 6px; } .home-post h2 a { text-decoration: none; color: inherit; } .post-date { color: #888; font-size: 14px; margin-bottom: 18px; } .post-excerpt { font-size: 17px; line-height: 1.9; margin-bottom: 20px; } .post-photos { display: grid; grid-template-columns: repeat(2, 1fr); gap: 14px; margin: 20px 0; } .post-photos img { width: 100%; height: 260px; object-fit: cover; border-radius: 8px; cursor: pointer; box-shadow: 0 2px 8px rgba(0,0,0,0.12); transition: transform 0.2s; } .post-photos img:hover { transform: scale(1.02); } .read-more { display: inline-block; margin-top: 10px; font-weight: bold; text-decoration: none; } /* ========================= 我的图片集按钮 ========================= */ .album-button { display: inline-block; margin: 10px 0 45px 0; padding: 11px 20px; border: 1px solid #ddd; border-radius: 8px; color: inherit; text-decoration: none; font-size: 16px; transition: all 0.2s; } .album-button:hover { background: #f5f5f5; border-color: #ccc; } /* ========================= 分页 ========================= */ .pagination { display: flex; align-items: center; justify-content: center; gap: 25px; margin: 60px 0 70px 0; padding-top: 25px; border-top: 1px solid #e5e5e5; } .pagination a { display: inline-block; padding: 10px 18px; border: 1px solid #ddd; border-radius: 8px; text-decoration: none; color: inherit; transition: all 0.2s; } .pagination a:hover { background: #f5f5f5; border-color: #ccc; } .pagination span { color: #777; font-size: 14px; }   /* ========================= 图片放大 ========================= */   .photo-lightbox { display: none; position: fixed; z-index: 9999; left: 0; top: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); align-items: center; justify-content: center; padding: 20px; box-sizing: border-box; } .photo-lightbox img { max-width: 95%; max-height: 90%; object-fit: contain; } .photo-lightbox-close { position: absolute; top: 20px; right: 30px; color: white; font-size: 40px; cursor: pointer; } /* ========================= 手机 ========================= */ @media (max-width: 600px) { .post-excerpt { font-size: 16px; } .post-photos { grid-template-columns: 1fr; } .post-photos img { height: auto; } .album-button { width: 100%; box-sizing: border-box; text-align: center; } .pagination { gap: 12px; margin: 45px 0 55px 0; } .pagination a { padding: 9px 14px; } } </style>

欢迎来到我的个人网站。

这里记录生活、旅行、照片和一些随想。



<!-- ========================= 文章列表 ========================= -->

{% for post in paginator.posts %}

<article class="home-post">

<h2> <a href="{{ post.url | relative_url }}"> {{ post.title }} </a> </h2>

<div class="post-date"> {{ post.date | date: "%Y年%m月%d日" }} </div>

<div class="post-excerpt"> {{ post.content | strip_html | strip_newlines | truncate: 100 }} </div>

{% assign image_parts = post.content | split: '<img' %}

{% if image_parts.size > 1 %}

<div class="post-photos">

{% for image_part in image_parts offset:1 limit:1 %}

  {% assign image_src = image_part
    | split: 'src="'
    | last
    | split: '"'
    | first %}

  {% if image_src != "" %}

    <img
      src="{{ image_src }}"
      alt="{{ post.title }}"
      loading="lazy">

  {% endif %}

{% endfor %}

</div>

{% endif %}

<a class="read-more" href="{{ post.url | relative_url }}">
阅读全文 →
</a>

</article>

{% endfor %}

<!-- ========================= 分页 ========================= -->

{% if paginator.total_pages > 1 %}

<nav class="pagination">

{% if paginator.previous_page %}
<a href="{{ paginator.previous_page_path | relative_url }}">
← 上一页
</a>
{% endif %}

<span> 第 {{ paginator.page }} / {{ paginator.total_pages }} 页 </span>

{% if paginator.next_page %}
<a href="{{ paginator.next_page_path | relative_url }}">
下一页 →
</a>
{% endif %}

</nav>

{% endif %}

<!-- ========================= 图片放大 ========================= -->

<div class="photo-lightbox" id="photoLightbox">

<span class="photo-lightbox-close" onclick="closePhoto()">
×
</span>

<img id="lightboxImage" src="" alt="">

</div>

<script> document.addEventListener("DOMContentLoaded", function() { const images = document.querySelectorAll(".post-photos img"); const lightbox = document.getElementById("photoLightbox"); const lightboxImage = document.getElementById("lightboxImage"); images.forEach(function(img) { img.addEventListener("click", function() { lightboxImage.src = this.src; lightbox.style.display = "flex"; }); }); }); function closePhoto() { document.getElementById("photoLightbox").style.display = "none"; document.getElementById("lightboxImage").src = ""; } document.getElementById("photoLightbox").addEventListener( "click", function(e) { if (e.target === this) { closePhoto(); } } ); /* ESC 关闭图片 */ document.addEventListener("keydown", function(e) { if (e.key === "Escape") { closePhoto(); } }); </script>


