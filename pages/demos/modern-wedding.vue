<template>
  <main class="modern-invite">
    <section class="hero reveal">
      <div class="status-bar">
        <span>INVITE — 2026</span>
        <span>Seoul, KR</span>
      </div>
      <div class="hero-card">
        <div class="hero-photo">
          <!-- AI-IMG: 흑백 모던 웨딩 화보, 강한 대비·도시적 · 3:4 -->
          <!-- prompt: black and white modern editorial wedding portrait, high contrast, urban minimal, 3:4 -->
          <img
            src="/images/wedding-ai/modern-couple.png"
            alt="흑백 톤의 모던 웨딩 커플 포트레이트"
          >
        </div>
        <p class="eyebrow">우리, 결혼합니다</p>
        <h1>지우<br><span>&amp;</span><br>도현</h1>
        <p class="date">2026 . 10 . 24 &nbsp;SAT &nbsp;5:30 PM</p>
      </div>
      <div class="quick-actions">
        <a href="#rsvp">참석 의사 전하기</a>
        <a href="#map">오시는 길</a>
      </div>
    </section>

    <section class="intro panel reveal">
      <p class="index">00 — GREETING</p>
      <p class="lead">
        격식보다 우리다운 하루를 남기고 싶었습니다.<br>
        좋아하는 음악과 가까운 사람들, 늦은 오후의 빛으로 채운
        작은 저녁에 두 분을 초대합니다.
      </p>
      <div class="hosts">
        <p><strong>김도현</strong> · 김성모 · 이현주 의 장남</p>
        <p><strong>한지우</strong> · 한정우 · 박수경 의 차녀</p>
      </div>
    </section>

    <section class="section reveal">
      <p class="index">01 — CEREMONY</p>
      <h2 class="display">예식 정보</h2>
      <p v-if="dday !== null" class="dday">
        예식까지 <strong>{{ dday > 0 ? `D-${dday}` : dday === 0 ? 'D-DAY' : `D+${-dday}` }}</strong>
      </p>
      <div class="info-strip">
        <article v-for="item in ceremonyInfo" :key="item.label">
          <span>{{ item.label }}</span>
          <strong>{{ item.value }}</strong>
          <p>{{ item.note }}</p>
        </article>
      </div>
    </section>

    <section class="section reveal">
      <p class="index">02 — TIMELINE</p>
      <h2 class="display">하루의 흐름</h2>
      <div class="timeline">
        <article v-for="item in timeline" :key="item.time">
          <time>{{ item.time }}</time>
          <div>
            <h3>{{ item.title }}</h3>
            <p>{{ item.body }}</p>
          </div>
        </article>
      </div>
    </section>

    <section class="section gallery-section reveal">
      <p class="index">03 — GALLERY</p>
      <h2 class="display">우리의 순간</h2>
      <div class="gallery">
        <figure class="gallery-feature">
          <!-- AI-IMG: 흑백 모던 웨딩 화보, 강한 대비·도시적 · 3:4 -->
          <!-- prompt: black and white modern editorial wedding portrait, high contrast, urban minimal, 3:4 -->
          <img
            src="/images/wedding-ai/editorial-studio-couple.png"
            alt="스튜디오에서 촬영한 흑백 웨딩 화보"
          >
        </figure>
        <figure>
          <!-- AI-IMG: 흑백 모던 웨딩 화보, 강한 대비·도시적 · 3:4 -->
          <!-- prompt: black and white modern editorial wedding portrait, high contrast, urban minimal, 3:4 -->
          <img
            src="/images/wedding-ai/archive-coast-couple.png"
            alt="도시 배경의 흑백 웨딩 스냅"
          >
        </figure>
        <figure>
          <!-- AI-IMG: 흑백 모던 웨딩 화보, 강한 대비·도시적 · 3:4 -->
          <!-- prompt: black and white modern editorial wedding portrait, high contrast, urban minimal, 3:4 -->
          <img
            src="/images/wedding-ai/signature-hotel-couple.png"
            alt="호텔 로비에서 촬영한 흑백 웨딩 화보"
          >
        </figure>
        <figure>
          <!-- AI-IMG: 흑백 모던 웨딩 화보, 강한 대비·도시적 · 3:4 -->
          <!-- prompt: black and white modern editorial wedding portrait, high contrast, urban minimal, 3:4 -->
          <img
            src="/images/wedding-ai/garden-couple.png"
            alt="야외에서 촬영한 흑백 웨딩 화보"
          >
        </figure>
        <figure>
          <!-- AI-IMG: 흑백 모던 웨딩 화보, 강한 대비·도시적 · 3:4 -->
          <!-- prompt: black and white modern editorial wedding portrait, high contrast, urban minimal, 3:4 -->
          <img
            src="/images/wedding-ai/garden-couple-close.png"
            alt="가까이서 담은 흑백 웨딩 커플 클로즈업"
          >
        </figure>
      </div>
    </section>

    <section id="map" class="section reveal">
      <p class="index">04 — LOCATION</p>
      <h2 class="display">{{ mapInfo.name }}</h2>
      <iframe
        :src="mapInfo.embedUrl"
        :title="`${mapInfo.name} 지도`"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
      <p class="addr">{{ mapInfo.address }}</p>
      <div class="button-row">
        <a :href="mapInfo.externalUrl" target="_blank" rel="noopener noreferrer">지도 열기</a>
        <button type="button" @click="copyText(mapInfo.address, 'address')">주소 복사</button>
      </div>
      <ul class="transit">
        <li v-for="line in mapInfo.transit" :key="line.label">
          <span>{{ line.label }}</span>
          <p>{{ line.body }}</p>
        </li>
      </ul>
    </section>

    <section class="section reveal">
      <p class="index">05 — GIFT</p>
      <h2 class="display">마음 전하실 곳</h2>
      <div class="account-grid">
        <article v-for="account in accountInfo" :key="account.side">
          <span>{{ account.side }}</span>
          <h3>{{ account.holder }}</h3>
          <p>{{ account.bank }}</p>
          <strong>{{ account.number }}</strong>
          <button type="button" @click="copyText(`${account.bank} ${account.number} ${account.holder}`, account.side)">
            계좌 복사
          </button>
        </article>
      </div>
      <p v-if="copyStatus" class="copy-status">{{ copyStatus }}</p>
    </section>

    <section id="rsvp" class="section reveal">
      <p class="index">06 — RSVP</p>
      <h2 class="display">참석 의사</h2>
      <p class="sub">원활한 준비를 위해 9월 30일까지 참석 여부를 알려 주세요.</p>

      <form v-if="!sent" class="rsvp-form" @submit.prevent="submitRsvp">
        <label>
          <span>성함</span>
          <input v-model.trim="rsvpForm.name" type="text" placeholder="이름을 입력해 주세요" maxlength="20" required>
        </label>
        <div class="rsvp-choice">
          <button
            v-for="side in ['신랑측', '신부측']"
            :key="side"
            type="button"
            :class="{ active: rsvpForm.side === side }"
            @click="rsvpForm.side = side"
          >{{ side }}</button>
        </div>
        <div class="rsvp-choice">
          <button
            v-for="attend in [{ v: 'yes', t: '참석합니다' }, { v: 'no', t: '어렵습니다' }]"
            :key="attend.v"
            type="button"
            :class="{ active: rsvpForm.attend === attend.v }"
            @click="rsvpForm.attend = attend.v"
          >{{ attend.t }}</button>
        </div>
        <label>
          <span>동반 인원 (본인 포함)</span>
          <input v-model.number="rsvpForm.headcount" type="number" min="1" max="10">
        </label>
        <button class="submit" type="submit">참석 의사 보내기</button>
      </form>

      <div v-else class="rsvp-done">
        <p class="done-mark">SENT</p>
        <p><strong>{{ rsvpForm.name }}</strong> 님, 감사합니다.</p>
        <p>소중한 마음 잘 전달받았습니다. 그날 반갑게 뵙겠습니다.</p>
        <button type="button" @click="sent = false">다시 작성</button>
      </div>
    </section>

    <section class="section reveal">
      <p class="index">07 — NOTICE</p>
      <h2 class="display">안내 사항</h2>
      <div class="faq">
        <article v-for="(item, i) in faqs" :key="item.q" :class="{ open: openFaq === i }">
          <button type="button" @click="toggleFaq(i)" :aria-expanded="openFaq === i">
            <span>{{ item.q }}</span>
            <em>{{ openFaq === i ? '−' : '+' }}</em>
          </button>
          <p v-show="openFaq === i">{{ item.a }}</p>
        </article>
      </div>
    </section>

    <section class="section reveal">
      <p class="index">08 — GUESTBOOK</p>
      <h2 class="display">축하 메시지</h2>
      <form class="guestbook-form" @submit.prevent="submitGuestbook">
        <input v-model.trim="guestbookForm.name" type="text" placeholder="이름" maxlength="20">
        <textarea v-model.trim="guestbookForm.message" rows="4" placeholder="메시지를 남겨 주세요" maxlength="160"></textarea>
        <button type="submit">메시지 남기기</button>
      </form>
      <div class="guestbook-list">
        <article v-for="entry in paginatedGuestbookEntries" :key="entry.id">
          <div>
            <strong>{{ entry.name }}</strong>
            <span>{{ entry.date }}</span>
          </div>
          <p>{{ entry.message }}</p>
        </article>
      </div>
      <div v-if="guestbookTotalPages > 1" class="pagination">
        <button type="button" :disabled="guestbookPage === 1" @click="changeGuestbookPage(guestbookPage - 1)">이전</button>
        <span>{{ guestbookPage }} / {{ guestbookTotalPages }}</span>
        <button type="button" :disabled="guestbookPage === guestbookTotalPages" @click="changeGuestbookPage(guestbookPage + 1)">다음</button>
      </div>
    </section>

    <footer class="foot reveal">
      <p>지우 &amp; 도현</p>
      <span>2026 . 10 . 24</span>
    </footer>
  </main>
