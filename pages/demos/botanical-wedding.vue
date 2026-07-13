<template>
  <main class="garden-invite">
    <section class="hero">
      <div class="blob one"></div>
      <div class="blob two"></div>
      <p class="kicker">Garden wedding day</p>
      <h1>서윤<br><span>+</span><br>예준</h1>
      <p class="hero-note">초록이 깊어지는 오후, 작은 정원에서 결혼식을 엽니다.</p>
      <div class="date-chip">2026.10.24 SAT 3:00 PM</div>
    </section>

    <section class="story-card">
      <div class="photo-stack">
        <img src="/images/wedding-ai/garden-couple.png" alt="AI로 생성한 정원 웨딩 커플">
        <img src="/images/wedding-ai/garden-couple-close.png" alt="AI로 생성한 야외 웨딩 포트레이트">
      </div>
      <p>
        자연스러운 웃음과 느린 대화가 있는 하루를 준비했습니다.
        바람이 지나가는 정원에서 두 사람의 새로운 시작을 함께 축복해 주세요.
      </p>
    </section>

    <section class="section">
      <div class="section-head">
        <span>DETAILS</span>
        <h2>초대 안내</h2>
      </div>
      <div class="detail-grid">
        <article v-for="item in invitationDetails" :key="item.label">
          <strong>{{ item.label }}</strong>
          <p>{{ item.value }}</p>
        </article>
      </div>
    </section>

    <section class="section schedule-section">
      <div class="section-head">
        <span>FLOW</span>
        <h2>정원의 시간표</h2>
      </div>
      <article v-for="item in timeline" :key="item.time">
        <time>{{ item.time }}</time>
        <div>
          <h3>{{ item.title }}</h3>
          <p>{{ item.body }}</p>
        </div>
      </article>
    </section>

    <section class="section card-carousel">
      <div class="section-head">
        <span>MOOD</span>
        <h2>오늘의 분위기</h2>
      </div>
      <div class="mood-row">
        <article v-for="mood in moods" :key="mood.title" :style="{ backgroundImage: `linear-gradient(rgba(31, 56, 34, 0.12), rgba(31, 56, 34, 0.52)), url('${mood.image}')` }">
          <span>{{ mood.title }}</span>
        </article>
      </div>
    </section>

    <section class="section notes">
      <div class="section-head">
        <span>NOTICE</span>
        <h2>참고해 주세요</h2>
      </div>
      <article v-for="note in guestNotes" :key="note.title">
        <h3>{{ note.title }}</h3>
        <p>{{ note.body }}</p>
      </article>
    </section>

    <section class="section map-card">
      <div class="section-head">
        <span>MAP</span>
        <h2>정원 위치</h2>
      </div>
      <iframe
        :src="mapInfo.embedUrl"
        :title="`${mapInfo.name} 지도`"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
      <h3>{{ mapInfo.name }}</h3>
      <p>{{ mapInfo.address }}</p>
      <div class="button-grid">
        <a :href="mapInfo.externalUrl" target="_blank" rel="noopener noreferrer">지도 열기</a>
        <button type="button" @click="copyText(mapInfo.address, 'address')">주소 복사</button>
      </div>
    </section>

    <section class="section">
      <div class="section-head">
        <span>ACCOUNT</span>
        <h2>마음 전하실 곳</h2>
      </div>
      <div class="account-grid">
        <article v-for="account in accountInfo" :key="account.side">
          <strong>{{ account.side }}</strong>
          <h3>{{ account.holder }}</h3>
          <p>{{ account.bank }}</p>
          <p class="account-number">{{ account.number }}</p>
          <button type="button" @click="copyText(`${account.bank} ${account.number} ${account.holder}`, account.side)">
            계좌 복사
          </button>
        </article>
      </div>
      <p v-if="copyStatus" class="copy-feedback">{{ copyStatus }}</p>
    </section>

    <section class="section guestbook">
      <div class="section-head">
        <span>GUESTBOOK</span>
        <h2>축하 메시지</h2>
      </div>
      <form @submit.prevent="submitGuestbook">
        <input v-model.trim="guestbookForm.name" type="text" placeholder="이름" maxlength="20">
        <textarea v-model.trim="guestbookForm.message" rows="4" placeholder="메시지를 남겨 주세요" maxlength="160"></textarea>
        <button type="submit">메시지 남기기</button>
      </form>
      <div class="guestbook-list">
        <article v-for="entry in paginatedGuestbookEntries" :key="entry.id">
          <div>
            <h3>{{ entry.name }}</h3>
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
const invitationDetails = [
  { label: '일시', value: '2026년 10월 24일 토요일\n오후 3시 예식' },
  { label: '장소', value: '그린하우스 가든\n경기도 남양주시 화도읍 가온로 00' },
  { label: '연회', value: '예식 후 같은 정원 안 글라스하우스에서 이어집니다.' }
]

