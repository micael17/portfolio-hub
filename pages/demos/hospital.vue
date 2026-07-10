<template>
  <div class="hospital">
    <nav class="navbar">
      <div class="logo">AURA <span>CLINIC</span></div>
      <div class="nav-links">
        <a href="#procedures">Procedures</a>
        <a href="#doctors">Specialists</a>
        <a href="#clinic">The Clinic</a>
        <button class="btn-book">BOOK CONSULTATION</button>
      </div>
    </nav>
    
    <header class="hero">
      <div class="hero-text">
        <p class="eyebrow">REDEFINING BEAUTY</p>
        <h1>Artistry in <br>Aesthetics.</h1>
        <button class="btn-outline">Explore Our Philosophy</button>
      </div>
      <div class="hero-img"></div>
    </header>

    <section class="features">
      <div class="f-card">
        <p class="num">01.</p>
        <h3>Advanced Technology</h3>
        <p>State-of-the-art FDA approved equipment for precise, safe, and effective treatments.</p>
      </div>
      <div class="f-card">
        <p class="num">02.</p>
        <h3>Expert Surgeons</h3>
        <p>Board-certified plastic surgeons with over decades of specialized experience.</p>
      </div>
      <div class="f-card">
        <p class="num">03.</p>
        <h3>Private Recovery</h3>
        <p>Exclusive, hotel-like VIP suites designed for your utmost comfort and privacy.</p>
      </div>
    </section>

    <section class="banner">
      <h2>"Where medical precision meets aesthetic perfection."</h2>
    </section>
  </div>
</template>

<script setup>
useHead({ title: 'Aura Clinic | Premium Aesthetics' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant:wght@400;600&family=Jost:wght@300;400;500;600&display=swap');

.hospital {
  font-family: 'Jost', sans-serif;
  color: #2b2b2b;
  background: #fdfdfc;
  min-height: 100vh;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 5%;
  border-bottom: 1px solid #eaeaea;
  background: #fff;
}

.logo {
  font-family: 'Cormorant', serif;
  font-size: 1.8rem;
  font-weight: 600;
  letter-spacing: 2px;
}

.logo span {
  font-family: 'Jost', sans-serif;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 4px;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 3rem;
}

.nav-links a {
  text-decoration: none;
  color: #2b2b2b;
  font-size: 0.9rem;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.btn-book {
  background: #2b2b2b;
  color: #fff;
  border: none;
  padding: 1rem 2rem;
  font-family: inherit;
  font-size: 0.8rem;
  letter-spacing: 2px;
  cursor: pointer;
}

.hero {
  display: flex;
  height: 85vh;
  border-bottom: 1px solid #eaeaea;
}

.hero-text {
  flex: 1;
  padding: 0 5%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  background: #fdfdfc;
}

.eyebrow {
  font-size: 0.85rem;
  letter-spacing: 4px;
  margin-bottom: 2rem;
  color: #888;
}

.hero-text h1 {
  font-family: 'Cormorant', serif;
  font-size: 6rem;
  line-height: 1;
  margin-bottom: 3rem;
  font-weight: 400;
}

.btn-outline {
  background: transparent;
  border: 1px solid #2b2b2b;
  padding: 1rem 3rem;
  font-family: inherit;
  font-size: 0.9rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.3s;
}

.btn-outline:hover {
  background: #2b2b2b;
  color: #fff;
}

.hero-img {
  flex: 1;
  background: url('https://images.unsplash.com/photo-1519494026892-80bbd2d6fd0d?w=1200&q=80') center/cover;
}

.features {
  display: flex;
  border-bottom: 1px solid #eaeaea;
}

.f-card {
  flex: 1;
  padding: 5rem 3rem;
  border-right: 1px solid #eaeaea;
  background: #fff;
}

.f-card:last-child {
  border-right: none;
}

.num {
  font-family: 'Cormorant', serif;
  font-size: 2rem;
  color: #ccc;
  margin-bottom: 1.5rem;
}

.f-card h3 {
  font-size: 1.2rem;
  letter-spacing: 1px;
  margin-bottom: 1rem;
  text-transform: uppercase;
}

.f-card p {
  color: #666;
  line-height: 1.6;
}

.banner {
  background: #f4f1ee;
  padding: 8rem 5%;
  text-align: center;
}

.banner h2 {
  font-family: 'Cormorant', serif;
  font-size: 3rem;
  font-weight: 400;
  font-style: italic;
  color: #2b2b2b;
}
</style>
