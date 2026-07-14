<template>
  <main class="invitation">
    <!-- COVER -->
    <section class="cover">
      <div class="topline"><span>J + H</span><span>2026. 10. 17</span></div>
      <!-- AI-IMG: 에디토리얼 스튜디오 웨딩 화보, 매거진 무드·큰 여백 · 3:4 -->
      <!-- prompt: editorial studio wedding shoot, magazine mood, generous whitespace, fashion, 3:4 -->
      <img src="/images/wedding-ai/editorial-studio-couple.png" alt="스튜디오 배경 앞에서 나란히 선 신랑과 신부의 화보 컷" class="cover-photo">
      <div class="cover-copy">
        <p>THE WEDDING ISSUE</p>
        <h1>JUNE<br>&amp; HYUN</h1>
        <span>Saturday, 4 PM · Seoul</span>
      </div>
    </section>

    <!-- 01 / 인사말 -->
    <section class="note section-pad">
      <p class="index">EDITORIAL 01 — HELLO</p>
      <h2>우리의 가장<br>좋아하는 장면에<br>함께해 주세요.</h2>
      <p class="body">좋아하는 사람들, 좋아하는 음악, 그리고 오래 남을 어느 가을 오후. 두 사람이 서로의 다음 챕터를 함께 쓰기로 한 날, 그 첫 페이지에 소중한 당신의 이름을 남기고 싶습니다.</p>
      <p class="signoff">— 김준 · 이현 드림</p>
    </section>

    <!-- 02 / 예식 정보 -->
    <section class="details section-pad">
      <p class="index">EDITORIAL 02 — SAVE THE DATE</p>
      <div class="date-card">
        <strong>17</strong>
        <div><span>OCTOBER 2026</span><b>SATURDAY · 4:00 PM</b></div>
        <em v-if="dday !== null" class="dday">{{ dday > 0 ? `D-${dday}` : dday === 0 ? 'D-DAY' : `D+${-dday}` }}</em>
      </div>
      <div class="venue"><span>VENUE</span><b>Layer 7 Seongsu<br>서울 성동구 서울숲길 57, 7F</b></div>
      <div class="venue"><span>DRESS CODE</span><b>가을빛 어스톤, 편안한 옷차림 환영</b></div>
      <a href="#rsvp" class="primary">참석 의사 전하기 <span>↘</span></a>
    </section>

    <!-- 03 / 화보 갤러리 -->
    <section class="gallery-head section-pad">
      <p class="index">EDITORIAL 03 — THE SHOOT</p>
      <h2>Two people,<br>one autumn.</h2>
      <p class="body">가을의 도시와 정원을 배경으로 담은 프리웨딩 화보. 스크롤을 따라 한 장면씩 열립니다.</p>
    </section>
    <section class="gallery">
      <figure class="g-tall reveal">
        <!-- AI-IMG: 정원에서 마주 보는 신랑 신부 웨딩 화보, 매거진 무드·큰 여백 · 3:4 -->
        <!-- prompt: bride and groom facing each other in a garden, editorial wedding shoot, magazine mood, generous whitespace, 3:4 -->
        <img src="/images/wedding-ai/garden-couple.png" alt="정원에서 서로를 마주 본 신랑 신부의 화보 컷">
        <figcaption><span>PLATE 01</span>The Garden</figcaption>
      </figure>
      <figure class="g-wide reveal">
        <!-- AI-IMG: 모던 도시 배경 신랑 신부 웨딩 화보, 매거진 무드·큰 여백 · 16:9 -->
        <!-- prompt: modern urban backdrop couple wedding editorial shoot, magazine mood, generous whitespace, 16:9 -->
        <img src="/images/wedding-ai/modern-couple.png" alt="모던한 도시 배경에서 촬영한 신랑 신부의 가로 화보 컷">
        <figcaption><span>PLATE 02</span>The City</figcaption>
      </figure>
      <div class="g-pair">
        <figure class="reveal">
          <!-- AI-IMG: 클래식 무드 신랑 신부 웨딩 화보, 매거진 무드·큰 여백 · 3:4 -->
          <!-- prompt: classic mood couple wedding editorial portrait, magazine, generous whitespace, 3:4 -->
          <img src="/images/wedding-ai/classic-couple.png" alt="클래식한 분위기로 촬영한 신랑 신부의 세로 화보 컷">
          <figcaption><span>PLATE 03</span>Classic</figcaption>
        </figure>
        <figure class="reveal">
          <!-- AI-IMG: 정원에서 가까이 붙은 신랑 신부 클로즈업 화보, 매거진 무드·큰 여백 · 3:4 -->
          <!-- prompt: close-up of couple in a garden, wedding editorial, magazine mood, generous whitespace, 3:4 -->
          <img src="/images/wedding-ai/garden-couple-close.png" alt="정원에서 가까이 마주 선 신랑 신부의 클로즈업 화보 컷">
          <figcaption><span>PLATE 04</span>Closer</figcaption>
        </figure>
      </div>
      <figure class="g-tall reveal">
        <!-- AI-IMG: 시그니처 호텔 로비 배경 신랑 신부 웨딩 화보, 매거진 무드·큰 여백 · 3:4 -->
        <!-- prompt: couple in a signature hotel lobby, wedding editorial shoot, magazine mood, generous whitespace, 3:4 -->
        <img src="/images/wedding-ai/signature-hotel-couple.png" alt="호텔 로비를 배경으로 촬영한 신랑 신부의 화보 컷">
        <figcaption><span>PLATE 05</span>The Hotel</figcaption>
      </figure>
      <figure class="g-wide reveal">
        <!-- AI-IMG: 해안가 아카이브 무드 신랑 신부 웨딩 화보, 매거진 무드·큰 여백 · 16:9 -->
        <!-- prompt: coastal archive-mood couple wedding editorial shoot, film grain, magazine, generous whitespace, 16:9 -->
        <img src="/images/wedding-ai/archive-coast-couple.png" alt="해안가에서 촬영한 신랑 신부의 가로 화보 컷">
        <figcaption><span>PLATE 06</span>The Coast</figcaption>
      </figure>
    </section>

    <!-- 04 / 에디터의 노트 · 타임라인 -->
    <section class="editorial section-pad">
      <p class="index">EDITORIAL 04 — EDITOR'S NOTE</p>
      <p class="quote">“The best is yet to come.”</p>
      <div class="plan">
        <div v-for="item in plan" :key="item.time"><span>{{ item.time }}</span><b>{{ item.title }}</b><p>{{ item.detail }}</p></div>
      </div>
    </section>

    <!-- 05 / 오시는 길 -->
    <section class="visit section-pad">
      <p class="index">EDITORIAL 05 — FIND US</p>
      <h2>Layer 7,<br>Seongsu.</h2>
      <p>서울숲역 4번 출구에서 도보 6분<br>주차는 건물 발렛을 이용해 주세요.</p>
      <a href="https://www.openstreetmap.org/?mlat=37.5462&mlon=127.0445#map=17/37.5462/127.0445" target="_blank" rel="noopener" class="text-link">지도에서 보기 ↗</a>
    </section>

    <!-- 06 / 마음 전하실 곳 -->
    <section class="accounts section-pad">
      <p class="index">EDITORIAL 06 — WITH THANKS</p>
      <h2>마음을<br>전하실 곳.</h2>
      <p class="body">축하의 마음을 전하고 싶은 분들을 위해 남겨둡니다. 마음만으로도 충분합니다.</p>
      <ul class="account-list">
        <li v-for="acc in accounts" :key="acc.owner">
          <div><span>{{ acc.role }}</span><b>{{ acc.owner }}</b></div>
          <div class="acc-num">{{ acc.bank }} {{ acc.number }}</div>
        </li>
      </ul>
    </section>

    <!-- 07 / RSVP -->
    <section id="rsvp" class="rsvp">
      <p class="index">EDITORIAL 07 — RSVP</p>
      <h2>자리를 비워둘게요.</h2>
      <div class="choice-row"><button :class="{ selected: attendance === 'yes' }" @click="attendance = 'yes'">기쁘게 참석</button><button :class="{ selected: attendance === 'no' }" @click="attendance = 'no'">마음으로 축하</button></div>
      <input v-model="guestName" type="text" placeholder="성함을 알려주세요">
      <button class="primary wide" :disabled="!guestName.trim() && !sent" @click="submit">{{ sent ? '전해졌어요. 고마워요.' : '참석 의사 보내기' }}</button>
    </section>

    <!-- 08 / 안내사항 -->
    <section class="info section-pad">
      <p class="index">EDITORIAL 08 — GOOD TO KNOW</p>
      <div class="info-grid">
        <div v-for="tip in tips" :key="tip.title"><b>{{ tip.title }}</b><p>{{ tip.detail }}</p></div>
      </div>
    </section>

    <footer>JUNE &amp; HYUN · WITH LOVE</footer>
  </main>
