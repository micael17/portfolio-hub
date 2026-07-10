<template>
  <div class="invitation-app">
    <section class="hero">
      <div class="border-frame">
        <p class="top-text">INVITATION TO OUR WEDDING</p>
        <h1>William<br>&<br>Charlotte</h1>
        <p class="date">OCTOBER 24, 2026</p>
      </div>
    </section>
    
    <section class="content">
      <h2>The Beginning</h2>
      <div class="line"></div>
      <p class="msg">
        Together with our families, we invite you to share our joy as we exchange our vows and begin our new life together.
      </p>
      
      <div class="info-box">
        <h3>CEREMONY</h3>
        <p>4:00 PM</p>
        <p>Grace Cathedral</p>
        <p>1100 California St, San Francisco</p>
      </div>

      <div class="info-box">
        <h3>RECEPTION</h3>
        <p>6:00 PM</p>
        <p>The Fairmont</p>
        <p>950 Mason St, San Francisco</p>
      </div>
      
      <button class="rsvp">RSVP ONLINE</button>
    </section>
  </div>
</template>

<script setup>
useHead({ title: 'Classic Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Lato:wght@300;400&display=swap');

.invitation-app {
  font-family: 'Playfair Display', serif;
  background: #fffdf9;
  color: #2c3e50;
  max-width: 450px;
  margin: 0 auto;
  min-height: 100vh;
  border-left: 1px solid #e0d8c3;
  border-right: 1px solid #e0d8c3;
}

.hero {
  padding: 2rem;
  height: 80vh;
  display: flex;
}

.border-frame {
  flex: 1;
  border: 1px solid #2c3e50;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 2rem;
  background: #fff;
}

.top-text {
  font-family: 'Lato', sans-serif;
  font-size: 0.7rem;
  letter-spacing: 4px;
  margin-bottom: 3rem;
}

h1 {
  font-size: 3.5rem;
  font-weight: 400;
  font-style: italic;
  line-height: 1.2;
  margin-bottom: 3rem;
}

.date {
  font-family: 'Lato', sans-serif;
  font-size: 0.9rem;
  letter-spacing: 2px;
}

.content {
  padding: 4rem 2rem;
  text-align: center;
  background: #fff;
  border-top: 1px solid #2c3e50;
}

h2 {
  font-size: 2rem;
  font-style: italic;
  font-weight: 400;
  margin-bottom: 1rem;
}

.line {
  width: 1px;
  height: 40px;
  background: #2c3e50;
  margin: 0 auto 2rem;
}

.msg {
  font-family: 'Lato', sans-serif;
  line-height: 2;
  font-size: 0.95rem;
  margin-bottom: 4rem;
}

.info-box {
  margin-bottom: 3rem;
  border: 1px solid #e0d8c3;
  padding: 2rem;
  background: #fffdf9;
}

.info-box h3 {
  font-family: 'Lato', sans-serif;
  font-size: 0.8rem;
  letter-spacing: 3px;
  margin-bottom: 1rem;
  color: #8e806a;
}

.info-box p {
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}

.rsvp {
  font-family: 'Lato', sans-serif;
  background: #2c3e50;
  color: #fff;
  border: none;
  padding: 1.2rem 3rem;
  letter-spacing: 3px;
  font-size: 0.8rem;
  cursor: pointer;
  width: 100%;
  margin-top: 2rem;
}
</style>