</template>

<script setup>
const ceremonyInfo = [
  { label: 'DATE', value: '10.24 SAT', note: '오후 5시 30분 예식 시작' },
  { label: 'PLACE', value: '레이어 17', note: '서울 성동구 성수이로 00, 17층' },
  { label: 'DRESS', value: 'Smart casual', note: '블랙·그레이 톤, 편한 차림 환영' }
]

const timeline = [
  { time: '17:00', title: '웰컴 체크인', body: '포토 부스와 웰컴 드링크를 먼저 즐겨 주세요.' },
  { time: '17:30', title: '세리머니', body: '짧고 선명한 서약식으로 시작합니다.' },
  { time: '18:10', title: '디너 파티', body: '스탠딩 코스와 테이블 메뉴가 함께 준비됩니다.' },
  { time: '19:30', title: '뮤직 타임', body: '두 사람이 고른 플레이리스트와 작은 공연이 이어집니다.' }
]

const mapInfo = {
  name: '레이어 17',
  address: '서울 성동구 성수이로 00, 17층',
  externalUrl: 'https://www.openstreetmap.org/?mlat=37.5448&mlon=127.0557#map=17/37.5448/127.0557',
  embedUrl: 'https://www.openstreetmap.org/export/embed.html?bbox=127.0515%2C37.5428%2C127.0595%2C37.5468&layer=mapnik&marker=37.5448%2C127.0557',
  transit: [
    { label: '지하철', body: '2호선 성수역 3번 출구에서 도보 6분.' },
    { label: '주차', body: '건물 지하 주차 30분 무료. 만차 시 인근 공영주차장을 이용해 주세요.' }
  ]
}

