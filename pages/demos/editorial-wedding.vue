<template>
  <main class="invitation">
    <section class="cover">
      <div class="topline"><span>J + H</span><span>2026. 10. 17</span></div>
      <img src="/images/wedding-ai/editorial-studio-couple.png" alt="스튜디오에서 촬영한 신랑 신부" class="cover-photo">
      <div class="cover-copy">
        <p>THE WEDDING ISSUE</p>
        <h1>JUNE<br>&amp; HYUN</h1>
        <span>Saturday, 4 PM · Seoul</span>
      </div>
    </section>

    <section class="note section-pad">
      <p class="index">01 / HELLO</p>
      <h2>우리의 가장<br>좋아하는 장면에<br>함께해 주세요.</h2>
      <p class="body">좋아하는 사람들, 좋아하는 음악, 그리고 오래 남을 오후. 두 사람이 새 챕터를 시작하는 날에 소중한 당신을 초대합니다.</p>
    </section>

    <section class="details section-pad">
      <p class="index">02 / SAVE THE DATE</p>
      <div class="date-card">
        <strong>17</strong>
        <div><span>OCTOBER</span><b>SATURDAY · 4:00 PM</b></div>
      </div>
      <div class="venue"><span>VENUE</span><b>Layer 7 Seongsu<br>서울 성동구 서울숲길 57</b></div>
      <a href="#rsvp" class="primary">참석 의사 전하기 <span>↘</span></a>
    </section>

    <section class="editorial section-pad">
      <p class="index">03 / EDITOR'S NOTE</p>
      <p class="quote">“The best is yet to come.”</p>
      <div class="plan">
        <div v-for="item in plan" :key="item.time"><span>{{ item.time }}</span><b>{{ item.title }}</b><p>{{ item.detail }}</p></div>
      </div>
    </section>

    <section id="rsvp" class="rsvp">
      <p class="index">04 / RSVP</p>
      <h2>자리를 비워둘게요.</h2>
      <div class="choice-row"><button :class="{ selected: attendance === 'yes' }" @click="attendance = 'yes'">기쁘게 참석</button><button :class="{ selected: attendance === 'no' }" @click="attendance = 'no'">마음으로 축하</button></div>
      <input v-model="guestName" type="text" placeholder="성함을 알려주세요">
      <button class="primary wide" @click="submitted = true">{{ submitted ? '전해졌어요. 고마워요.' : '참석 의사 보내기' }}</button>
    </section>

    <section class="visit section-pad">
      <p class="index">05 / FIND US</p>
      <h2>Layer 7,<br>Seongsu.</h2>
      <p>서울숲역 4번 출구에서 도보 6분<br>주차는 건물 발렛을 이용해 주세요.</p>
      <a href="https://www.openstreetmap.org/?mlat=37.5462&mlon=127.0445#map=17/37.5462/127.0445" target="_blank" rel="noopener" class="text-link">지도에서 보기 ↗</a>
    </section>
    <footer>JUNE &amp; HYUN · WITH LOVE</footer>
  </main>
</template>

<script setup lang="ts">
const attendance = ref('yes')
const guestName = ref('')
const submitted = ref(false)
const plan = [
  { time: '15:20', title: 'DOORS OPEN', detail: '웰컴 드링크와 포토 부스' },
  { time: '16:00', title: 'CEREMONY', detail: '두 사람의 약속' },
  { time: '16:40', title: 'TOAST & TABLE', detail: '축하와 작은 만찬' }
]
useHead({ title: 'June & Hyun | Editorial Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono&family=Playfair+Display:ital,wght@0,500;0,700;1,500&family=Pretendard:wght@400;500;700&display=swap');
.invitation{max-width:540px;margin:auto;min-height:100vh;background:#f5f2ed;color:#1b1b1a;font-family:Pretendard,sans-serif}.cover{height:100svh;min-height:650px;position:relative;overflow:hidden;background:#d8d1c7}.cover-photo{width:100%;height:100%;object-fit:cover;object-position:center}.topline,.cover-copy{position:absolute;z-index:1;left:24px;right:24px;display:flex;justify-content:space-between;color:#fff;font:10px 'DM Mono',monospace;letter-spacing:.08em}.topline{top:24px}.cover-copy{bottom:27px;display:block;text-shadow:0 2px 16px #3338}.cover-copy p,.index{font:10px 'DM Mono',monospace;letter-spacing:.12em;margin:0 0 13px}.cover-copy h1{font:500 clamp(58px,17vw,88px)/.78 'Playfair Display',serif;margin:0 0 17px}.cover-copy span{font-size:11px}.section-pad{padding:65px 24px}.note h2,.rsvp h2,.visit h2{font:500 42px/.98 'Playfair Display',serif;margin:0;letter-spacing:-.05em}.body{font-size:15px;line-height:1.8;margin:28px 0 0;max-width:330px}.details{background:#1d1c1a;color:#f8f6f0}.date-card{padding:22px 0;border-top:1px solid #68645e;border-bottom:1px solid #68645e;display:flex;align-items:center;gap:20px}.date-card strong{font:500 74px/.8 'Playfair Display',serif}.date-card div{display:grid;gap:6px;font:11px 'DM Mono',monospace;letter-spacing:.08em}.date-card b{font:500 13px Pretendard,sans-serif}.venue{display:grid;gap:9px;padding:28px 0;font-size:14px;line-height:1.6}.venue span{font:10px 'DM Mono',monospace;color:#aaa39a}.primary{display:flex;justify-content:space-between;align-items:center;padding:17px 18px;background:#f1e7d6;color:#1c1b19;text-decoration:none;border:0;font:700 14px Pretendard,sans-serif;cursor:pointer}.primary span{font-size:20px}.editorial{background:#e2ddd4}.quote{font:italic 38px/1.05 'Playfair Display',serif;margin:44px 0}.plan>div{display:grid;grid-template-columns:66px 1fr;gap:2px;padding:17px 0;border-top:1px solid #b9b3aa}.plan span{font:10px 'DM Mono',monospace}.plan b{font-size:13px}.plan p{grid-column:2;margin:4px 0 0;color:#5f5b55;font-size:12px}.rsvp{padding:60px 24px;background:#b9422b;color:#fff}.rsvp h2{font-size:38px;margin-bottom:28px}.choice-row{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px}.choice-row button{padding:14px 6px;border:1px solid #ffffff80;background:transparent;color:#fff;font:13px Pretendard,sans-serif}.choice-row .selected{background:#fff;color:#ad3622}.rsvp input{box-sizing:border-box;width:100%;padding:16px;margin-bottom:10px;border:1px solid #ffffff80;background:transparent;color:#fff;font:14px Pretendard,sans-serif}.rsvp input::placeholder{color:#ffe6df}.wide{width:100%;background:#1d1c1a;color:#fff;justify-content:center}.visit h2{margin-bottom:25px}.visit p{font-size:14px;line-height:1.8}.text-link{display:inline-block;margin-top:19px;color:inherit;font-weight:700;text-decoration:none;border-bottom:1px solid;padding-bottom:4px}footer{padding:26px 24px;background:#1d1c1a;color:#fff;font:10px 'DM Mono',monospace;letter-spacing:.09em}@media(min-width:541px){.invitation{box-shadow:0 0 60px #0002}}
</style>
