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
    {% assign encoded_folder = category.folder | url_encode %}
    {% assign encoded_file = track.file | url_encode %}
    {% assign file_url = "https://jskhundrakpam.github.io/Tapta-Songs-Collection/" | append: encoded_folder | append: "/" | append: encoded_file %}
    <div class="audio-item">
      <span class="track-name">{{ track.name }}</span>
      <audio controls preload="none">
        <source src="{{ file_url }}" type="audio/mpeg">
        Your browser does not support audio.
      </audio>
      <a class="dl-btn" href="{{ file_url }}" download>⬇ Download</a>
    </div>
    {% endfor %}
  {% endif %}

  {% if category.subfolders %}
    {% for subfolder in category.subfolders %}
    <div class="audio-subfolder">
      <h3>{{ subfolder.name }}</h3>
      {% for track in subfolder.files %}
      {% assign encoded_folder = category.folder | url_encode %}
      {% assign encoded_subfolder = subfolder.folder | url_encode %}
      {% assign encoded_file = track.file | url_encode %}
      {% assign file_url = "https://jskhundrakpam.github.io/Tapta-Songs-Collection/" | append: encoded_folder | append: "/" | append: encoded_subfolder | append: "/" | append: encoded_file %}
      <div class="audio-item">
        <span class="track-name">{{ track.name }}</span>
        <audio controls preload="none">
          <source src="{{ file_url }}" type="audio/mpeg">
          Your browser does not support audio.
        </audio>
        <a class="dl-btn" href="{{ file_url }}" download>⬇ Download</a>
      </div>
      {% endfor %}
    </div>
    {% endfor %}
  {% endif %}

</div>
{% endfor %}

</div>