const accountInfo = [
  { side: '신랑측', holder: '김도현', bank: '카카오뱅크', number: '3333-12-3456789' },
  { side: '신부측', holder: '한지우', bank: '토스뱅크', number: '1000-2345-6789' }
]

const faqs = [
  { q: '화환은 어떻게 하나요?', a: '마음만 감사히 받겠습니다. 화환 대신 따뜻한 축하의 말씀으로 대신해 주세요.' },
  { q: '식사는 준비되나요?', a: '스탠딩 코스와 테이블 메뉴가 함께 제공됩니다. 알레르기가 있으시면 RSVP에 미리 알려 주세요.' },
  { q: '아이와 함께 가도 되나요?', a: '물론입니다. 좌석과 식사 준비를 위해 동반 인원을 참석 의사에 남겨 주세요.' },
  { q: '사진은 어떻게 공유하나요?', a: '현장 QR 앨범에 촬영하신 사진을 올려 주시면 함께 간직하겠습니다.' }
]

const rsvpForm = ref({ name: '', side: '신랑측', attend: 'yes', headcount: 1 })
const sent = ref(false)

const submitRsvp = () => {
  if (!rsvpForm.value.name) return
  sent.value = true
}

const openFaq = ref(-1)
const toggleFaq = (i) => {
  openFaq.value = openFaq.value === i ? -1 : i
}

const weddingDate = new Date('2026-10-24T17:30:00+09:00')
const dday = ref(null)

const guestbookForm = ref({ name: '', message: '' })
const guestbookEntries = ref([
  { id: 1, name: '수민', message: '두 사람답게 감각적인 초대장이라 더 기대돼요. 진심으로 축하합니다.', date: '2026.07.13' },
  { id: 2, name: '태오', message: '성수에서 하는 웨딩 파티라니 꼭 갈게요. 오래오래 행복하세요.', date: '2026.07.12' }
])

