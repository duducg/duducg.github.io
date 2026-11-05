---
layout: default
title: templateProject
permalink: /projects/templateProject/
---

# Template Project

<!-- Carousel Section -->
<div class="carousel-container">
  <div class="carousel-wrapper" id="carouselWrapper">
    {% assign project_images = site.static_files | where_exp: "item", "item.path contains '/assets/images/projects/templateProject'" %}
    {% for image in project_images %}
      <div class="carousel-slide">
        <img src="{{ image.path | relative_url }}" alt="Project Preview">
      </div>
    {% endfor %}
  </div>
  
  <!-- Navigation Controls -->
  <button class="carousel-btn prev" onclick="moveCarousel(-1)">&#10094;</button>
  <button class="carousel-btn next" onclick="moveCarousel(1)">&#10095;</button>
  
  <!-- Indicators -->
  <div class="carousel-dots">
    {% for image in project_images %}
      <span class="dot {% if forloop.first %}active{% endif %}" onclick="currentSlide({{ forloop.index0 }})"></span>
    {% endfor %}
  </div>
</div>

<div class="split-container">
    <!-- Left Side -->
    <div class="split-column">
        <h2>Left Column Title</h2>
        <p>left-side content.</p>
    </div>

    <!-- Right Side -->
    <div class="split-column">
        <h2>Right Column Title</h2>
        <p>left-side content.</p>
    </div>
</div>

<script>
  let currentIndex = 0;
  function updateCarousel() {
    const wrapper = document.getElementById('carouselWrapper');
    const dots = document.querySelectorAll('.dot');
    wrapper.style.transform = `translateX(-${currentIndex * 100}%)`;
    dots.forEach((dot, index) => {
      dot.classList.toggle('active', index === currentIndex);
    });
  }
  function moveCarousel(direction) {
    const totalSlides = document.querySelectorAll('.carousel-slide').length;
    if (totalSlides === 0) return;
    currentIndex = (currentIndex + direction + totalSlides) % totalSlides;
    updateCarousel();
  }
  function currentSlide(index) {
    currentIndex = index;
    updateCarousel();
  }
</script>
