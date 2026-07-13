<template>
  <main class="classic-invite">
    <section class="cover">
      <p class="small">A quiet wedding note</p>
      <div class="monogram">M<br>S</div>
      <h1>민서와 서아</h1>
      <p class="cover-copy">
        서로에게 가장 좋은 계절이 되어 주기로 약속합니다.
        소중한 분들을 모시고 조용하고 깊은 예식을 올립니다.
      </p>
      <a href="#details" class="line-button">초대장 열기</a>
    </section>

    <section class="letter">
      <figure>
        <img
          src="/images/wedding-ai/classic-couple.png"
          alt="AI로 생성한 클래식 웨딩 커플 포트레이트"
        >
        <figcaption>Minseo and Seoa, autumn 2026</figcaption>
      </figure>
      <p>
        오래 기억될 하루가 화려함보다 진심으로 채워지길 바랍니다.
        두 사람이 함께 쓰는 첫 문장에 귀한 걸음으로 함께해 주세요.
      </p>
    </section>

    <section id="details" class="section detail-section">
      <p class="small">CEREMONY</p>
      <h2>예식 안내</h2>
      <div class="detail-card" v-for="item in detailCards" :key="item.title">
        <span>{{ item.title }}</span>
        <strong>{{ item.primary }}</strong>
        <p>{{ item.secondary }}</p>
        <p>{{ item.tertiary }}</p>
      </div>
    </section>

    <section class="section">
      <p class="small">ORDER</p>
      <h2>진행 순서</h2>
      <div class="order-list">
        <article v-for="slot in timeline" :key="slot.time">
          <time>{{ slot.time }}</time>
          <div>
            <h3>{{ slot.title }}</h3>
            <p>{{ slot.description }}</p>
          </div>
        </article>
      </div>
    </section>

    <section class="section notice-section">
      <p class="small">NOTICE</p>
      <h2>하객 안내</h2>
      <article v-for="note in guestNotes" :key="note.title">
        <h3>{{ note.title }}</h3>
        <p>{{ note.body }}</p>
      </article>
    </section>

    <section class="section map-section">
      <p class="small">LOCATION</p>
      <h2>오시는 길</h2>
      <iframe
        :src="mapInfo.embedUrl"
        :title="`${mapInfo.name} 지도`"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
      <div class="map-meta">
        <h3>{{ mapInfo.name }}</h3>
        <p>{{ mapInfo.address }}</p>
      </div>
      <div class="action-grid">
        <a :href="mapInfo.externalUrl" target="_blank" rel="noopener noreferrer" class="line-button">지도 열기</a>
        <button type="button" class="line-button dark" @click="copyText(mapInfo.address, 'address')">주소 복사</button>
      </div>
    </section>

    <section class="section">
      <p class="small">THANKS</p>
      <h2>마음 전하실 곳</h2>
      <div class="account-list">
        <article v-for="account in accountInfo" :key="account.side">
          <span>{{ account.side }}</span>
          <h3>{{ account.holder }}</h3>
          <p>{{ account.bank }}</p>
          <strong>{{ account.number }}</strong>
          <button type="button" class="line-button" @click="copyText(`${account.bank} ${account.number} ${account.holder}`, account.side)">
            계좌 복사
          </button>
        </article>
      </div>
      <p v-if="copyStatus" class="copy-feedback">{{ copyStatus }}</p>
    </section>

    <section class="section guestbook">
      <p class="small">MESSAGE</p>
      <h2>축하 인사</h2>
      <form @submit.prevent="submitGuestbook">
        <input v-model.trim="guestbookForm.name" type="text" placeholder="이름" maxlength="20">
        <textarea v-model.trim="guestbookForm.message" rows="4" placeholder="축하 메시지를 남겨 주세요" maxlength="160"></textarea>
        <button type="submit" class="line-button dark">메시지 남기기</button>
      </form>
      <div class="message-list">
        <article v-for="entry in paginatedGuestbookEntries" :key="entry.id">
          <div>
            <h3>{{ entry.name }}</h3>
            <span>{{ entry.date }}</span>
          </div>
          <p>{{ entry.message }}</p>
        </article>
      </div>
      <div v-if="guestbookTotalPages > 1" class="pager">
        <button type="button" class="line-button" :disabled="guestbookPage === 1" @click="changeGuestbookPage(guestbookPage - 1)">이전</button>
        <span>{{ guestbookPage }} / {{ guestbookTotalPages }}</span>
        <button type="button" class="line-button" :disabled="guestbookPage === guestbookTotalPages" @click="changeGuestbookPage(guestbookPage + 1)">다음</button>
      </div>
    </section>
  </main>