const guestbookPage = ref(1)
const guestbookPageSize = 3
const guestbookTotalPages = computed(() => Math.max(1, Math.ceil(guestbookEntries.value.length / guestbookPageSize)))
const paginatedGuestbookEntries = computed(() => {
  const start = (guestbookPage.value - 1) * guestbookPageSize
  return guestbookEntries.value.slice(start, start + guestbookPageSize)
})

const copyStatus = ref('')

const copyText = async (value, key) => {
  if (!import.meta.client || !navigator.clipboard) {
    copyStatus.value = '현재 브라우저에서 복사를 지원하지 않습니다.'
    return
  }

  await navigator.clipboard.writeText(value)
  copyStatus.value = key === 'address' ? '주소를 복사했습니다.' : `${key} 계좌를 복사했습니다.`
  window.setTimeout(() => {
    copyStatus.value = ''
  }, 2000)
}

const submitGuestbook = () => {
  if (!guestbookForm.value.name || !guestbookForm.value.message) return

  guestbookEntries.value.unshift({
    id: Date.now(),
    name: guestbookForm.value.name,
    message: guestbookForm.value.message,
    date: '방금 전'
  })
  guestbookPage.value = 1
  guestbookForm.value = { name: '', message: '' }
}

const changeGuestbookPage = (page) => {
  guestbookPage.value = Math.min(Math.max(page, 1), guestbookTotalPages.value)
}

onMounted(() => {
  const today = new Date()
  const startOfToday = new Date(today.getFullYear(), today.getMonth(), today.getDate())
  const startOfWedding = new Date(weddingDate.getFullYear(), weddingDate.getMonth(), weddingDate.getDate())
  dday.value = Math.round((startOfWedding - startOfToday) / 86400000)

  const io = new IntersectionObserver((entries) => entries.forEach((entry) => {
    if (entry.isIntersecting) entry.target.classList.add('in')
  }), { threshold: 0.15 })
  document.querySelectorAll('.reveal').forEach((el) => io.observe(el))
})

