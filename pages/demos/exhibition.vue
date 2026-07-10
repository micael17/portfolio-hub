<template>
  <div class="app-wrap">
    <div class="art-card">
      <div class="image-area">
        <img src="https://images.unsplash.com/photo-1536924940846-227afb31e2a5?w=600&q=80" alt="Art">
        <div class="title-overlay">
          <span>EXHIBITION 04</span>
          <h1>VOID</h1>
        </div>
      </div>
      
      <div class="layout-grid">
        <div class="grid-text left">
          <p class="vertical">OPENING RECEPTION</p>
        </div>
        <div class="grid-text right">
          <p>You are invited to the private viewing of VOID, an immersive installation by Studio Blank.</p>
          <div class="line"></div>
          <p class="data">OCTOBER 24, 2026<br>19:00 - 22:00</p>
          <p class="data">GALLERY NEU<br>125 10th Ave, NY</p>
          <button class="rsvp">RSVP &rarr;</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Exhibition Opening' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&display=swap');

.app-wrap {
  background: #d9d9d9;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  font-family: 'Syne', sans-serif;
}

.art-card {
  max-width: 500px;
  width: 100%;
  background: #ececec;
  border: 1px solid #999;
}

.image-area {
  position: relative;
  height: 500px;
  border-bottom: 1px solid #999;
}

.image-area img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(100%) contrast(1.2);
}

.title-overlay {
  position: absolute;
  top: 2rem;
  left: 2rem;
  background: #fff;
  padding: 1rem;
  border: 1px solid #000;
}

.title-overlay span {
  font-size: 0.7rem;
  letter-spacing: 2px;
  display: block;
  margin-bottom: 0.5rem;
}

h1 {
  font-size: 4rem;
  font-weight: 800;
  line-height: 1;
  color: #000;
}

.layout-grid {
  display: flex;
}

.grid-text {
  padding: 2rem;
}

.left {
  border-right: 1px solid #999;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #000;
  color: #fff;
}

.vertical {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  font-size: 1.2rem;
  letter-spacing: 5px;
}

.right {
  flex: 1;
  background: #fff;
}

.right p {
  font-size: 1rem;
  line-height: 1.5;
  margin-bottom: 2rem;
}

.line {
  height: 1px;
  background: #000;
  width: 100%;
  margin-bottom: 2rem;
}

.data {
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 1px;
  margin-bottom: 1.5rem !important;
}

.rsvp {
  background: transparent;
  border: 1px solid #000;
  color: #000;
  padding: 1rem 2rem;
  font-family: inherit;
  font-weight: 700;
  cursor: pointer;
  width: 100%;
  text-align: left;
  display: flex;
  justify-content: space-between;
  transition: background 0.3s;
}

.rsvp:hover {
  background: #000;
  color: #fff;
}
</style>