</template>

<script setup>
const detailCards = [
  { title: '본식', primary: '2026.10.24 토요일 오후 1시', secondary: '가회재 가든홀', tertiary: '서울 종로구 북촌로 00' },
  { title: '연회', primary: '오후 2시 30분부터', secondary: '가회재 연회장', tertiary: '예식 종료 후 같은 층 이동' }
]

const timeline = [
  { time: '12:20', title: '하객 입장', description: '로비 접수와 포토 테이블을 먼저 이용해 주세요.' },
  { time: '13:00', title: '예식 시작', description: '가족 인사와 서약, 축가 순서로 차분히 진행됩니다.' },
  { time: '13:40', title: '사진 촬영', description: '가족 사진과 하객 단체 촬영이 이어집니다.' },
  { time: '14:30', title: '연회', description: '정갈한 한식 코스와 차를 준비했습니다.' }
]

const guestNotes = [
  { title: '복장', body: '차분한 정장 또는 원피스 차림을 권합니다. 밝은 베이지와 네이비 톤이 공간과 잘 어울립니다.' },
  { title: '주차', body: '건물 주차장이 협소합니다. 안국역 공영주차장 또는 대중교통 이용을 추천드립니다.' },
  { title: '동반', body: '좌석 준비를 위해 동반 인원이 있으시면 사전에 알려 주세요.' }
]

const mapInfo = {
  name: '가회재 가든홀',
  address: '서울 종로구 북촌로 00',
  externalUrl: 'https://www.openstreetmap.org/?mlat=37.5824&mlon=126.9830#map=17/37.5824/126.9830',
  embedUrl: 'https://www.openstreetmap.org/export/embed.html?bbox=126.9795%2C37.5809%2C126.9865%2C37.5839&layer=mapnik&marker=37.5824%2C126.9830'
}

const accountInfo = [
  { side: '신랑측', holder: '김민서', bank: '국민은행', number: '123-456789-01-234' },
  { side: '신부측', holder: '최서아', bank: '신한은행', number: '110-345-678901' }
]

