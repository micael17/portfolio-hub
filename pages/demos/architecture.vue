<template>
  <div class="architecture">
    <nav class="navbar">
      <div class="logo">STUDIO.A</div>
      <div class="menu-btn">MENU</div>
    </nav>
    
    <div class="hero">
      <div class="title-container">
        <h1>SPATIAL<br>POETRY.</h1>
      </div>
      <div class="hero-image">
        <img src="https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=1600&q=80" alt="Architecture">
      </div>
    </div>

    <section class="project-list">
      <div class="p-row">
        <h2>01 / THE CONCRETE HOUSE</h2>
        <span>RESIDENTIAL, 2025</span>
      </div>
      <div class="p-row">
        <h2>02 / SEOUL MUSEUM OF ART</h2>
        <span>CULTURAL, 2024</span>
      </div>
      <div class="p-row">
        <h2>03 / VERTICAL FOREST HQ</h2>
        <span>COMMERCIAL, 2023</span>
      </div>
      <div class="p-row">
        <h2>04 / MINIMALIST PAVILION</h2>
        <span>PUBLIC, 2022</span>
      </div>
    </section>

    <div class="about">
      <p>We believe in the power of raw materials, rigorous geometry, and the interplay of light and shadow.</p>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Studio A | Architecture' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@400;700&family=Roboto+Mono:wght@400&display=swap');

.architecture {
  font-family: 'Oswald', sans-serif;
  background: #e5e5e5;
  color: #1a1a1a;
  min-height: 100vh;
}

.navbar {
  display: flex;
  justify-content: space-between;
  padding: 2rem 5%;
  font-family: 'Roboto Mono', monospace;
  font-weight: 700;
  border-bottom: 2px solid #1a1a1a;
}

.hero {
  display: flex;
  height: 80vh;
  border-bottom: 2px solid #1a1a1a;
}

.title-container {
  width: 40%;
  display: flex;
  align-items: center;
  padding: 0 5%;
  border-right: 2px solid #1a1a1a;
}

h1 {
  font-size: 6rem;
  line-height: 0.9;
  text-transform: uppercase;
}

.hero-image {
  width: 60%;
  height: 100%;
}

.hero-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(100%);
}

.project-list {
  display: flex;
  flex-direction: column;
}

.p-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 3rem 5%;
  border-bottom: 2px solid #1a1a1a;
  cursor: pointer;
  transition: background 0.3s;
}

.p-row:hover {
  background: #1a1a1a;
  color: #e5e5e5;
}

.p-row h2 {
  font-size: 3rem;
  text-transform: uppercase;
  margin: 0;
}

.p-row span {
  font-family: 'Roboto Mono', monospace;
  font-size: 1rem;
}

.about {
  padding: 8rem 5%;
  text-align: center;
}

.about p {
  font-size: 2.5rem;
  line-height: 1.4;
  max-width: 1000px;
  margin: 0 auto;
  text-transform: uppercase;
}
</style>
