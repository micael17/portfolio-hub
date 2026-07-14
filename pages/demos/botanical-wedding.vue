<template>
  <main class="garden-invite">
    <section class="hero">
      <div class="blob one"></div>
      <div class="blob two"></div>
      <p class="kicker">Garden wedding day</p>
      <h1>서윤<br><span>+</span><br>예준</h1>
      <p class="hero-note">초록이 깊어지는 오후, 작은 정원에서 결혼식을 엽니다.</p>
      <div class="date-chip">2026.10.24 SAT 3:00 PM</div>
      <p v-if="dDay !== null" class="dday-hero">
        <template v-if="dDay > 0">두 사람의 정원까지 <strong>D-{{ dDay }}</strong></template>
        <template v-else-if="dDay === 0"><strong>오늘</strong>, 정원에서 만나요</template>
        <template v-else>함께해 주셔서 감사했습니다</template>
      </p>
    </section>

    <section class="story-card">
      <div class="photo-stack">
        <!-- AI-IMG: 야외 가든 웨딩 커플, 그린 식물·따뜻한 자연광 · 3:4 -->
        <!-- prompt: outdoor garden wedding couple portrait, lush greenery, warm natural light, botanical, 3:4 -->
        <img src="/images/wedding-ai/garden-couple.png" alt="정원에서 손을 맞잡고 걷는 신랑 신부">
        <!-- AI-IMG: 야외 웨딩 클로즈업 포트레이트, 자연광·초록 배경 · 3:4 -->
        <!-- prompt: outdoor wedding couple close-up portrait, soft natural light, green foliage background, botanical, 3:4 -->
        <img src="/images/wedding-ai/garden-couple-close.png" alt="자연광 아래 마주보며 웃는 두 사람">
      </div>
      <p class="greeting">
        서로의 계절을 오래 지켜봐 온 두 사람이<br>
        같은 정원을 함께 가꾸기로 했습니다.<br>
        화려한 예식 대신, 바람과 초록이 지나는 오후에<br>
        가까운 분들과 느린 하루를 나누고 싶습니다.<br>
        귀한 걸음으로 두 사람의 새로운 시작을 축복해 주세요.
      </p>
      <div class="hosts">
        <p><span>윤재호 · 김선영</span>의 딸 <strong>서윤</strong></p>
        <p><span>정민수 · 이하늘</span>의 아들 <strong>예준</strong></p>
      </div>
    </section>

    <section class="section">
      <div class="section-head">
        <span>DETAILS</span>
        <h2>예식 안내</h2>
      </div>
      <div v-if="dDay !== null && dDay >= 0" class="dday-banner">
        <span>결혼식까지</span>
        <strong>{{ dDay === 0 ? 'D-DAY' : `D-${dDay}` }}</strong>
        <span>2026년 10월 24일 토요일</span>
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

    <section class="section gallery-section">
      <div class="section-head">
        <span>GALLERY</span>
        <h2>정원의 순간들</h2>
      </div>
      <div class="gallery">
        <!-- AI-IMG: 각 이미지 소재/생성 프롬프트는 아래 galleryImages 배열의 item.prompt 참조 (모두 야외 가든 웨딩 톤 · 4:3) -->
        <figure v-for="(photo, index) in galleryImages" :key="photo.alt" class="reveal" :class="`g-${index % 3}`">
          <img :src="photo.src" :alt="photo.alt" loading="lazy">
        </figure>
      </div>
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

    <section class="section map-card">
      <div class="section-head">
        <span>LOCATION</span>
        <h2>오시는 길</h2>
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
        <a :href="mapInfo.externalUrl" target="_blank" rel="noopener noreferrer">지도 보기</a>
        <button type="button" @click="copyText(mapInfo.address, 'address')">주소 복사</button>
      </div>
      <div class="directions">
        <article v-for="way in directions.transit" :key="way.label">
          <strong>{{ way.label }}</strong>
          <p>{{ way.body }}</p>
        </article>
        <article class="parking">
          <strong>주차</strong>
          <p>{{ directions.parking }}</p>
        </article>
      </div>
    </section>

    <section class="section">
      <div class="section-head">
        <span>ACCOUNT</span>
        <h2>마음 전하실 곳</h2>
      </div>
      <p class="account-lead">참석이 어려우신 분들을 위해 계좌를 함께 안내드립니다. 축하하는 마음만으로도 충분히 감사합니다.</p>
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

    <section class="section rsvp-section">
      <div class="section-head">
        <span>RSVP</span>
        <h2>참석 회신</h2>
      </div>
      <p class="rsvp-lead">정원 좌석과 식사를 준비하는 데 큰 도움이 됩니다. 9월 30일까지 참석 여부를 알려 주세요.</p>

      <form v-if="!sent" class="rsvp-form" @submit.prevent="submitRsvp">
        <div class="chip-group" role="group" aria-label="구분">
          <button
            v-for="side in ['신랑측 하객', '신부측 하객']"
            :key="side"
            type="button"
            class="chip"
            :class="{ active: rsvpForm.side === side }"
            @click="rsvpForm.side = side"
          >{{ side }}</button>
        </div>
        <div class="chip-group" role="group" aria-label="참석 여부">
          <button
            v-for="option in ['참석', '미참석']"
            :key="option"
            type="button"
            class="chip"
            :class="{ active: rsvpForm.attendance === option }"
            @click="rsvpForm.attendance = option"
          >{{ option }}</button>
        </div>
        <input v-model.trim="rsvpForm.name" type="text" placeholder="성함" maxlength="20" aria-label="성함">
        <div class="count-row">
          <label for="rsvp-count">동반 인원(본인 포함)</label>
          <input id="rsvp-count" v-model.number="rsvpForm.headcount" type="number" min="1" max="10" inputmode="numeric">
        </div>
        <button type="submit" class="rsvp-submit">회신 보내기</button>
      </form>

      <div v-else class="rsvp-sent">
        <p class="sent-mark">🌿</p>
        <h3>회신이 전달되었어요</h3>
        <p>
          {{ rsvpForm.name || '소중한 분' }}님, {{ rsvpForm.attendance }} 의사를 잘 받았습니다.<br>
          <template v-if="rsvpForm.attendance === '참석'">정원에서 반갑게 맞이하겠습니다.</template>
          <template v-else>함께하지 못해 아쉽지만, 마음 깊이 감사드립니다.</template>
        </p>
        <button type="button" @click="resetRsvp">다시 작성하기</button>
      </div>
    </section>

    <section class="section faq-section">
      <div class="section-head">
        <span>NOTICE</span>
        <h2>안내 사항</h2>
      </div>
      <div class="faq-list">
        <article v-for="(faq, index) in faqItems" :key="faq.q" :class="{ open: openFaq === index }">
          <button type="button" class="faq-q" :aria-expanded="openFaq === index" @click="toggleFaq(index)">
            <span>{{ faq.q }}</span>
            <em aria-hidden="true">{{ openFaq === index ? '−' : '+' }}</em>
          </button>
          <p v-show="openFaq === index" class="faq-a">{{ faq.a }}</p>
        </article>
      </div>
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

    <footer class="garden-footer">
      <p class="footer-mark">🌿</p>
      <p class="footer-names">서윤 &amp; 예준</p>
      <p class="footer-date">2026. 10. 24 · 그린하우스 가든</p>
      <p class="footer-thanks">저희의 시작을 함께 기억해 주셔서 감사합니다.</p>
    </footer>
  </main>
