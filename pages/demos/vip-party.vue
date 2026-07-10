<template>
  <div class="app-wrap">
    <div class="luxury-card">
      <div class="gold-frame">
        <p class="exclusive">STRICTLY INVITATION ONLY</p>
        <h1>THE<br>GALA<br>2026</h1>
        <div class="divider"></div>
        <p class="invitee">Presented to<br><span>VIP GUEST</span></p>
        
        <div class="details">
          <div class="row">
            <span class="label">DATE</span>
            <span class="val">DEC 31, 2026</span>
          </div>
          <div class="row">
            <span class="label">TIME</span>
            <span class="val">9:00 PM</span>
          </div>
          <div class="row">
            <span class="label">VENUE</span>
            <span class="val">ASTOR HOUSE, NY</span>
          </div>
          <div class="row">
            <span class="label">DRESS</span>
            <span class="val">BLACK TIE</span>
          </div>
        </div>

        <button class="rsvp">ACCEPT INVITATION</button>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'VIP Luxury Party' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700;900&family=Montserrat:wght@300;400;600&display=swap');

.app-wrap {
  background: #050505;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  font-family: 'Montserrat', sans-serif;
  color: #d4af37;
}

.luxury-card {
  max-width: 450px;
  width: 100%;
  background: #0a0a0a;
  padding: 1.5rem;
  position: relative;
}

.luxury-card::before {
  content: ''; position: absolute; top:0; left:0; width:100%; height:100%;
  background: linear-gradient(135deg, rgba(212,175,55,0.2) 0%, transparent 50%, rgba(212,175,55,0.2) 100%);
  pointer-events: none;
}

.gold-frame {
  border: 1px solid #d4af37;
  padding: 4rem 2rem;
  text-align: center;
  background: #050505;
  position: relative;
  z-index: 1;
}

.exclusive {
  font-size: 0.65rem;
  letter-spacing: 5px;
  margin-bottom: 3rem;
  color: #8c7322;
}

h1 {
  font-family: 'Cinzel', serif;
  font-size: 4rem;
  line-height: 1.1;
  font-weight: 400;
  margin-bottom: 2rem;
  background: linear-gradient(to right, #bf953f, #fcf6ba, #b38728, #fbf5b7, #aa771c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.divider {
  width: 1px;
  height: 60px;
  background: #d4af37;
  margin: 0 auto 3rem;
}

.invitee {
  font-size: 0.8rem;
  color: #8c7322;
  letter-spacing: 2px;
  margin-bottom: 4rem;
}

.invitee span {
  display: block;
  font-family: 'Cinzel', serif;
  font-size: 1.5rem;
  color: #d4af37;
  margin-top: 0.5rem;
}

.details {
  border-top: 1px solid rgba(212,175,55,0.3);
  margin-bottom: 4rem;
}

.row {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid rgba(212,175,55,0.3);
  padding: 1.5rem 0;
}

.label {
  font-size: 0.75rem;
  letter-spacing: 3px;
  color: #8c7322;
}

.val {
  font-family: 'Cinzel', serif;
  font-size: 1rem;
  font-weight: 700;
}

.rsvp {
  width: 100%;
  background: #d4af37;
  color: #000;
  border: none;
  padding: 1.2rem;
  font-family: 'Montserrat', sans-serif;
  font-size: 0.9rem;
  font-weight: 600;
  letter-spacing: 3px;
  cursor: pointer;
  transition: all 0.3s;
}

.rsvp:hover {
  background: #fff;
}
</style>
