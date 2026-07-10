<template>
  <div class="app-wrap">
    <div class="corp-card">
      <header>
        <div class="logo">TECHCON 26</div>
        <div class="badge">INVITATION</div>
      </header>
      
      <div class="hero">
        <h1>THE FUTURE OF <br>ENTERPRISE AI</h1>
        <p class="subtitle">Annual Leadership Summit</p>
      </div>
      
      <div class="grid-table">
        <div class="row">
          <div class="col label">DATE</div>
          <div class="col val">October 24-25, 2026</div>
        </div>
        <div class="row">
          <div class="col label">LOCATION</div>
          <div class="col val">Moscone Center, SF</div>
        </div>
        <div class="row">
          <div class="col label">ATTENDEES</div>
          <div class="col val">C-Level Executives Only</div>
        </div>
      </div>
      
      <div class="desc">
        <p>Join industry leaders to discuss the impact of generative AI on enterprise architecture, security, and scaling operations.</p>
      </div>
      
      <button class="register">REGISTER NOW</button>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Corporate Seminar' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;600;700&display=swap');

.app-wrap {
  background: #f0f4f8;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  font-family: 'IBM Plex Sans', sans-serif;
}

.corp-card {
  max-width: 500px;
  width: 100%;
  background: #fff;
  border: 1px solid #cbd5e1;
  box-shadow: 10px 10px 0px #0f172a;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  border-bottom: 1px solid #cbd5e1;
  background: #f8fafc;
}

.logo {
  font-weight: 700;
  font-size: 1.2rem;
  color: #0f172a;
  letter-spacing: 1px;
}

.badge {
  background: #2563eb;
  color: #fff;
  font-size: 0.7rem;
  font-weight: 600;
  padding: 0.3rem 0.6rem;
  letter-spacing: 1px;
}

.hero {
  padding: 4rem 2rem;
  background: #0f172a;
  color: #fff;
}

h1 {
  font-size: 2.5rem;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.subtitle {
  color: #94a3b8;
  font-size: 1.1rem;
}

.grid-table {
  display: flex;
  flex-direction: column;
}

.row {
  display: flex;
  border-bottom: 1px solid #cbd5e1;
}

.col {
  padding: 1.5rem;
}

.label {
  flex: 0 0 120px;
  background: #f8fafc;
  border-right: 1px solid #cbd5e1;
  font-size: 0.8rem;
  font-weight: 600;
  color: #64748b;
  letter-spacing: 1px;
}

.val {
  flex: 1;
  font-weight: 600;
  color: #0f172a;
}

.desc {
  padding: 2rem;
  line-height: 1.6;
  color: #475569;
  border-bottom: 1px solid #cbd5e1;
}

.register {
  width: 100%;
  background: #2563eb;
  color: #fff;
  border: none;
  padding: 1.5rem;
  font-family: inherit;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  transition: background 0.2s;
}

.register:hover {
  background: #1d4ed8;
}
</style>