</template>

<script setup>
const weddingDate = '2026-10-24T15:00:00'

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

const galleryImages = [
  {
    src: '/images/wedding-ai/garden-couple.png',
    alt: '햇살 드는 정원 산책로를 손잡고 함께 걷는 신랑 신부',
    prompt: 'bride and groom walking hand in hand along a sunlit garden path, lush greenery, warm afternoon light, botanical outdoor wedding, 4:3'
  },
  {
    src: '/images/wedding-ai/garden-couple-close.png',
    alt: '초록 잎 배경 앞에서 서로 마주보며 웃는 두 사람의 클로즈업',
    prompt: 'close-up of a couple smiling at each other in front of green foliage, soft natural light, intimate botanical wedding portrait, 4:3'
  },
  {
    src: 'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=900&q=85',
    alt: '유칼립투스와 흰 꽃으로 세팅한 가든 리셉션 테이블',
    prompt: 'garden reception dining table set with eucalyptus and white floral centerpieces, natural daylight, elegant outdoor wedding, 4:3'
  },
  {
    src: 'https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&fit=crop&w=900&q=85',
    alt: '초록 넝쿨과 꽃으로 장식한 야외 예식 아치',
    prompt: 'outdoor ceremony arch draped with green vines and flowers, standing on a lawn, sunny botanical wedding, 4:3'
  },
  {
    src: 'https://images.unsplash.com/photo-1465495976277-4387d4b0b4c6?auto=format&fit=crop&w=900&q=85',
    alt: '햇살이 스며드는 정원에 정돈된 하객 좌석',
    prompt: 'rows of guest chairs arranged on a garden lawn with dappled sunlight filtering through trees, outdoor wedding seating, 4:3'
  },
  {
    src: 'https://images.unsplash.com/photo-1478146896981-b80fe463b330?auto=format&fit=crop&w=900&q=85',
    alt: '들꽃과 유칼립투스 잎으로 엮은 자연스러운 신부 부케',
    prompt: 'natural bridal bouquet of wildflowers and eucalyptus leaves held in hand, soft light, botanical garden wedding, 4:3'
  }
]