useHead({ title: '모던 앱형 모바일 청첩장' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Archivo:wght@500;700;900&family=Gowun+Dodum&display=swap');

.modern-invite {
  --ink: #0a0a0b;
  --paper: #ffffff;
  --muted: #7a7c82;
  --line: #e6e6e6;
  --smoke: #f2f2f0;
  max-width: 480px;
  min-height: 100vh;
  margin: 0 auto;
  background: var(--paper);
  color: var(--ink);
  font-family: 'Gowun Dodum', sans-serif;
}

/* ---------- scroll reveal ---------- */
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.reveal.in {
  opacity: 1;
  transform: none;
}

/* ---------- shared display type ---------- */
.eyebrow,
.status-bar span,
.quick-actions a,
.index,
.info-strip span,
.account-grid span {
  font-family: 'Archivo', sans-serif;
  font-size: 0.72rem;
  font-weight: 900;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.index {
  color: var(--muted);
  margin-bottom: 0.5rem;
}

.display {
  font-family: 'Archivo', sans-serif;
  font-size: clamp(2.2rem, 11vw, 3rem);
  font-weight: 900;
  line-height: 0.92;
  letter-spacing: -0.045em;
  margin-bottom: 1.4rem;
}

/* ---------- hero ---------- */
.hero {
  min-height: 100svh;
  padding: 1.1rem;
  display: grid;
  grid-template-rows: auto 1fr auto;
  gap: 1.1rem;
  background: var(--ink);
  color: var(--paper);
}

.status-bar,
.quick-actions {
  display: flex;
  justify-content: space-between;
  gap: 0.75rem;
}

.hero-card {
  align-self: center;
  text-align: left;
}

.hero-photo {
  aspect-ratio: 3 / 4;
  margin-bottom: 1.6rem;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.24);
}

.hero-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 30%;
  filter: grayscale(1) contrast(1.08);
}

.hero .eyebrow {
  color: rgba(255, 255, 255, 0.6);
}

h1 {
  margin: 0.8rem 0 1.2rem;
  font-family: 'Archivo', sans-serif;
  font-size: clamp(4.6rem, 22vw, 7rem);
  font-weight: 900;
  line-height: 0.76;
  letter-spacing: -0.09em;
  text-transform: uppercase;
}

h1 span {
  display: inline-block;
  font-size: 1.4rem;
  font-weight: 700;
  letter-spacing: 0;
  color: rgba(255, 255, 255, 0.55);
}

.date {
  display: inline-block;
  padding: 0.6rem 0;
  color: var(--paper);
  font-family: 'Archivo', sans-serif;
  font-weight: 700;
  letter-spacing: 0.04em;
  border-top: 1px solid rgba(255, 255, 255, 0.25);
}

.quick-actions a {
  flex: 1;
  padding: 1rem;
  border: 1px solid var(--paper);
  text-align: center;
  text-decoration: none;
  color: var(--paper);
}

.quick-actions a:first-child {
  background: var(--paper);
  color: var(--ink);
}

/* ---------- sections ---------- */
.section,
.intro {
  padding: 3rem 1.4rem;
  border-top: 1px solid var(--line);
}

.intro .lead {
  font-size: 1.2rem;
  line-height: 1.9;
  color: var(--ink);
  word-break: keep-all;
}

.hosts {
  margin-top: 1.8rem;
  padding-top: 1.4rem;
  border-top: 1px solid var(--line);
}

.hosts p {
  margin: 0.35rem 0;
  color: var(--muted);
}

.hosts strong {
  color: var(--ink);
  margin-right: 0.4rem;
}

.sub,
.addr {
  color: var(--muted);
  margin-bottom: 1rem;
  word-break: keep-all;
}

/* ---------- ceremony info ---------- */
.dday {
  margin: -0.6rem 0 1.4rem;
  font: 900 0.8rem 'Archivo', sans-serif;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
}

.dday strong {
  color: var(--ink);
  font-size: 1.4rem;
  letter-spacing: -0.01em;
}

.info-strip {
  display: grid;
  gap: 0;
}

.info-strip article {
  padding: 1.2rem 0;
  border-bottom: 1px solid var(--line);
}

.info-strip article:first-child {
  border-top: 1px solid var(--line);
}

.info-strip span {
  color: var(--muted);
}

.info-strip strong {
  display: block;
  margin: 0.4rem 0;
  font: 900 1.7rem 'Archivo', sans-serif;
  letter-spacing: -0.02em;
}

/* ---------- timeline ---------- */
.timeline {
  display: grid;
  gap: 0;
}

.timeline article {
  display: grid;
  grid-template-columns: 72px 1fr;
  gap: 1rem;
  padding: 1.2rem 0;
  border-bottom: 1px solid var(--line);
}

.timeline article:first-child {
  border-top: 1px solid var(--line);
}

.timeline time {
  font: 900 1.05rem 'Archivo', sans-serif;
}

.timeline h3 {
  margin-bottom: 0.3rem;
  font-size: 1.1rem;
}

/* ---------- gallery ---------- */
.gallery {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.5rem;
}

.gallery figure {
  aspect-ratio: 3 / 4;
  overflow: hidden;
  margin: 0;
  background: var(--smoke);
}

.gallery-feature {
  grid-column: 1 / -1;
  aspect-ratio: 4 / 5;
}

.gallery img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(1) contrast(1.06);
  transition: transform 0.6s ease;
}

.gallery img:hover {
  transform: scale(1.04);
}

/* ---------- map ---------- */
iframe {
  width: 100%;
  height: 230px;
  border: 1px solid var(--line);
  margin-bottom: 1rem;
}

.transit {
  list-style: none;
  padding: 0;
  margin: 1.4rem 0 0;
}

.transit li {
  padding: 0.9rem 0;
  border-top: 1px solid var(--line);
}

.transit span {
  display: block;
  margin-bottom: 0.25rem;
  font: 900 0.72rem 'Archivo', sans-serif;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

/* ---------- buttons ---------- */
.button-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.6rem;
}

.button-row a,
button {
  font: 800 0.9rem 'Archivo', sans-serif;
  border: 1px solid var(--ink);
  padding: 0.95rem 1rem;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
}

.button-row a {
  background: var(--ink);
  color: var(--paper);
}

.button-row button {
  background: var(--paper);
  color: var(--ink);
}

/* ---------- account ---------- */
.account-grid {
  display: grid;
  gap: 0.6rem;
}

.account-grid article {
  padding: 1.3rem;
  border: 1px solid var(--line);
}

.account-grid span {
  color: var(--muted);
}

.account-grid h3 {
  margin: 0.4rem 0 0.1rem;
  font-size: 1.15rem;
}

.account-grid strong {
  display: block;
  margin: 0.35rem 0 1rem;
  font-family: 'Archivo', sans-serif;
  font-size: 1.05rem;
}