const guestbookForm = ref({ name: '', message: '' })
const guestbookEntries = ref([
  { id: 1, name: '이수연', message: '두 분의 시작을 진심으로 축하합니다. 오래도록 다정하게 행복하세요.', date: '2026.07.13' },
  { id: 2, name: '박정우', message: '초대장 분위기가 두 사람처럼 단정하고 예뻐요. 기쁜 날 함께하겠습니다.', date: '2026.07.12' }
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

useHead({ title: '클래식 매거진 모바일 청첩장' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600;700&family=Nanum+Myeongjo:wght@400;700&display=swap');

.classic-invite {
  --paper: #f8f2e8;
  --card: #fffaf2;
  --ink: #2b261f;
  --muted: #766b5d;
  --gold: #a77b45;
  max-width: 480px;
  min-height: 100vh;
  margin: 0 auto;
  background: var(--paper);
  color: var(--ink);
  font-family: 'Nanum Myeongjo', serif;
}

.cover {
  min-height: 100svh;
  padding: 2rem 1.4rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  background:
    linear-gradient(rgba(248, 242, 232, 0.72), rgba(248, 242, 232, 0.95)),
    url('https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&fit=crop&w=1200&q=80') center/cover;
}

.small {
  color: var(--gold);
  font-family: 'Cormorant Garamond', serif;
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}

.monogram {
  width: 108px;
  height: 108px;
  margin: 2rem auto;
  border: 1px solid var(--gold);
  border-radius: 999px;
  display: grid;
  place-items: center;
  color: var(--gold);
  font: 600 2.1rem/0.85 'Cormorant Garamond', serif;
}

h1,
h2 {
  font-weight: 400;
  letter-spacing: -0.04em;
}

h1 {
  font-size: clamp(3.4rem, 14vw, 5rem);
  line-height: 1;
}

h2 {
  margin: 0.35rem 0 1.4rem;
  font-size: 2.55rem;
}

.cover-copy,
.letter p,
p {
  color: var(--muted);
  line-height: 1.9;
  word-break: keep-all;
}

.cover-copy {
  margin: 1.6rem auto 2rem;
  max-width: 19rem;
}

.line-button {
  display: inline-block;
  width: 100%;
  border: 1px solid var(--gold);
  background: transparent;
  color: var(--ink);
  padding: 0.95rem 1rem;
  text-align: center;
  text-decoration: none;
  font: 700 0.86rem 'Nanum Myeongjo', serif;
}

.line-button.dark {
  background: var(--ink);
  border-color: var(--ink);
  color: #fff;
}

.letter {
  margin: 1rem;
  padding: 2rem 1.5rem;
  border: 1px solid rgba(167, 123, 69, 0.3);
  background: var(--card);
  text-align: center;
}

.letter figure {
  margin-bottom: 1.6rem;
}

.letter img {
  width: 100%;
  height: 360px;
  object-fit: cover;
  object-position: center 30%;
  filter: sepia(0.18) saturate(0.82) contrast(1.02);
}

.letter figcaption {
  margin-top: 0.75rem;
  color: var(--gold);
  font: 600 0.82rem 'Cormorant Garamond', serif;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

.letter p {
  font-size: 1.08rem;
}

.section {
  padding: 3rem 1.25rem;
  border-top: 1px solid rgba(167, 123, 69, 0.26);
}

.detail-card,
.notice-section article,
.account-list article,
.message-list article {
  padding: 1.35rem 0;
  border-bottom: 1px solid rgba(167, 123, 69, 0.25);
}

.detail-card span,
.account-list span,
.message-list span {
  color: var(--gold);
  font-size: 0.82rem;
}

.detail-card strong,
.account-list strong {
  display: block;
  margin: 0.4rem 0;
  font-size: 1.18rem;
}

.order-list {
  display: grid;
  gap: 0.4rem;
}

.order-list article {
  display: grid;
  grid-template-columns: 74px 1fr;
  gap: 1rem;
  padding: 1rem 0;
}

.order-list time {
  color: var(--gold);
  font: 700 1rem 'Cormorant Garamond', serif;
}

h3 {
  margin-bottom: 0.35rem;
  font-size: 1.12rem;
}

.map-section iframe {
  width: 100%;
  height: 245px;
  border: 0;
  margin-bottom: 1rem;
  filter: sepia(0.2) saturate(0.85);
}

.map-meta {
  margin-bottom: 1rem;
}

.action-grid,
.account-list,
.message-list,
form {
  display: grid;
  gap: 0.8rem;
}

.action-grid {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.account-list {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.account-list article {
  border: 1px solid rgba(167, 123, 69, 0.28);
  padding: 1.2rem;
  background: var(--card);
}

.copy-feedback {
  margin-top: 1rem;
  color: var(--gold);
  text-align: center;
}

input,
textarea {
  width: 100%;
  border: 1px solid rgba(167, 123, 69, 0.35);
  background: var(--card);
  padding: 1rem;
  color: var(--ink);
  font: inherit;
}

input:focus,
textarea:focus {
  border-color: var(--gold);
  outline: none;
}

.message-list {
  margin-top: 1rem;
}

.message-list article div,
.pager {
  display: flex;
  justify-content: space-between;
  gap: 0.75rem;
}

.pager {
  align-items: center;
  margin-top: 1rem;
}

.pager button:disabled {
  opacity: 0.45;
}

@media (max-width: 430px) {
  .action-grid,
  .account-list,
  .order-list article,
  .pager {
    grid-template-columns: 1fr;
    display: grid;
  }
}
</style>
