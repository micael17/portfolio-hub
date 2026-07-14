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
        <!-- AI-IMG: 클래식 웨딩 커플 대표 포트레이트 · 세피아 필름 톤, 차분한 무드 · 3:4 -->
        <!-- prompt: A timeless film-style portrait of a Korean couple in elegant formal wedding attire, warm sepia tones, soft natural window light, quiet and intimate mood, shallow depth of field, hanok interior background, 3:4 aspect ratio -->
        <img
          src="/images/wedding-ai/classic-couple.png"
          alt="정장 차림으로 마주 서 웃고 있는 신랑 민서와 신부 서아의 클래식 웨딩 포트레이트"
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
      <p class="dday">
        2026. 10. 24 SAT
        <span v-if="dDay !== ''"> · 예식까지 <strong>D-{{ dDay }}</strong></span>
      </p>
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

    <section class="section gallery-section">
      <p class="small">GALLERY</p>
      <h2>사진첩</h2>
      <p class="section-lead">본식을 앞두고 담은 스튜디오와 야외 촬영 컷입니다. 편안한 마음으로 둘러봐 주세요.</p>
      <div class="gallery-grid">
        <figure class="gallery-item wide">
          <!-- AI-IMG: 가든 야외에서 손을 맞잡은 커플 · 오후 자연광, 따뜻한 톤 · 3:2 -->
          <!-- prompt: A Korean couple holding hands in a lush garden during golden hour, natural warm light, romantic and calm mood, wearing elegant wedding attire, 3:2 aspect ratio -->
          <img src="/images/wedding-ai/garden-couple.png" alt="가든에서 손을 맞잡고 걷는 신랑 신부의 야외 촬영 사진" loading="lazy">
        </figure>
        <figure class="gallery-item">
          <!-- AI-IMG: 야외 클로즈업, 마주 본 두 사람 · 얕은 심도, 부드러운 무드 · 1:1 -->
          <!-- prompt: A close-up of a Korean couple facing each other in a garden, soft focus background, shallow depth of field, intimate expressions, 1:1 aspect ratio -->
          <img src="/images/wedding-ai/garden-couple-close.png" alt="정원에서 마주 보며 미소 짓는 신랑 신부의 클로즈업 사진" loading="lazy">
        </figure>
        <figure class="gallery-item">
          <!-- AI-IMG: 스튜디오 에디토리얼 촬영 · 미니멀 배경, 세련된 톤 · 1:1 -->
          <!-- prompt: An editorial studio photograph of a Korean couple in formal attire, minimal neutral backdrop, refined and modern styling, soft studio lighting, 1:1 aspect ratio -->
          <img src="/images/wedding-ai/editorial-studio-couple.png" alt="미니멀한 스튜디오 배경에서 촬영한 신랑 신부의 에디토리얼 사진" loading="lazy">
        </figure>
        <figure class="gallery-item">
          <!-- AI-IMG: 호텔 시그니처 공간 촬영 · 우아한 인테리어, 차분한 톤 · 1:1 -->
          <!-- prompt: A Korean couple posing in an elegant hotel interior, warm ambient lighting, classic and sophisticated atmosphere, formal wedding attire, 1:1 aspect ratio -->
          <img src="/images/wedding-ai/signature-hotel-couple.png" alt="우아한 호텔 실내에서 촬영한 신랑 신부의 웨딩 사진" loading="lazy">
        </figure>
        <figure class="gallery-item wide">
          <!-- AI-IMG: 해안가 야외 촬영 · 자연 배경, 여유로운 무드 · 3:2 -->
          <!-- prompt: A Korean couple walking along a quiet coastline, soft overcast light, serene and airy mood, elegant casual wedding attire, wide horizon, 3:2 aspect ratio -->
          <img src="/images/wedding-ai/archive-coast-couple.png" alt="바닷가를 나란히 걷는 신랑 신부의 야외 촬영 사진" loading="lazy">
        </figure>
      </div>
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
        <p class="map-tel">문의 02-000-0000</p>
      </div>
      <ul class="transit-list">
        <li v-for="t in transitInfo" :key="t.label">
          <span>{{ t.label }}</span>
          <p>{{ t.body }}</p>
        </li>
      </ul>
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

    <section class="section rsvp-section">
      <p class="small">RSVP</p>
      <h2>참석 의사 전달</h2>
      <p class="section-lead">좌석과 식사 준비를 위해 <strong>9월 30일</strong>까지 참석 여부를 알려 주시면 감사하겠습니다.</p>
      <form class="rsvp-form" @submit.prevent="sent = true">
        <div class="radio-row">
          <label :class="{ on: rsvp.side === '신랑측' }"><input type="radio" value="신랑측" v-model="rsvp.side" :disabled="sent"> 신랑측 하객</label>
          <label :class="{ on: rsvp.side === '신부측' }"><input type="radio" value="신부측" v-model="rsvp.side" :disabled="sent"> 신부측 하객</label>
        </div>
        <input v-model.trim="rsvp.name" type="text" placeholder="성함" maxlength="20" :disabled="sent">
        <div class="radio-row">
          <label :class="{ on: rsvp.attend === '참석' }"><input type="radio" value="참석" v-model="rsvp.attend" :disabled="sent"> 참석합니다</label>
          <label :class="{ on: rsvp.attend === '불참' }"><input type="radio" value="불참" v-model="rsvp.attend" :disabled="sent"> 참석이 어렵습니다</label>
        </div>
        <div class="rsvp-count">
          <label for="rsvp-count">동반 인원 (본인 포함)</label>
          <select id="rsvp-count" v-model.number="rsvp.count" :disabled="sent">
            <option v-for="n in 6" :key="n" :value="n">{{ n }}명</option>
          </select>
        </div>
        <label class="rsvp-meal"><input type="checkbox" v-model="rsvp.meal" :disabled="sent"> 예식 후 식사할 예정입니다</label>
        <button type="submit" class="line-button dark" :disabled="sent">{{ sent ? '참석 의사가 접수되었습니다' : '참석 의사 보내기' }}</button>
      </form>
      <p v-if="sent" class="rsvp-thanks">소중한 응답 감사합니다. 예식 3일 전 안내 문자를 다시 보내 드릴게요.</p>
    </section>

    <section class="section faq-section">
      <p class="small">NOTICE</p>
      <h2>안내 사항</h2>
      <div class="faq-list">
        <div class="faq-item" v-for="(faq, i) in faqItems" :key="faq.q">
          <button type="button" class="faq-q" :aria-expanded="openFaq === i" @click="openFaq = openFaq === i ? -1 : i">
            <span>{{ faq.q }}</span>
            <em aria-hidden="true">{{ openFaq === i ? '−' : '+' }}</em>
          </button>
          <p class="faq-a" v-show="openFaq === i">{{ faq.a }}</p>
        </div>
      </div>
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

    <footer class="invite-footer">
      <div class="monogram footer-mono">M<br>S</div>
      <p class="footer-names">민서 · 서아</p>
      <p class="footer-date">2026. 10. 24 SATURDAY PM 1:00</p>
      <p class="footer-note">
        귀한 걸음으로 축복해 주시는 모든 분께 깊이 감사드립니다.
        두 사람, 서로에게 다정한 하루하루로 보답하겠습니다.
      </p>
      <button type="button" class="line-button" @click="copyText(shareUrl, 'link')">청첩장 링크 복사</button>
      <p v-if="copyStatus" class="copy-feedback">{{ copyStatus }}</p>
      <small class="footer-credit">Minseo &amp; Seoa · Wedding Invitation</small>
    </footer>
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

