<template>
  <div class="ecommerce">
    <header class="navbar">
      <div class="nav-left">
        <a href="#">Shop</a>
        <a href="#">Collections</a>
      </div>
      <div class="logo">ESSENTIALS.</div>
      <div class="nav-right">
        <a href="#">Search</a>
        <a href="#">Cart (0)</a>
      </div>
    </header>

    <section class="hero">
      <img src="https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=1600&q=80" alt="Hero">
      <div class="hero-text">
        <h2>The New Standard.</h2>
        <button class="shop-btn">Shop Collection</button>
      </div>
    </section>

    <section class="products">
      <div class="section-title">
        <h3>New Arrivals</h3>
        <a href="#">View All</a>
      </div>
      
      <div class="grid">
        <div class="p-card">
          <div class="img-box"><img src="https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=400&q=80" alt="Product"></div>
          <div class="p-info">
            <h4>Cotton Basic Tee</h4>
            <span>$45</span>
          </div>
        </div>
        <div class="p-card">
          <div class="img-box"><img src="https://images.unsplash.com/photo-1591047139829-d91aecb6caea?w=400&q=80" alt="Product"></div>
          <div class="p-info">
            <h4>Utility Jacket</h4>
            <span>$120</span>
          </div>
        </div>
        <div class="p-card">
          <div class="img-box"><img src="https://images.unsplash.com/photo-1588099768531-a72d4a198538?w=400&q=80" alt="Product"></div>
          <div class="p-info">
            <h4>Canvas Sneakers</h4>
            <span>$85</span>
          </div>
        </div>
        <div class="p-card">
          <div class="img-box"><img src="https://images.unsplash.com/photo-1543163521-1bf539c55dd2?w=400&q=80" alt="Product"></div>
          <div class="p-info">
            <h4>Leather Tote</h4>
            <span>$210</span>
          </div>
        </div>
      </div>
    </section>

    <footer>
      <p>ESSENTIALS. &copy; 2026</p>
    </footer>
  </div>
</template>

<script setup>
useHead({ title: 'Essentials | E-Commerce' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap');

.ecommerce {
  font-family: 'Inter', sans-serif;
  color: #000;
  background: #fff;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 3rem;
  border-bottom: 1px solid #000;
  position: sticky;
  top: 0;
  background: #fff;
  z-index: 100;
}

.logo {
  font-size: 1.5rem;
  font-weight: 800;
  letter-spacing: -1px;
}

.nav-left, .nav-right {
  display: flex;
  gap: 2rem;
}

.navbar a {
  text-decoration: none;
  color: #000;
  font-weight: 600;
  font-size: 0.9rem;
  text-transform: uppercase;
}

.hero {
  position: relative;
  height: 80vh;
  border-bottom: 1px solid #000;
}

.hero img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  background: #fff;
  padding: 3rem 4rem;
  border: 1px solid #000;
}

.hero-text h2 {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 2rem;
  letter-spacing: -2px;
}

.shop-btn {
  background: #000;
  color: #fff;
  border: none;
  padding: 1rem 3rem;
  font-weight: 600;
  text-transform: uppercase;
  cursor: pointer;
  transition: opacity 0.3s;
}

.shop-btn:hover {
  opacity: 0.8;
}

.products {
  padding: 5rem 3rem;
}

.section-title {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 3rem;
  border-bottom: 1px solid #000;
  padding-bottom: 1rem;
}

.section-title h3 {
  font-size: 2rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: -1px;
}

.section-title a {
  color: #000;
  font-weight: 600;
  text-decoration: underline;
}

.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
}

.p-card {
  cursor: pointer;
}

.img-box {
  border: 1px solid #000;
  height: 400px;
  margin-bottom: 1rem;
  overflow: hidden;
}

.img-box img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s;
}

.p-card:hover .img-box img {
  transform: scale(1.05);
}

.p-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.p-info h4 {
  font-size: 1rem;
  font-weight: 600;
}

.p-info span {
  font-weight: 800;
}

footer {
  text-align: center;
  padding: 3rem;
  border-top: 1px solid #000;
  font-weight: 800;
  font-size: 1.2rem;
}
</style>
