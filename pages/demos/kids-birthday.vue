<template>
  <div class="app-wrap">
    <div class="pop-card">
      <div class="block header bg-yellow">
        <h1>LEO IS TURNING 5!</h1>
      </div>
      <div class="block photo bg-blue">
        <img src="https://images.unsplash.com/photo-1530103862676-de8892795816?w=600&q=80" alt="Birthday Boy">
      </div>
      <div class="block details bg-pink">
        <h2>JOIN THE FUN!</h2>
        <div class="info-line">
          <span>WHEN</span>
          <strong>SAT, OCT 24 @ 2PM</strong>
        </div>
        <div class="info-line">
          <span>WHERE</span>
          <strong>PLAYLAND PARK</strong>
        </div>
      </div>
      <div class="block rsvp bg-black">
        <button class="btn">COUNT ME IN!</button>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Kids Birthday' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Archivo+Black&family=Chivo+Mono:wght@700&display=swap');

.app-wrap {
  background: #e5e5e5;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  font-family: 'Chivo Mono', monospace;
}

.pop-card {
  max-width: 450px;
  width: 100%;
  border: 4px solid #000;
  background: #000;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.block {
  padding: 2rem;
  text-align: center;
}

.bg-yellow { background: #ffde00; }
.bg-blue { background: #005ce6; padding: 0 !important; }
.bg-pink { background: #ff007f; color: #fff; }
.bg-black { background: #000; padding: 1rem !important; }

h1 {
  font-family: 'Archivo Black', sans-serif;
  font-size: 3rem;
  line-height: 1;
  color: #000;
  text-transform: uppercase;
}

.photo img {
  width: 100%;
  height: 350px;
  object-fit: cover;
  display: block;
}

h2 {
  font-family: 'Archivo Black', sans-serif;
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #000;
}

.info-line {
  display: flex;
  flex-direction: column;
  margin-bottom: 1.5rem;
  background: #000;
  color: #fff;
  padding: 1rem;
}

.info-line span {
  font-size: 0.9rem;
  color: #ff007f;
  margin-bottom: 0.5rem;
}

.info-line strong {
  font-size: 1.2rem;
}

.btn {
  width: 100%;
  background: #00ffcc;
  color: #000;
  border: 4px solid #00ffcc;
  padding: 1.5rem;
  font-family: 'Archivo Black', sans-serif;
  font-size: 1.5rem;
  cursor: pointer;
  transition: all 0.2s;
}

.btn:hover {
  background: #000;
  color: #00ffcc;
}
</style>