const timeline = [
  { time: '14:30', title: '정원 입장', body: '웰컴 티와 작은 디저트를 준비했습니다.' },
  { time: '15:00', title: '본식', body: '초록 아치 아래에서 짧은 서약식을 진행합니다.' },
  { time: '16:00', title: '가든 리셉션', body: '사진 촬영과 함께 가벼운 스몰 플레이트를 나눕니다.' },
  { time: '17:30', title: '선셋 디너', body: '노을이 내려앉는 시간에 정원 디너가 시작됩니다.' }
]

const moods = [
  { title: 'Couple walk', image: '/images/wedding-ai/garden-couple.png' },
  { title: 'Garden vows', image: '/images/wedding-ai/garden-couple-close.png' },
  { title: 'After party', image: 'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=900&q=85' }
]

const guestNotes = [
  { title: '복장 안내', body: '잔디 이동이 있어 편한 구두를 추천드립니다. 밝은 그린, 아이보리, 브라운 톤이 잘 어울립니다.' },
  { title: '우천 안내', body: '비가 올 경우 글라스하우스 실내 예식으로 전환됩니다. 당일 오전 문자로 다시 안내드립니다.' },
  { title: '셔틀 안내', body: '평내호평역 2번 출구에서 오후 2시, 2시 30분 셔틀이 출발합니다.' }
]

const mapInfo = {
  name: '그린하우스 가든',
  address: '경기도 남양주시 화도읍 가온로 00',
  externalUrl: 'https://www.openstreetmap.org/?mlat=37.6528&mlon=127.3116#map=16/37.6528/127.3116',
  embedUrl: 'https://www.openstreetmap.org/export/embed.html?bbox=127.3035%2C37.6489%2C127.3197%2C37.6567&layer=mapnik&marker=37.6528%2C127.3116'
}

const accountInfo = [
  { side: '신랑측', holder: '정예준', bank: '하나은행', number: '448-910234-56707' },
  { side: '신부측', holder: '윤서윤', bank: '우리은행', number: '1002-348-567891' }
]

