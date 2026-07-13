<template>
  <main class="modern-invite">
    <section class="hero">
      <div class="status-bar">
        <span>INVITE 2026</span>
        <span>Seoul, KR</span>
      </div>
      <div class="hero-card">
        <img
          src="/images/wedding-ai/modern-couple.png"
          alt="AI로 생성한 모던 웨딩 커플 포트레이트"
        >
        <p class="eyebrow">우리 결혼합니다</p>
        <h1>지우<br><span>and</span><br>도현</h1>
        <p class="date">2026.10.24 Sat 5:30 PM</p>
      </div>
      <div class="quick-actions">
        <a href="#rsvp">참석 의사</a>
        <a href="#map">오시는 길</a>
      </div>
    </section>

    <section class="intro panel">
      <p>
        격식보다 우리다운 장면을 남기고 싶었습니다.
        좋아하는 음악, 가까운 사람들, 늦은 오후의 빛으로 채운 작은 파티에 초대합니다.
      </p>
    </section>

    <section class="info-strip">
      <article v-for="item in ceremonyInfo" :key="item.label">
        <span>{{ item.label }}</span>
        <strong>{{ item.value }}</strong>
        <p>{{ item.note }}</p>
      </article>
    </section>

    <section class="panel">
      <div class="section-title">
        <p class="eyebrow">TIMELINE</p>
        <h2>하루의 흐름</h2>
      </div>
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

    <section class="guide-grid">
      <article v-for="guide in guestGuides" :key="guide.title" class="guide-card">
        <span>{{ guide.icon }}</span>
        <h3>{{ guide.title }}</h3>
        <p>{{ guide.body }}</p>
      </article>
    </section>

    <section id="map" class="panel map-panel">
      <div class="section-title">
        <p class="eyebrow">LOCATION</p>
        <h2>{{ mapInfo.name }}</h2>
      </div>
      <iframe
        :src="mapInfo.embedUrl"
        :title="`${mapInfo.name} 지도`"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
      <p>{{ mapInfo.address }}</p>
      <div class="button-row">
        <a :href="mapInfo.externalUrl" target="_blank" rel="noopener noreferrer">지도 열기</a>
        <button type="button" @click="copyText(mapInfo.address, 'address')">주소 복사</button>
      </div>
    </section>

    <section id="rsvp" class="panel">
      <div class="section-title">
        <p class="eyebrow">ACCOUNT</p>
        <h2>마음 전하실 곳</h2>
      </div>
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

    <section class="panel">
      <div class="section-title">
        <p class="eyebrow">GUESTBOOK</p>
        <h2>축하 메시지</h2>
      </div>
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
  </main>
</template>

<script setup>
const ceremonyInfo = [
  { label: 'DATE', value: '10.24 SAT', note: '오후 5시 30분 예식 시작' },
  { label: 'PLACE', value: '스튜디오 레이어 17', note: '서울 성동구 성수이로 00' },
  { label: 'DRESS', value: 'Smart casual', note: '블랙, 실버, 데님 포인트 환영' }
]

const timeline = [
  { time: '17:00', title: '웰컴 체크인', body: '포토 부스와 웰컴 드링크를 먼저 즐겨 주세요.' },
  { time: '17:30', title: '세리머니', body: '짧고 선명한 서약식으로 시작합니다.' },
  { time: '18:10', title: '디너 파티', body: '스탠딩 코스와 테이블 메뉴가 함께 준비됩니다.' },
  { time: '19:30', title: '뮤직 타임', body: '두 사람이 고른 플레이리스트와 작은 공연이 이어집니다.' }
]

const guestGuides = [
  { icon: '01', title: '주차 안내', body: '건물 지하 주차는 제한적입니다. 성수역 3번 출구 도보 이동을 추천드립니다.' },
  { icon: '02', title: '동반 안내', body: '좌석과 식사 준비를 위해 동반 인원은 미리 알려 주세요.' },
  { icon: '03', title: '사진 공유', body: '촬영한 사진은 QR 앨범에 업로드해 주시면 함께 간직하겠습니다.' }
]

const mapInfo = {
  name: '스튜디오 레이어 17',
  address: '서울 성동구 성수이로 00',
  externalUrl: 'https://www.openstreetmap.org/?mlat=37.5448&mlon=127.0557#map=17/37.5448/127.0557',
  embedUrl: 'https://www.openstreetmap.org/export/embed.html?bbox=127.0515%2C37.5428%2C127.0595%2C37.5468&layer=mapnik&marker=37.5448%2C127.0557'
}

const accountInfo = [
  { side: '신랑측', holder: '김도현', bank: '카카오뱅크', number: '3333-12-3456789' },
  { side: '신부측', holder: '한지우', bank: '토스뱅크', number: '1000-2345-6789' }
]

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

