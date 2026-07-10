<template>
  <div class="botanical-app">
    <div class="frame">
      <div class="hero-img"></div>
      <div class="content-box">
        <p class="eyebrow">A GARDEN WEDDING</p>
        <h1>Emma & Noah</h1>
        <div class="leaf-divider"></div>
        <p class="desc">
          We invite you to our outdoor celebration under the ancient oaks.<br>
          Join us for an evening of love, laughter, and nature.
        </p>
        
        <div class="details-grid">
          <div class="d-item">
            <strong>WHEN</strong>
            <p>Oct 24, 2026<br>3:00 PM</p>
          </div>
          <div class="d-item">
            <strong>WHERE</strong>
            <p>Greenhouse Gardens<br>Seattle, WA</p>
          </div>
        </div>

        <button class="rsvp-btn">RSVP</button>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Botanical Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Montserrat:wght@400;600&display=swap');

.botanical-app {
  background: #f2f5f0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
}

.frame {
  max-width: 450px;
  width: 100%;
  background: #fff;
  border: 1px solid #c8d5b9;
  position: relative;
}

.hero-img {
  height: 350px;
  background: url('https://images.unsplash.com/photo-1518112166137-85f9979a43dd?w=800&q=80') center/cover;
  border-bottom: 10px solid #4a5d23;
}

.content-box {
  padding: 4rem 3rem;
  text-align: center;
  background: #fff;
}

.eyebrow {
  font-family: 'Montserrat', sans-serif;
  color: #4a5d23;
  font-size: 0.8rem;
  letter-spacing: 3px;
  margin-bottom: 1.5rem;
}

h1 {
  font-family: 'Cormorant Garamond', serif;
  font-size: 3.5rem;
  color: #2b3a1a;
  line-height: 1.1;
  margin-bottom: 1.5rem;
}

.leaf-divider {
  width: 40px;
  height: 40px;
  background: #4a5d23;
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  margin: 0 auto 2rem;
}

.desc {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.2rem;
  line-height: 1.8;
  color: #5c6650;
  margin-bottom: 3rem;
}

.details-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  border-top: 1px solid #c8d5b9;
  border-bottom: 1px solid #c8d5b9;
  padding: 2rem 0;
  margin-bottom: 3rem;
}

.d-item strong {
  font-family: 'Montserrat', sans-serif;
  font-size: 0.8rem;
  color: #4a5d23;
  letter-spacing: 2px;
  display: block;
  margin-bottom: 0.5rem;
}

.d-item p {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  color: #2b3a1a;
}

.rsvp-btn {
  background: #4a5d23;
  color: #fff;
  border: none;
  font-family: 'Montserrat', sans-serif;
  padding: 1.2rem 3rem;
  font-size: 0.9rem;
  letter-spacing: 3px;
  cursor: pointer;
  transition: background 0.3s;
}

.rsvp-btn:hover {
  background: #2b3a1a;
}
</style>