const guestbookForm = ref({ name: '', message: '' })
const guestbookEntries = ref([
  { id: 1, name: '강다은', message: '정원 분위기가 두 사람과 정말 잘 어울려. 따뜻한 하루가 되길 바라.', date: '2026.07.13' },
  { id: 2, name: '최지호', message: '사진만 봐도 벌써 설렌다. 초록 가득한 날 꼭 함께할게.', date: '2026.07.11' }
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

useHead({ title: '가든 스토리 모바일 청첩장' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Gowun+Dodum&display=swap');

.garden-invite {
  --leaf: #22412a;
  --stem: #6c8f45;
  --mint: #d9efcf;
  --cream: #fff8dc;
  --peach: #ffb894;
  --ink: #1d2d1f;
  max-width: 480px;
  min-height: 100vh;
  margin: 0 auto;
  overflow: hidden;
  background: linear-gradient(180deg, #f8ffd8 0%, #eff8df 36%, #fff8dc 100%);
  color: var(--ink);
  font-family: 'Gowun Dodum', sans-serif;
}

.hero {
  position: relative;
  min-height: 92svh;
  padding: 2rem 1.2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

.blob {
  position: absolute;
  border-radius: 45% 55% 60% 40%;
  filter: blur(1px);
}

.blob.one {
  top: 6%;
  left: -24%;
  width: 230px;
  height: 250px;
  background: var(--mint);
}

.blob.two {
  right: -18%;
  bottom: 12%;
  width: 210px;
  height: 210px;
  background: var(--peach);
}

.kicker,
.section-head span,
.detail-grid strong,
.account-grid strong {
  position: relative;
  z-index: 1;
  color: var(--stem);
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

h1,
h2 {
  position: relative;
  z-index: 1;
  font-family: 'Fraunces', serif;
  font-weight: 700;
  letter-spacing: -0.06em;
}

h1 {
  margin: 1rem 0;
  color: var(--leaf);
  font-size: clamp(4.6rem, 19vw, 6.5rem);
  line-height: 0.82;
}

h1 span {
  color: var(--peach);
  font-size: 2.8rem;
}

h2 {
  margin-top: 0.25rem;
  color: var(--leaf);
  font-size: 2.35rem;
}

.hero-note {
  position: relative;
  z-index: 1;
  max-width: 18rem;
  margin: 0 auto 1.4rem;
  font-size: 1.05rem;
}

.date-chip {
  position: relative;
  z-index: 1;
  width: fit-content;
  margin: 0 auto;
  border: 1px solid var(--leaf);
  border-radius: 999px;
  background: rgba(255, 248, 220, 0.74);
  padding: 0.8rem 1.1rem;
  font-weight: 700;
}

.story-card,
.section {
  margin: 1rem;
  padding: 1.2rem;
  border-radius: 30px;
  background: rgba(255, 255, 255, 0.7);
  box-shadow: 0 20px 60px rgba(65, 93, 48, 0.12);
}

.photo-stack {
  display: grid;
  grid-template-columns: 1fr 0.75fr;
  gap: 0.8rem;
  align-items: end;
  margin-bottom: 1.2rem;
}

.photo-stack img {
  width: 100%;
  height: 250px;
  border-radius: 26px;
  object-fit: cover;
}

.photo-stack img:last-child {
  height: 180px;
}

p {
  color: #586e46;
  line-height: 1.78;
  word-break: keep-all;
}

.section-head {
  margin-bottom: 1rem;
  text-align: center;
}

.detail-grid,
.account-grid,
.guestbook-list,
form {
  display: grid;
  gap: 0.8rem;
}

.detail-grid article,
.notes article,
.account-grid article,
.guestbook-list article {
  border: 1px solid rgba(108, 143, 69, 0.25);
  border-radius: 22px;
  background: rgba(255, 255, 255, 0.72);
  padding: 1rem;
}

.detail-grid p {
  white-space: pre-line;
}

.schedule-section article {
  display: grid;
  grid-template-columns: 76px 1fr;
  gap: 0.8rem;
  padding: 1rem 0;
  border-bottom: 1px dashed rgba(108, 143, 69, 0.38);
}

.schedule-section article:last-child {
  border-bottom: 0;
}

time {
  color: var(--peach);
  font-family: 'Fraunces', serif;
  font-weight: 700;
}

h3 {
  margin-bottom: 0.35rem;
  color: var(--leaf);
  font-size: 1.1rem;
}

.mood-row {
  display: flex;
  gap: 0.85rem;
  overflow-x: auto;
  padding-bottom: 0.35rem;
  scroll-snap-type: x mandatory;
}

.mood-row article {
  min-width: 72%;
  min-height: 260px;
  border-radius: 28px;
  background-position: center;
  background-size: cover;
  display: flex;
  align-items: flex-end;
  padding: 1rem;
  scroll-snap-align: center;
}

.mood-row span {
  color: #fff;
  font-family: 'Fraunces', serif;
  font-size: 1.6rem;
}

.map-card iframe {
  width: 100%;
  height: 230px;
  border: 0;
  border-radius: 24px;
  margin-bottom: 1rem;
}

.button-grid,
.account-grid,
.pagination {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.75rem;
  margin-top: 1rem;
}

a,
button {
  display: inline-block;
  width: 100%;
  border: 0;
  border-radius: 999px;
  background: var(--leaf);
  color: #fff;
  padding: 0.95rem 1rem;
  text-align: center;
  text-decoration: none;
  font: 700 0.9rem 'Gowun Dodum', sans-serif;
}

.button-grid a,
.pagination button {
  background: var(--mint);
  color: var(--leaf);
}

.account-number {
  margin: 0.25rem 0 0.9rem;
}

.copy-feedback {
  margin-top: 0.8rem;
  color: var(--stem);
  text-align: center;
}

input,
textarea {
  width: 100%;
  border: 1px solid rgba(108, 143, 69, 0.25);
  border-radius: 20px;
  background: #fff;
  padding: 1rem;
  color: var(--ink);
  font: inherit;
}

input:focus,
textarea:focus {
  border-color: var(--stem);
  outline: none;
}

.guestbook-list {
  margin-top: 1rem;
}

.guestbook-list article div {
  display: flex;
  justify-content: space-between;
  gap: 0.75rem;
}

.guestbook-list span,
.pagination span {
  color: var(--stem);
  font-size: 0.82rem;
}

.pagination {
  align-items: center;
}

.pagination span {
  text-align: center;
}

.pagination button:disabled {
  opacity: 0.45;
}

@media (max-width: 430px) {
  .photo-stack,
  .schedule-section article,
  .button-grid,
  .account-grid,
  .pagination {
    grid-template-columns: 1fr;
  }

  .photo-stack img,
  .photo-stack img:last-child {
    height: 220px;
  }
}
</style>