const weddingDate = new Date('2026-10-24T00:00:00+09:00')
const dDay = ref('')
onMounted(() => {
  const today = new Date()
  today.setHours(0, 0, 0, 0)
  const diff = Math.round((weddingDate.getTime() - today.getTime()) / 86400000)
  dDay.value = diff > 0 ? diff : 'Day'
})

const transitInfo = [
  { label: '지하철', body: '3호선 안국역 2번 출구에서 도보 6분. 출구 앞 안내 표지판을 따라오시면 됩니다.' },
  { label: '버스', body: '간선 109·151·162번 또는 종로02 마을버스 이용 후 재동초등학교 정류장에서 하차해 주세요.' },
  { label: '자가용', body: '내비게이션에 “가회재 가든홀”을 검색하세요. 건물 주차는 20대 규모로 협소하니, 만차 시 안국역 공영주차장(예식 2시간 무료 등록)을 이용해 주세요.' }
]

const openFaq = ref(0)
const faqItems = [
  { q: '주차는 어떻게 하나요?', a: '건물 지하 주차장은 20대 규모로 예식 시작 30분 전에는 만차가 되는 편입니다. 안국역 공영주차장(예식 2시간 무료 등록)이나 대중교통 이용을 권해 드립니다.' },
  { q: '식사는 제공되나요?', a: '예식 종료 후 같은 층 연회장에서 정갈한 한식 코스를 준비했습니다. 좌석 배정을 위해 위 RSVP에서 식사 여부를 함께 남겨 주세요.' },
  { q: '화환을 보내고 싶어요.', a: '마음은 감사하지만 공간이 협소하여 화환은 정중히 사양합니다. 축하의 마음은 마음 전하실 곳으로 대신해 주시면 소중히 간직하겠습니다.' },
  { q: '포토부스나 사진 촬영이 있나요?', a: '로비에 셀프 포토부스를 운영하며, 촬영한 사진은 현장 QR로 바로 내려받을 수 있습니다. 예식 중에는 원활한 진행을 위해 지정 포토존에서만 촬영을 부탁드립니다.' },
  { q: '복장 권장 사항이 있나요?', a: '차분한 정장이나 원피스 차림이면 충분합니다. 밝은 베이지와 네이비 톤이 한옥 공간과 잘 어우러집니다.' },
  { q: '아이와 함께 가도 될까요?', a: '물론입니다. 다만 좌석과 유아용 의자 준비를 위해 동반 인원을 RSVP에 미리 남겨 주시면 감사하겠습니다.' }
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

const shareUrl = 'https://invite.example.com/minseo-seoa'
const sent = ref(false)
const rsvp = ref({ side: '신랑측', name: '', attend: '참석', count: 1, meal: true })

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
  copyStatus.value =
    key === 'address' ? '주소를 복사했습니다.'
      : key === 'link' ? '청첩장 링크를 복사했습니다.'
        : `${key} 계좌를 복사했습니다.`
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

.dday {
  margin-bottom: 1.6rem;
  color: var(--ink);
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.05rem;
  letter-spacing: 0.06em;
}

.dday strong {
  color: var(--gold);
  font-size: 1.3rem;
}

.section-lead {
  margin-bottom: 1.6rem;
  color: var(--muted);
  line-height: 1.85;
}

.section-lead strong {
  color: var(--gold);
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.6rem;
}

.gallery-item {
  margin: 0;
  overflow: hidden;
}

.gallery-item.wide {
  grid-column: 1 / -1;
}

.gallery-item img {
  display: block;
  width: 100%;
  height: 220px;
  object-fit: cover;
  filter: sepia(0.16) saturate(0.85) contrast(1.02);
}

.gallery-item.wide img {
  height: 250px;
}

.transit-list {
  list-style: none;
  padding: 0;
  margin: 0 0 1.2rem;
  display: grid;
  gap: 0.9rem;
}

.transit-list li {
  display: grid;
  grid-template-columns: 60px 1fr;
  gap: 0.75rem;
  align-items: baseline;
}

.transit-list span {
  color: var(--gold);
  font-weight: 700;
  font-size: 0.9rem;
}

.map-tel {
  margin-top: 0.35rem;
  font-size: 0.92rem;
}

.faq-list {
  display: grid;
  gap: 0;
}

.faq-item {
  border-bottom: 1px solid rgba(167, 123, 69, 0.25);
}

.faq-q {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 1.15rem 0;
  border: 0;
  background: transparent;
  color: var(--ink);
  text-align: left;
  cursor: pointer;
  font: 700 1.02rem 'Nanum Myeongjo', serif;
}

.faq-q em {
  flex-shrink: 0;
  color: var(--gold);
  font-style: normal;
  font-size: 1.3rem;
}

.faq-a {
  padding: 0 0 1.2rem;
  font-size: 0.98rem;
}

.rsvp-form {
  display: grid;
  gap: 0.85rem;
}

.radio-row {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.6rem;
}

.radio-row label {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.4rem;
  padding: 0.85rem;
  border: 1px solid rgba(167, 123, 69, 0.35);
  background: var(--card);
  cursor: pointer;
  font-size: 0.95rem;
}

.radio-row label.on {
  border-color: var(--gold);
  background: rgba(167, 123, 69, 0.12);
}

.radio-row input {
  width: auto;
  accent-color: var(--gold);
}

.rsvp-count {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.rsvp-count label {
  color: var(--muted);
  font-size: 0.95rem;
}

.rsvp-count select {
  width: auto;
  border: 1px solid rgba(167, 123, 69, 0.35);
  background: var(--card);
  padding: 0.7rem 1rem;
  color: var(--ink);
  font: inherit;
}

.rsvp-meal {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: var(--muted);
  font-size: 0.95rem;
  cursor: pointer;
}

.rsvp-meal input {
  width: auto;
  accent-color: var(--gold);
}

.rsvp-thanks {
  margin-top: 1rem;
  color: var(--gold);
  text-align: center;
  line-height: 1.8;
}

.invite-footer {
  padding: 3rem 1.25rem 3.5rem;
  border-top: 1px solid rgba(167, 123, 69, 0.26);
  text-align: center;
}

.footer-mono {
  width: 78px;
  height: 78px;
  margin: 0 auto 1.4rem;
  font-size: 1.5rem;
}

.footer-names {
  color: var(--ink);
  font-size: 1.35rem;
  letter-spacing: 0.1em;
}

.footer-date {
  margin-top: 0.35rem;
  color: var(--gold);
  font: 600 0.85rem 'Cormorant Garamond', serif;
  letter-spacing: 0.12em;
}

.footer-note {
  margin: 1.2rem auto 1.6rem;
  max-width: 20rem;
  font-size: 0.98rem;
}

.footer-credit {
  display: block;
  margin-top: 1.6rem;
  color: var(--muted);
  font: 600 0.75rem 'Cormorant Garamond', serif;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

@media (max-width: 430px) {
  .action-grid,
  .account-list,
  .order-list article,
  .pager {
    grid-template-columns: 1fr;
    display: grid;
  }

  .gallery-item img {
    height: 180px;
  }
}
</style>