useHead({ title: '모던 앱형 모바일 청첩장' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Archivo:wght@500;700;900&family=Gowun+Dodum&display=swap');

.modern-invite {
  --ink: #111216;
  --muted: #646873;
  --lime: #d8ff3e;
  --coral: #ff6d4a;
  --blue: #4f7cff;
  --paper: #f4f0e8;
  max-width: 480px;
  min-height: 100vh;
  margin: 0 auto;
  background: var(--ink);
  color: var(--ink);
  font-family: 'Gowun Dodum', sans-serif;
}

.hero {
  min-height: 100svh;
  padding: 1rem;
  display: grid;
  grid-template-rows: auto 1fr auto;
  gap: 1rem;
  background:
    radial-gradient(circle at 15% 20%, rgba(216, 255, 62, 0.9), transparent 26%),
    radial-gradient(circle at 88% 28%, rgba(255, 109, 74, 0.85), transparent 24%),
    linear-gradient(145deg, #f7f1df 0%, #dce7ff 100%);
}

.status-bar,
.quick-actions {
  display: flex;
  justify-content: space-between;
  gap: 0.75rem;
}

.status-bar span,
.quick-actions a,
.eyebrow,
.info-strip span,
.guide-card span,
.account-grid span {
  font-family: 'Archivo', sans-serif;
  font-size: 0.72rem;
  font-weight: 900;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.hero-card {
  align-self: center;
  padding: 2rem 1.4rem;
  border: 2px solid var(--ink);
  border-radius: 34px;
  background: rgba(255, 255, 255, 0.66);
  box-shadow: 10px 10px 0 var(--ink);
  backdrop-filter: blur(14px);
}

.hero-card img {
  width: 100%;
  height: 260px;
  margin-bottom: 1.4rem;
  border: 2px solid var(--ink);
  border-radius: 24px;
  object-fit: cover;
  object-position: center 35%;
  filter: saturate(1.08) contrast(1.03);
}

h1 {
  margin: 1rem 0;
  font-family: 'Archivo', sans-serif;
  font-size: clamp(4.4rem, 20vw, 6.4rem);
  font-weight: 900;
  line-height: 0.78;
  letter-spacing: -0.08em;
}

h1 span {
  display: inline-block;
  margin-left: 0.3rem;
  color: var(--blue);
  font-size: 1.3rem;
  letter-spacing: 0.02em;
}

.date {
  display: inline-flex;
  padding: 0.7rem 1rem;
  border-radius: 999px;
  background: var(--lime);
  font-family: 'Archivo', sans-serif;
  font-weight: 700;
}

.quick-actions a,
button,
.button-row a {
  border: 2px solid var(--ink);
  border-radius: 999px;
  background: var(--ink);
  color: #fff;
  padding: 0.95rem 1rem;
  text-align: center;
  text-decoration: none;
  font: 800 0.9rem 'Archivo', sans-serif;
}

.quick-actions a:first-child {
  flex: 1.2;
  background: var(--coral);
  color: var(--ink);
}

.quick-actions a:last-child {
  flex: 1;
}

.panel,
.info-strip,
.guide-grid {
  margin: 0.85rem;
}

.panel {
  padding: 1.45rem;
  border-radius: 28px;
  background: var(--paper);
}

.intro p {
  font-size: 1.25rem;
  line-height: 1.75;
  word-break: keep-all;
}

.info-strip,
.guide-grid,
.account-grid,
.guestbook-list {
  display: grid;
  gap: 0.85rem;
}

.info-strip article,
.guide-card,
.account-grid article,
.guestbook-list article {
  padding: 1.2rem;
  border-radius: 24px;
  background: #fff;
}

.info-strip strong {
  display: block;
  margin: 0.45rem 0;
  font: 900 1.45rem 'Archivo', sans-serif;
}

.section-title {
  margin-bottom: 1.2rem;
}

.section-title h2 {
  margin-top: 0.35rem;
  font-size: 2rem;
  line-height: 1.05;
}

.timeline {
  display: grid;
  gap: 1rem;
}

.timeline article {
  display: grid;
  grid-template-columns: 72px 1fr;
  gap: 0.9rem;
}

.timeline time {
  color: var(--blue);
  font: 900 1rem 'Archivo', sans-serif;
}

.timeline h3,
.guide-card h3,
.account-grid h3 {
  margin-bottom: 0.35rem;
  font-size: 1.15rem;
}

p {
  color: var(--muted);
  line-height: 1.7;
  word-break: keep-all;
}

.guide-grid {
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.guide-card span {
  color: var(--coral);
}

.map-panel iframe {
  width: 100%;
  height: 230px;
  border: 0;
  border-radius: 22px;
  margin-bottom: 1rem;
}

.button-row,
.account-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.75rem;
  margin-top: 1rem;
}

.button-row button,
.account-grid button,
.guestbook-form button,
.pagination button {
  width: 100%;
}

.button-row a,
.button-row button {
  background: #fff;
  color: var(--ink);
}

.account-grid strong {
  display: block;
  margin: 0.35rem 0 1rem;
  font-family: 'Archivo', sans-serif;
}

.copy-status {
  margin-top: 0.8rem;
  color: var(--blue);
  text-align: center;
}

.guestbook-form {
  display: grid;
  gap: 0.8rem;
  margin-bottom: 1rem;
}

.guestbook-form input,
.guestbook-form textarea {
  width: 100%;
  border: 2px solid transparent;
  border-radius: 20px;
  background: #fff;
  padding: 1rem;
  color: var(--ink);
  font: inherit;
}

.guestbook-form input:focus,
.guestbook-form textarea:focus {
  border-color: var(--blue);
  outline: none;
}

.guestbook-list article div,
.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.75rem;
}

.guestbook-list span,
.pagination span {
  color: var(--muted);
  font-size: 0.82rem;
}

.pagination {
  margin-top: 1rem;
}

.pagination button:disabled {
  opacity: 0.45;
}

@media (max-width: 430px) {
  .guide-grid,
  .account-grid,
  .button-row,
  .timeline article,
  .pagination {
    grid-template-columns: 1fr;
    display: grid;
  }
}
</style>