.account-grid button {
  width: 100%;
}

.copy-status {
  margin-top: 0.9rem;
  text-align: center;
  color: var(--ink);
  font-weight: 700;
}

/* ---------- rsvp ---------- */
.rsvp-form {
  display: grid;
  gap: 1rem;
}

.rsvp-form label {
  display: grid;
  gap: 0.45rem;
}

.rsvp-form label span {
  font: 900 0.72rem 'Archivo', sans-serif;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
}

.rsvp-form input {
  width: 100%;
  border: 1px solid var(--line);
  padding: 0.95rem 1rem;
  font: inherit;
  color: var(--ink);
  background: var(--paper);
}

.rsvp-form input:focus {
  outline: none;
  border-color: var(--ink);
}

.rsvp-choice {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.6rem;
}

.rsvp-choice button {
  background: var(--paper);
  color: var(--ink);
  font-family: 'Gowun Dodum', sans-serif;
  font-weight: 700;
}

.rsvp-choice button.active {
  background: var(--ink);
  color: var(--paper);
}

.rsvp-form .submit {
  background: var(--ink);
  color: var(--paper);
  width: 100%;
}

.rsvp-done {
  padding: 2.2rem 1.4rem;
  border: 1px solid var(--ink);
  text-align: center;
}

.rsvp-done .done-mark {
  font: 900 2.6rem 'Archivo', sans-serif;
  letter-spacing: 0.12em;
  margin-bottom: 0.8rem;
}

.rsvp-done p {
  color: var(--ink);
  margin-bottom: 0.4rem;
  word-break: keep-all;
}

.rsvp-done button {
  margin-top: 1.2rem;
  background: var(--paper);
  color: var(--ink);
}

/* ---------- faq ---------- */
.faq article {
  border-top: 1px solid var(--line);
}

.faq article:last-child {
  border-bottom: 1px solid var(--line);
}

.faq button {
  width: 100%;
  border: 0;
  background: none;
  padding: 1.15rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  text-align: left;
  font-family: 'Gowun Dodum', sans-serif;
  font-size: 1rem;
  font-weight: 700;
  color: var(--ink);
}

.faq button em {
  font-style: normal;
  font-family: 'Archivo', sans-serif;
  font-size: 1.4rem;
  color: var(--muted);
}

.faq p {
  padding: 0 0 1.2rem;
  color: var(--muted);
  line-height: 1.8;
  word-break: keep-all;
}

/* ---------- guestbook ---------- */
.guestbook-form {
  display: grid;
  gap: 0.7rem;
  margin-bottom: 1.4rem;
}

.guestbook-form input,
.guestbook-form textarea {
  width: 100%;
  border: 1px solid var(--line);
  padding: 1rem;
  color: var(--ink);
  background: var(--paper);
  font: inherit;
}

.guestbook-form input:focus,
.guestbook-form textarea:focus {
  outline: none;
  border-color: var(--ink);
}

.guestbook-form button {
  background: var(--ink);
  color: var(--paper);
  width: 100%;
}

.guestbook-list {
  display: grid;
  gap: 0;
}

.guestbook-list article {
  padding: 1.2rem 0;
  border-top: 1px solid var(--line);
}

.guestbook-list article div {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 0.75rem;
  margin-bottom: 0.4rem;
}

.guestbook-list span {
  color: var(--muted);
  font-size: 0.8rem;
}

.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.75rem;
  margin-top: 1.2rem;
}

.pagination span {
  color: var(--muted);
  font-size: 0.82rem;
}

.pagination button {
  flex: 1;
}

.pagination button:disabled {
  opacity: 0.35;
  cursor: default;
}

p {
  line-height: 1.7;
  word-break: keep-all;
}

/* ---------- footer ---------- */
.foot {
  padding: 3.5rem 1.4rem 4rem;
  background: var(--ink);
  color: var(--paper);
  text-align: center;
}

.foot p {
  font: 900 1.8rem 'Archivo', sans-serif;
  letter-spacing: 0.04em;
}

.foot span {
  display: block;
  margin-top: 0.5rem;
  color: rgba(255, 255, 255, 0.55);
  font-family: 'Archivo', sans-serif;
  letter-spacing: 0.14em;
}

@media (max-width: 380px) {
  .rsvp-choice,
  .button-row {
    grid-template-columns: 1fr;
  }
  .timeline article {
    grid-template-columns: 60px 1fr;
  }
}
</style>
