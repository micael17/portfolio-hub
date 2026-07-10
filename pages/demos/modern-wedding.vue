<template>
  <div class="app-wrap">
    <div class="hero">
      <div class="grid-overlay"></div>
      <h1 class="glitch" data-text="MARRIED.">MARRIED.</h1>
      <div class="hero-bottom">
        <span>A & B</span>
        <span>10.24.26</span>
      </div>
    </div>
    <div class="content">
      <div class="block black">
        <h2>WE DECIDED<br>TO DO THIS.</h2>
        <p>No flowers. No rings. Just us and you.</p>
      </div>
      <div class="block white">
        <h3>WHERE</h3>
        <p>Industrial Studio X<br>Brooklyn, NY</p>
      </div>
      <div class="block outline">
        <h3>WHEN</h3>
        <p>Midnight<br>October 24</p>
      </div>
      <button class="btn-rsvp">CONFIRM YOUR PRESENCE</button>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Modern Minimal Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;700;900&display=swap');

.app-wrap {
  font-family: 'Space Grotesk', sans-serif;
  background: #fff;
  color: #000;
  max-width: 450px;
  margin: 0 auto;
  border-left: 2px solid #000;
  border-right: 2px solid #000;
  min-height: 100vh;
}

.hero {
  height: 70vh;
  background: #000;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2rem;
  position: relative;
  overflow: hidden;
}

.grid-overlay {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background-image: linear-gradient(#333 1px, transparent 1px), linear-gradient(90deg, #333 1px, transparent 1px);
  background-size: 30px 30px;
  opacity: 0.2;
}

h1 {
  font-size: 5rem;
  font-weight: 900;
  line-height: 0.9;
  letter-spacing: -2px;
  position: relative;
  z-index: 2;
  margin: 0;
}

.hero-bottom {
  position: absolute;
  bottom: 2rem;
  left: 2rem;
  right: 2rem;
  display: flex;
  justify-content: space-between;
  font-weight: 700;
  font-size: 1.2rem;
  border-top: 2px solid #fff;
  padding-top: 1rem;
}

.content {
  padding: 2rem;
}

.block {
  padding: 3rem 2rem;
  margin-bottom: 2rem;
}

.block.black {
  background: #000;
  color: #fff;
}

.block.white {
  background: #fff;
  border: 2px solid #000;
}

.block.outline {
  border: 2px dashed #000;
}

h2 {
  font-size: 2.5rem;
  font-weight: 900;
  line-height: 1;
  margin-bottom: 1rem;
}

h3 {
  font-size: 1rem;
  font-weight: 900;
  margin-bottom: 0.5rem;
  letter-spacing: 2px;
}

p {
  font-size: 1.2rem;
  font-weight: 700;
}

.btn-rsvp {
  width: 100%;
  background: transparent;
  color: #000;
  border: 4px solid #000;
  padding: 1.5rem;
  font-size: 1.2rem;
  font-weight: 900;
  font-family: inherit;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-rsvp:hover {
  background: #000;
  color: #fff;
}
</style>
