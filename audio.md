---
layout: default
title: Tapta Songs Collection
permalink: /audio/
---

<style>
.audio-page h1 { margin-bottom: 1.5rem; }
.audio-category { margin-bottom: 3rem; }
.audio-category > h2 {
  background: #2c7be5;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  margin-bottom: 1rem;
}
.audio-subfolder { margin-bottom: 1.5rem; padding-left: 1rem; border-left: 3px solid #2c7be5; }
.audio-subfolder h3 { color: #2c7be5; margin-bottom: 0.5rem; font-size: 1rem; text-transform: uppercase; letter-spacing: 0.05em; }
.audio-item {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin: 0.6rem 0;
  flex-wrap: wrap;
  padding: 0.4rem 0;
  border-bottom: 1px solid #f0f0f0;
}
.audio-item:last-child { border-bottom: none; }
.track-name { min-width: 180px; font-size: 0.9rem; font-weight: 500; }
.audio-item audio { flex: 1; min-width: 200px; max-width: 380px; height: 32px; }
.dl-btn {
  background: #2c7be5;
  color: white !important;
  padding: 5px 12px;
  border-radius: 4px;
  text-decoration: none !important;
  font-size: 0.8rem;
  white-space: nowrap;
}
.dl-btn:hover { background: #1a5bbf; }
@media (max-width: 600px) {
  .audio-item { flex-direction: column; align-items: flex-start; }
  .audio-item audio { width: 100%; max-width: 100%; }
}
</style>

<div class="audio-page">

{% for category in site.data.audio %}
<div class="audio-category">
  <h2>{{ category.category }}</h2>

  {% if category.files %}
    {% for track in category.files %}
    <div class="audio-item"
         data-folder="{{ category.folder }}"
         data-file="{{ track.file }}">
      <span class="track-name">{{ track.name }}</span>
      <audio controls preload="none"></audio>
      <a class="dl-btn" href="#">⬇ Download</a>
    </div>
    {% endfor %}
  {% endif %}

  {% if category.subfolders %}
    {% for subfolder in category.subfolders %}
    <div class="audio-subfolder">
      <h3>{{ subfolder.name }}</h3>
      {% for track in subfolder.files %}
      <div class="audio-item"
           data-folder="{{ category.folder }}"
           data-subfolder="{{ subfolder.folder }}"
           data-file="{{ track.file }}">
        <span class="track-name">{{ track.name }}</span>
        <audio controls preload="none"></audio>
        <a class="dl-btn" href="#">⬇ Download</a>
      </div>
      {% endfor %}
    </div>
    {% endfor %}
  {% endif %}

</div>
{% endfor %}

</div>

<script>
var streamBase   = "https://jskhundrakpam.github.io/Tapta-Songs-Collection/";
var downloadBase = "https://github.com/jskhundrakpam/Tapta-Songs-Collection/raw/master/";

document.querySelectorAll('.audio-item').forEach(function(item) {
  var folder    = item.getAttribute('data-folder') || '';
  var subfolder = item.getAttribute('data-subfolder') || '';
  var file      = item.getAttribute('data-file') || '';

  var parts = [folder, subfolder, file].filter(Boolean);
  var encodedPath = parts.map(function(p) {
    return p.split('/').map(encodeURIComponent).join('/');
  }).join('/');

  var streamUrl   = streamBase + encodedPath;
  var downloadUrl = downloadBase + encodedPath;

  // Set audio player source
  var audio = item.querySelector('audio');
  var source = document.createElement('source');
  source.src = streamUrl;
  source.type = 'audio/mpeg';
  audio.appendChild(source);

  // Set download button to raw GitHub URL (works for download)
  var btn = item.querySelector('.dl-btn');
  btn.href = downloadUrl;
  btn.setAttribute('download', file);
});
</script>
