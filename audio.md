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
  flex-direction: row;
  align-items: center;
  gap: 0.8rem;
  margin: 0.6rem 0;
  padding: 0.4rem 0;
  border-bottom: 1px solid #f0f0f0;
  flex-wrap: nowrap;
}
.audio-item:last-child { border-bottom: none; }
.track-name { min-width: 140px; max-width: 160px; font-size: 0.85rem; font-weight: 500; }
.audio-item audio { flex: 1; min-width: 150px; height: 32px; }
.dl-btn {
  background: #2c7be5;
  color: white !important;
  padding: 6px 12px;
  border-radius: 4px;
  text-decoration: none !important;
  font-size: 0.8rem;
  white-space: nowrap;
  align-self: center;
  flex-shrink: 0;
}
.dl-btn:hover { background: #1a5bbf; }
@media (max-width: 500px) {
  .audio-item { flex-wrap: wrap; }
  .track-name { min-width: 100%; font-size: 0.85rem; }
  .audio-item audio { width: 100%; min-width: unset; }
  .dl-btn { width: 100%; text-align: center; }
}
</style>

<div class="audio-page">

{% for category in site.data.audio %}
<div class="audio-category">
  <h2>{{ category.category }}</h2>

  {% if category.files %}
    {% for track in category.files %}
    <div class="audio-item"
         data-base-stream="https://jskhundrakpam.github.io/Tapta-Songs-Collection/{{ category.folder }}/"
         data-base-download="https://github.com/jskhundrakpam/Tapta-Songs-Collection/raw/master/{{ category.folder }}/"
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
           data-base-stream="https://jskhundrakpam.github.io/Tapta-Songs-Collection/{{ category.folder }}/{{ subfolder.folder }}/"
           data-base-download="https://github.com/jskhundrakpam/Tapta-Songs-Collection/raw/master/{{ category.folder }}/{{ subfolder.folder }}/"
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
document.querySelectorAll('.audio-item').forEach(function(item) {
  var baseStream   = item.getAttribute('data-base-stream');
  var baseDownload = item.getAttribute('data-base-download');
  var file         = item.getAttribute('data-file');

  // Encode only the filename, keeping the base path as-is from Jekyll
  var encodedFile = file.split('').map(function(c) {
    // Keep alphanumeric and safe chars, encode everything else
    if (/[a-zA-Z0-9\-_.!~]/.test(c)) return c;
    if (c === ' ') return '%20';
    return encodeURIComponent(c);
  }).join('');

  var streamUrl   = baseStream + encodedFile;
  var downloadUrl = baseDownload + encodedFile;

  var audio = item.querySelector('audio');
  var source = document.createElement('source');
  source.src = streamUrl;
  source.type = 'audio/mpeg';
  audio.appendChild(source);

  var btn = item.querySelector('.dl-btn');
  btn.href = downloadUrl;
  btn.setAttribute('download', file);
});
</script>