const moods = [
  { title: 'Couple walk', image: '/images/wedding-ai/garden-couple.png' },
  { title: 'Garden vows', image: '/images/wedding-ai/garden-couple-close.png' },
  { title: 'After party', image: 'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=900&q=85' }
]

const mapInfo = {
  name: '그린하우스 가든',
  address: '경기도 남양주시 화도읍 가온로 00',
  externalUrl: 'https://www.openstreetmap.org/?mlat=37.6528&mlon=127.3116#map=16/37.6528/127.3116',
  embedUrl: 'https://www.openstreetmap.org/export/embed.html?bbox=127.3035%2C37.6489%2C127.3197%2C37.6567&layer=mapnik&marker=37.6528%2C127.3116'
}

const directions = {
  transit: [
    { label: '지하철', body: '경춘선 평내호평역 2번 출구에서 도보 12분. 완만한 오르막길이라 여유 있게 이동해 주세요.' },
    { label: '셔틀버스', body: '평내호평역 2번 출구 앞에서 오후 2시, 2시 30분 두 차례 운행합니다. 예식 후 복귀 셔틀은 오후 7시 출발입니다.' },
    { label: '자가용', body: '내비게이션에 "그린하우스 가든" 또는 위 주소를 입력해 주세요. 정문 진입 후 안내 요원의 수신호를 따라 주시면 됩니다.' }
  ],
  parking: '정원 내 주차장 60대 규모, 2시간 무료입니다. 만차 시 도보 3분 거리의 가온로 공영주차장을 이용해 주세요.'
}

const accountInfo = [
  { side: '신랑측', holder: '정예준', bank: '하나은행', number: '448-910234-56707' },
  { side: '신부측', holder: '윤서윤', bank: '우리은행', number: '1002-348-567891' }
]

const faqItems = [
  { q: '복장에 규정이 있나요?', a: '잔디 위 이동이 있어 편한 신발을 권해 드립니다. 밝은 그린, 아이보리, 브라운 톤이 정원과 잘 어울립니다.' },
  { q: '비가 오면 어떻게 되나요?', a: '우천 시 같은 정원 안 글라스하우스 실내 예식으로 전환됩니다. 당일 오전 9시 문자로 다시 안내드립니다.' },
  { q: '식사는 어떻게 준비되나요?', a: '예식 후 가든 리셉션에서 스몰 플레이트와 음료가 제공되고, 오후 5시 30분부터 정원 디너 코스가 이어집니다.' },
  { q: '아이와 함께 가도 되나요?', a: '물론입니다. 정원 한쪽에 아이들을 위한 놀이 공간과 유아용 의자를 마련해 두었습니다.' },
  { q: '화환이나 화분을 보내도 되나요?', a: '정원 특성상 별도 화환은 정중히 사양합니다. 축하하는 마음만으로 충분히 감사합니다.' }
]

const openFaq = ref(-1)
const toggleFaq = (index) => {
  openFaq.value = openFaq.value === index ? -1 : index
}

const rsvpForm = ref({ side: '신랑측 하객', attendance: '참석', name: '', headcount: 1 })
const sent = ref(false)

const submitRsvp = () => {
  if (!rsvpForm.value.name) return
  sent.value = true
}

const resetRsvp = () => {
  sent.value = false
  rsvpForm.value = { side: '신랑측 하객', attendance: '참석', name: '', headcount: 1 }
}

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
const dDay = ref(null)

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
  const target = new Date(weddingDate)
  const now = new Date()
  const startOfTarget = new Date(target.getFullYear(), target.getMonth(), target.getDate())
  const startOfToday = new Date(now.getFullYear(), now.getMonth(), now.getDate())
  dDay.value = Math.round((startOfTarget - startOfToday) / (1000 * 60 * 60 * 24))

  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('in')
        io.unobserve(entry.target)
      }
    })
  }, { threshold: 0.15 })
  document.querySelectorAll('.reveal').forEach((el) => io.observe(el))
})

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

.dday-hero {
  position: relative;
  z-index: 1;
  margin: 1rem auto 0;
  color: var(--leaf);
  font-size: 0.98rem;
}