</template>

<script setup lang="ts">
const attendance = ref('yes')
const guestName = ref('')
const sent = ref(false)
const dday = ref<number | null>(null)
const submit = () => {
  if (!guestName.value.trim()) return
  sent.value = true
}
const plan = [
  { time: '15:20', title: 'DOORS OPEN', detail: '웰컴 드링크와 포토 부스' },
  { time: '16:00', title: 'CEREMONY', detail: '두 사람의 약속' },
  { time: '16:40', title: 'TOAST & TABLE', detail: '축하와 작은 만찬' },
  { time: '18:00', title: 'AFTER PARTY', detail: '음악과 함께하는 마무리' }
]
const accounts = [
  { role: 'GROOM', owner: '김준', bank: '국민', number: '123-45-678901' },
  { role: 'BRIDE', owner: '이현', bank: '신한', number: '110-234-567890' }
]
const tips = [
  { title: 'PARKING', detail: '건물 발렛 주차 2시간 무료. 대중교통을 권장합니다.' },
  { title: 'FLOWERS', detail: '화환은 정중히 사양합니다. 마음만 감사히 받겠습니다.' },
  { title: 'PHOTO', detail: '식중 자유롭게 촬영하시고, 태그 @june.and.hyun 로 공유해 주세요.' },
  { title: 'DINING', detail: '뷔페식 만찬이 예식 직후 같은 층에서 이어집니다.' }
]

