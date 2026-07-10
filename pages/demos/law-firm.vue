<template>
  <div class="law-firm">
    <nav class="navbar">
      <div class="logo">LEX <span>PARTNERS</span></div>
      <div class="nav-links">
        <a href="#about">About</a>
        <a href="#practice">Practice Areas</a>
        <a href="#attorneys">Attorneys</a>
        <a href="#contact" class="btn">Consultation</a>
      </div>
    </nav>
    
    <header class="hero">
      <div class="hero-content">
        <h1>UNYIELDING<br>ADVOCACY.</h1>
        <p>A premier law firm dedicated to providing strategic and uncompromising legal representation for complex corporate and civil matters.</p>
        <button class="btn large">Our Expertise</button>
      </div>
    </header>

    <section class="stats">
      <div class="stat-item">
        <h2>25+</h2>
        <p>Years of Experience</p>
      </div>
      <div class="stat-item">
        <h2>$2B+</h2>
        <p>Recovered for Clients</p>
      </div>
      <div class="stat-item">
        <h2>50+</h2>
        <p>Top Tier Attorneys</p>
      </div>
    </section>

    <section class="practice-areas" id="practice">
      <div class="section-header">
        <h2>AREAS OF PRACTICE</h2>
        <a href="#">View All &rarr;</a>
      </div>
      <div class="grid">
        <div class="area-card">
          <h3>Corporate Litigation</h3>
          <p>Handling high-stakes disputes with precision and aggressive strategy.</p>
        </div>
        <div class="area-card">
          <h3>Mergers & Acquisitions</h3>
          <p>Facilitating multi-million dollar transactions across global markets.</p>
        </div>
        <div class="area-card">
          <h3>Intellectual Property</h3>
          <p>Protecting the innovations that drive tomorrow's industry leaders.</p>
        </div>
        <div class="area-card">
          <h3>White Collar Defense</h3>
          <p>Discreet and robust defense for executives and corporations.</p>
        </div>
      </div>
    </section>

    <footer>
      <div class="footer-content">
        <div class="logo">LEX <span>PARTNERS</span></div>
        <p>1200 Avenue of the Americas, New York, NY 10036</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
useHead({ title: 'Lex Partners | Law Firm' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Inter:wght@400;600&display=swap');

.law-firm {
  font-family: 'Inter', sans-serif;
  color: #111;
  background: #f9f9f9;
  min-height: 100vh;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 5%;
  background: #fff;
  border-bottom: 1px solid #000;
}

.logo {
  font-family: 'Playfair Display', serif;
  font-size: 1.5rem;
  font-weight: 900;
  letter-spacing: 2px;
}

.logo span {
  font-weight: 700;
  color: #666;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.nav-links a {
  text-decoration: none;
  color: #111;
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.85rem;
  letter-spacing: 1px;
}

.btn {
  background: #111;
  color: #fff !important;
  padding: 0.8rem 1.5rem;
  border: 1px solid #111;
  cursor: pointer;
  transition: all 0.3s;
}

.btn:hover {
  background: #fff;
  color: #111 !important;
}

.hero {
  height: 80vh;
  background: url('https://images.unsplash.com/photo-1589829085413-56de8ae18c73?w=1600&q=80') center/cover;
  position: relative;
  display: flex;
  align-items: center;
  padding: 0 5%;
}

.hero::after {
  content: ''; position: absolute; top:0; left:0; right:0; bottom:0; background: rgba(0,0,0,0.6);
}

.hero-content {
  position: relative;
  z-index: 1;
  color: #fff;
  max-width: 800px;
}

.hero h1 {
  font-family: 'Playfair Display', serif;
  font-size: 5rem;
  line-height: 1.1;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.hero p {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 2.5rem;
  color: #ccc;
}

.btn.large {
  padding: 1rem 2.5rem;
  font-size: 1rem;
}

.stats {
  display: flex;
  border-bottom: 1px solid #000;
}

.stat-item {
  flex: 1;
  text-align: center;
  padding: 4rem 2rem;
  border-right: 1px solid #000;
  background: #fff;
}

.stat-item:last-child {
  border-right: none;
}

.stat-item h2 {
  font-family: 'Playfair Display', serif;
  font-size: 3rem;
  margin-bottom: 0.5rem;
}

.stat-item p {
  text-transform: uppercase;
  letter-spacing: 2px;
  font-size: 0.85rem;
  font-weight: 600;
  color: #666;
}

.practice-areas {
  padding: 6rem 5%;
  background: #f9f9f9;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 4rem;
  border-bottom: 1px solid #000;
  padding-bottom: 1rem;
}

.section-header h2 {
  font-family: 'Playfair Display', serif;
  font-size: 2.5rem;
}

.section-header a {
  color: #111;
  text-decoration: none;
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.9rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
}

.area-card {
  background: #fff;
  border: 1px solid #000;
  padding: 3rem;
  transition: transform 0.3s;
}

.area-card:hover {
  transform: translateY(-5px);
  background: #111;
  color: #fff;
}

.area-card h3 {
  font-family: 'Playfair Display', serif;
  font-size: 1.8rem;
  margin-bottom: 1rem;
}

.area-card p {
  line-height: 1.6;
  color: inherit;
  opacity: 0.8;
}

footer {
  background: #111;
  color: #fff;
  padding: 4rem 5%;
  text-align: center;
}

footer .logo {
  color: #fff;
  margin-bottom: 1rem;
}
</style>