.dday-hero strong {
  color: var(--peach);
  font-family: 'Fraunces', serif;
  font-size: 1.1rem;
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

.greeting {
  text-align: center;
}

.hosts {
  margin-top: 1.2rem;
  padding-top: 1.1rem;
  border-top: 1px dashed rgba(108, 143, 69, 0.38);
  text-align: center;
}

.hosts p {
  margin: 0.2rem 0;
  font-size: 0.98rem;
}

.hosts span {
  color: var(--stem);
}

.hosts strong {
  color: var(--leaf);
}

.section-head {
  margin-bottom: 1rem;
  text-align: center;
}

.dday-banner {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.2rem;
  margin-bottom: 1.1rem;
  padding: 1rem;
  border-radius: 22px;
  background: rgba(217, 239, 207, 0.55);
}

.dday-banner span {
  color: var(--stem);
  font-size: 0.85rem;
}

.dday-banner strong {
  color: var(--leaf);
  font-family: 'Fraunces', serif;
  font-size: 2.4rem;
  line-height: 1;
  letter-spacing: -0.04em;
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

.gallery {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.7rem;
}

.gallery figure {
  margin: 0;
  border-radius: 22px;
  overflow: hidden;
}

.gallery figure.g-0 {
  grid-column: span 2;
}

.gallery img {
  display: block;
  width: 100%;
  height: 100%;
  min-height: 160px;
  object-fit: cover;
}

.gallery figure.g-0 img {
  min-height: 220px;
}

.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}

.reveal.in {
  opacity: 1;
  transform: none;
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

.directions {
  display: grid;
  gap: 0.7rem;
  margin-top: 1.1rem;
}

.directions article {
  border: 1px solid rgba(108, 143, 69, 0.25);
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.72);
  padding: 0.9rem 1rem;
}

.directions strong {
  display: block;
  margin-bottom: 0.3rem;
  color: var(--leaf);
  font-size: 0.95rem;
}

.directions .parking {
  background: rgba(217, 239, 207, 0.4);
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

.account-lead,
.rsvp-lead {
  margin-bottom: 1rem;
  text-align: center;
  font-size: 0.95rem;
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

.chip-group {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.6rem;
}

.chip {
  border: 1px solid rgba(108, 143, 69, 0.4);
  background: rgba(255, 255, 255, 0.72);
  color: var(--stem);
  padding: 0.85rem 1rem;
}

.chip.active {
  background: var(--leaf);
  border-color: var(--leaf);
  color: #fff;
}

.count-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.8rem;
  padding: 0.4rem 0.2rem;
}

.count-row label {
  color: var(--leaf);
  font-size: 0.95rem;
}

.count-row input {
  width: 92px;
  text-align: center;
  padding: 0.75rem;
}

.rsvp-submit {
  margin-top: 0.3rem;
}

.rsvp-sent {
  text-align: center;
  padding: 0.5rem 0 0.2rem;
}

.rsvp-sent .sent-mark {
  font-size: 2.2rem;
}

.rsvp-sent h3 {
  margin: 0.4rem 0 0.6rem;
  font-size: 1.35rem;
}

.rsvp-sent button {
  width: fit-content;
  margin: 1rem auto 0;
  padding: 0.8rem 1.6rem;
  background: var(--mint);
  color: var(--leaf);
}

.faq-list {
  display: grid;
  gap: 0.6rem;
}

.faq-list article {
  border: 1px solid rgba(108, 143, 69, 0.25);
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.72);
  overflow: hidden;
}

.faq-q {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.8rem;
  width: 100%;
  border-radius: 0;
  background: transparent;
  color: var(--leaf);
  text-align: left;
  padding: 1rem 1.1rem;
  font-size: 0.98rem;
}

.faq-q em {
  color: var(--stem);
  font-style: normal;
  font-family: 'Fraunces', serif;
  font-size: 1.4rem;
  line-height: 1;
}

.faq-a {
  padding: 0 1.1rem 1.05rem;
  font-size: 0.94rem;
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

.garden-footer {
  padding: 2.4rem 1.2rem 3rem;
  text-align: center;
}

.garden-footer .footer-mark {
  font-size: 1.6rem;
}

.garden-footer .footer-names {
  margin-top: 0.4rem;
  color: var(--leaf);
  font-family: 'Fraunces', serif;
  font-size: 1.8rem;
  letter-spacing: -0.04em;
}

.garden-footer .footer-date {
  margin-top: 0.3rem;
  color: var(--stem);
  font-size: 0.9rem;
}

.garden-footer .footer-thanks {
  margin-top: 0.9rem;
  font-size: 0.9rem;
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