onMounted(() => {
  const target = new Date('2026-10-17T16:00:00+09:00')
  const today = new Date()
  today.setHours(0, 0, 0, 0)
  const day = new Date(target)
  day.setHours(0, 0, 0, 0)
  dday.value = Math.round((day.getTime() - today.getTime()) / 86400000)

  const els = document.querySelectorAll('.reveal')
  const io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (e.isIntersecting) {
        e.target.classList.add('in')
        io.unobserve(e.target)
      }
    })
  }, { threshold: 0.15 })
  els.forEach((el) => io.observe(el))
})

useHead({ title: 'June & Hyun | Editorial Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono&family=Playfair+Display:ital,wght@0,500;0,700;1,500&family=Pretendard:wght@400;500;700&display=swap');
.invitation{max-width:540px;margin:auto;min-height:100vh;background:#f5f2ed;color:#1b1b1a;font-family:Pretendard,sans-serif}
.cover{height:100svh;min-height:650px;position:relative;overflow:hidden;background:#d8d1c7}
.cover-photo{width:100%;height:100%;object-fit:cover;object-position:center}
.topline,.cover-copy{position:absolute;z-index:1;left:24px;right:24px;display:flex;justify-content:space-between;color:#fff;font:10px 'DM Mono',monospace;letter-spacing:.08em}
.topline{top:24px}
.cover-copy{bottom:27px;display:block;text-shadow:0 2px 16px #3338}
.cover-copy p,.index{font:10px 'DM Mono',monospace;letter-spacing:.12em;margin:0 0 13px}
.cover-copy h1{font:500 clamp(58px,17vw,88px)/.78 'Playfair Display',serif;margin:0 0 17px}
.cover-copy span{font-size:11px}
.section-pad{padding:65px 24px}
.index{color:#8a8578}
.note h2,.rsvp h2,.visit h2,.gallery-head h2,.accounts h2{font:500 42px/.98 'Playfair Display',serif;margin:0;letter-spacing:-.05em}
.body{font-size:15px;line-height:1.8;margin:28px 0 0;max-width:330px;color:#3f3c37}
.signoff{margin:22px 0 0;font:italic 15px 'Playfair Display',serif;color:#6a655d}
.details{background:#1d1c1a;color:#f8f6f0}
.details .index{color:#8f887c}
.date-card{padding:22px 0;border-top:1px solid #68645e;border-bottom:1px solid #68645e;display:flex;align-items:center;gap:20px}
.date-card strong{font:500 74px/.8 'Playfair Display',serif}
.date-card div{display:grid;gap:6px;font:11px 'DM Mono',monospace;letter-spacing:.08em}
.date-card b{font:500 13px Pretendard,sans-serif}
.date-card .dday{margin-left:auto;font:600 12px 'DM Mono',monospace;letter-spacing:.1em;color:#1c1b19;background:#f1e7d6;padding:7px 11px;border-radius:2px}
.venue{display:grid;gap:9px;padding:24px 0;font-size:14px;line-height:1.6;border-bottom:1px solid #38352f}
.venue span{font:10px 'DM Mono',monospace;color:#aaa39a}
.primary{display:flex;justify-content:space-between;align-items:center;padding:17px 18px;margin-top:26px;background:#f1e7d6;color:#1c1b19;text-decoration:none;border:0;font:700 14px Pretendard,sans-serif;cursor:pointer}
.primary span{font-size:20px}
.gallery-head{padding-bottom:34px}
.gallery{padding:0 24px 8px;display:grid;gap:16px}
.gallery figure{margin:0;position:relative;overflow:hidden;background:#e2ddd4}
.gallery img{width:100%;height:100%;object-fit:cover;display:block}
.g-tall{aspect-ratio:3/4}
.g-wide{aspect-ratio:16/9}
.g-pair{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.g-pair figure{aspect-ratio:3/4}
.gallery figcaption{position:absolute;left:14px;bottom:14px;color:#fff;font:600 13px Pretendard,sans-serif;text-shadow:0 1px 10px #0007;display:grid;gap:4px}
.gallery figcaption span{font:10px 'DM Mono',monospace;letter-spacing:.1em;opacity:.85}
.reveal{opacity:0;transform:translateY(26px);transition:opacity .8s ease,transform .8s cubic-bezier(.2,.7,.2,1)}
.reveal.in{opacity:1;transform:none}
.editorial{background:#e2ddd4}
.quote{font:italic 38px/1.05 'Playfair Display',serif;margin:44px 0}
.plan>div{display:grid;grid-template-columns:66px 1fr;gap:2px;padding:17px 0;border-top:1px solid #b9b3aa}
.plan span{font:10px 'DM Mono',monospace}
.plan b{font-size:13px}
.plan p{grid-column:2;margin:4px 0 0;color:#5f5b55;font-size:12px}
.visit h2{margin-bottom:25px}
.visit p{font-size:14px;line-height:1.8}
.text-link{display:inline-block;margin-top:19px;color:inherit;font-weight:700;text-decoration:none;border-bottom:1px solid;padding-bottom:4px}
.accounts h2{margin-bottom:0}
.account-list{list-style:none;padding:0;margin:34px 0 0}
.account-list li{padding:18px 0;border-top:1px solid #d6d0c5;display:flex;justify-content:space-between;align-items:center;gap:12px}
.account-list li:last-child{border-bottom:1px solid #d6d0c5}
.account-list span{display:block;font:10px 'DM Mono',monospace;letter-spacing:.1em;color:#8a8578;margin-bottom:4px}
.account-list b{font:500 17px 'Playfair Display',serif}
.acc-num{font:12px 'DM Mono',monospace;color:#4a463f;text-align:right}
.rsvp{padding:60px 24px;background:#b9422b;color:#fff}
.rsvp .index{color:#f6cfc4}
.rsvp h2{font-size:38px;margin-bottom:28px}
.choice-row{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px}
.choice-row button{padding:14px 6px;border:1px solid #ffffff80;background:transparent;color:#fff;font:13px Pretendard,sans-serif;cursor:pointer}
.choice-row .selected{background:#fff;color:#ad3622}
.rsvp input{box-sizing:border-box;width:100%;padding:16px;margin-bottom:10px;border:1px solid #ffffff80;background:transparent;color:#fff;font:14px Pretendard,sans-serif}
.rsvp input::placeholder{color:#ffe6df}
.wide{width:100%;background:#1d1c1a;color:#fff;justify-content:center;margin-top:0}
.wide:disabled{opacity:.5;cursor:not-allowed}
.info-grid{display:grid;grid-template-columns:1fr 1fr;gap:26px 20px;margin-top:34px}
.info-grid b{display:block;font:10px 'DM Mono',monospace;letter-spacing:.1em;color:#8a8578;margin-bottom:8px}
.info-grid p{margin:0;font-size:13px;line-height:1.7;color:#3f3c37}
footer{padding:26px 24px;background:#1d1c1a;color:#fff;font:10px 'DM Mono',monospace;letter-spacing:.09em}
@media(max-width:400px){.info-grid{grid-template-columns:1fr}}
@media(min-width:541px){.invitation{box-shadow:0 0 60px #0002}}
</style>
