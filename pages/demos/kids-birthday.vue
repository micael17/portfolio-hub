<template>
  <div class="app-wrap">
    <div class="pop-card">
      <!-- 헤더 -->
      <div class="block header bg-yellow">
        <p class="kicker">YOU'RE INVITED</p>
        <h1>LEO IS TURNING 5!</h1>
        <p class="sub">레오의 다섯 번째 생일 파티에 초대합니다</p>
      </div>

      <!-- 주인공 사진 -->
      <div class="block photo bg-blue">
        <!-- AI-IMG: 밝고 컬러풀한 생일 파티 주인공 아이, 고깔모자·풍선, 환한 표정 · 4:3 -->
        <!-- prompt: cheerful little boy at his birthday party, party hat, colorful balloons, bright joyful lighting, 4:3 -->
        <img src="https://images.unsplash.com/photo-1530103862676-de8892795816?w=600&q=80" alt="생일 파티 고깔모자를 쓴 다섯 살 레오의 환하게 웃는 모습">
      </div>

      <!-- 행사 정보 -->
      <div class="block details bg-pink">
        <h2>JOIN THE FUN!</h2>
        <div class="info-line">
          <span>WHEN · 언제</span>
          <strong>2026년 11월 7일 (토) 오후 2시</strong>
          <em>2 ~ 5PM · 3시간 진행</em>
        </div>
        <div class="info-line">
          <span>WHERE · 어디서</span>
          <strong>플레이랜드 파크 파티룸 B</strong>
          <em>서울시 마포구 월드컵북로 123, 2층</em>
        </div>
        <div class="info-line">
          <span>DRESS CODE · 복장</span>
          <strong>편한 옷 & 알록달록한 색깔 환영!</strong>
          <em>마음껏 뛰어놀 수 있는 옷차림 추천</em>
        </div>
      </div>

      <!-- 오시는 길 -->
      <div class="block directions bg-cream">
        <h3>오시는 길</h3>
        <ul class="way-list">
          <li>
            <b>지하철</b>
            <span>6호선 월드컵경기장역 2번 출구에서 도보 6분</span>
          </li>
          <li>
            <b>버스</b>
            <span>월드컵파크 정류장 하차 (740, 8000번)</span>
          </li>
          <li>
            <b>주차</b>
            <span>건물 지하 주차장 2시간 무료 (파티룸에서 확인 도장)</span>
          </li>
        </ul>
        <a class="map-link" href="#" @click.prevent>지도 앱으로 위치 열기 →</a>
      </div>

      <!-- 안내 아코디언 -->
      <div class="block faq bg-mint">
        <h3>파티 안내</h3>
        <div v-for="(item, i) in faqs" :key="i" class="faq-item">
          <button class="faq-q" :aria-expanded="openFaq === i" @click="toggleFaq(i)">
            <span>{{ item.q }}</span>
            <span class="faq-icon">{{ openFaq === i ? '−' : '+' }}</span>
          </button>
          <p v-show="openFaq === i" class="faq-a">{{ item.a }}</p>
        </div>
      </div>

      <!-- 방명록 · 축하 메시지 -->
      <div class="block guestbook bg-blue">
        <h3 class="light">축하 메시지</h3>
        <p class="gb-count">{{ messages.length }}개의 메시지가 도착했어요</p>
        <ul class="gb-list">
          <li v-for="(m, i) in messages" :key="i">
            <b>{{ m.from }}</b>
            <span>{{ m.text }}</span>
          </li>
        </ul>
      </div>

      <!-- RSVP -->
      <div class="block rsvp-form bg-cream">
        <h3>참석 여부 알려주세요 (RSVP)</h3>
        <p class="rsvp-note">11월 3일까지 회신 부탁드려요</p>

        <form v-if="!sent" @submit.prevent="submitRsvp">
          <label class="field">
            <span>이름 / 가족 성함</span>
            <input v-model.trim="name" type="text" placeholder="예: 김민준 가족" required>
          </label>

          <div class="field">
            <span>참석하시나요?</span>
            <div class="choice-row">
              <button
                type="button"
                class="choice"
                :class="{ on: attending === true }"
                @click="attending = true"
              >참석해요</button>
              <button
                type="button"
                class="choice"
                :class="{ on: attending === false }"
                @click="attending = false"
              >어려워요</button>
            </div>
          </div>

          <div v-if="attending === true" class="field">
            <span>참석 인원 (어른 + 아이)</span>
            <div class="counter">
              <button type="button" @click="guests = Math.max(1, guests - 1)" aria-label="인원 줄이기">−</button>
              <strong>{{ guests }}명</strong>
              <button type="button" @click="guests = Math.min(10, guests + 1)" aria-label="인원 늘리기">+</button>
            </div>
          </div>

          <label class="field">
            <span>축하 한마디 (선택)</span>
            <textarea v-model.trim="message" rows="2" placeholder="레오에게 남길 축하 메시지를 적어주세요"></textarea>
          </label>

          <button class="btn" type="submit" :disabled="attending === null">RSVP 보내기</button>
        </form>

        <div v-else class="rsvp-done">
          <p class="done-title">회신 완료! 🎈</p>
          <p v-if="attending" class="done-body">
            <b>{{ name }}</b>님, <b>{{ guests }}명</b> 참석으로 접수되었어요.<br>
            11월 7일에 만나요!
          </p>
          <p v-else class="done-body">
            <b>{{ name }}</b>님, 회신 감사합니다.<br>
            다음 기회에 함께해요!
          </p>
          <button class="btn ghost" type="button" @click="resetRsvp">다시 작성하기</button>
        </div>
      </div>

      <!-- 답례 문구 -->
      <div class="block footer bg-black">
        <p>레오와 가족이 준비한 작은 파티,<br>함께해 주시면 큰 기쁨이 됩니다 💛</p>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Kids Birthday' })
definePageMeta({ layout: false })

const faqs = [
  { q: '아이 동반 형제·자매도 괜찮나요?', a: '물론이에요! RSVP 인원에 함께 적어주시면 좌석과 답례품을 넉넉히 준비할게요.' },
  { q: '주차는 어떻게 하나요?', a: '건물 지하 주차장을 2시간 무료로 이용하실 수 있어요. 파티룸에서 주차 확인 도장을 받아 가세요.' },
  { q: '포토테이블이 있나요?', a: '입구에 풍선 포토존과 폴라로이드 포토테이블을 마련했어요. 가족사진 꼭 남겨 가세요!' },
  { q: '답례품이 준비되나요?', a: '참석해 주신 모든 가족께 수제 쿠키 세트와 아이용 미니 선물을 답례품으로 드려요.' },
  { q: '알레르기가 있는 아이가 있어요', a: 'RSVP 메시지에 알레르기 정보를 남겨 주시면 대체 간식을 따로 준비해 드릴게요.' }
]

const messages = ref([
  { from: '민준이네', text: '레오 생일 축하해! 벌써 다섯 살이라니 🎉' },
  { from: '이모', text: '건강하고 씩씩하게 자라줘서 고마워 ❤️' },
  { from: '어린이집 친구 서아', text: '레오야 생일 축하해! 같이 놀자~' }
])

const openFaq = ref(-1)
const toggleFaq = (i) => { openFaq.value = openFaq.value === i ? -1 : i }

const name = ref('')
const attending = ref(null)
const guests = ref(2)
const message = ref('')
const sent = ref(false)

const submitRsvp = () => {
  if (attending.value === true && message.value) {
    messages.value.unshift({ from: name.value || '익명', text: message.value })
  }
  sent.value = true
}

const resetRsvp = () => {
  sent.value = false
  attending.value = null
  guests.value = 2
  message.value = ''
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Archivo+Black&family=Chivo+Mono:wght@400;700&display=swap');

.app-wrap {
  background: #e5e5e5;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 2rem 1rem;
  font-family: 'Chivo Mono', monospace;
}

.pop-card {
  max-width: 460px;
  width: 100%;
  border: 4px solid #000;
  background: #000;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.block {
  padding: 2rem;
  text-align: center;
}

.bg-yellow { background: #ffde00; }
.bg-blue { background: #005ce6; padding: 0 !important; }
.bg-pink { background: #ff007f; color: #fff; }
.bg-cream { background: #fff6e6; color: #000; text-align: left; }
.bg-mint { background: #d6fff2; color: #000; text-align: left; }
.bg-black { background: #000; }

/* 헤더 */
.kicker {
  font-weight: 700;
  letter-spacing: 0.3em;
  font-size: 0.75rem;
  color: #005ce6;
  margin-bottom: 0.75rem;
}

h1 {
  font-family: 'Archivo Black', sans-serif;
  font-size: 3rem;
  line-height: 1;
  color: #000;
  text-transform: uppercase;
}

.sub {
  margin-top: 1rem;
  font-size: 0.9rem;
  color: #000;
}

/* 사진 */
.photo img {
  width: 100%;
  height: 340px;
  object-fit: cover;
  display: block;
}

/* 행사 정보 */
h2 {
  font-family: 'Archivo Black', sans-serif;
  font-size: 2rem;
  margin-bottom: 1.75rem;
  color: #000;
}

.info-line {
  display: flex;
  flex-direction: column;
  margin-bottom: 1rem;
  background: #000;
  color: #fff;
  padding: 1rem;
  text-align: left;
}

.info-line span {
  font-size: 0.85rem;
  color: #ffde00;
  margin-bottom: 0.5rem;
  letter-spacing: 0.05em;
}

.info-line strong {
  font-size: 1.1rem;
  line-height: 1.35;
}

.info-line em {
  font-style: normal;
  font-size: 0.8rem;
  color: #b3c7ff;
  margin-top: 0.35rem;
}

/* 공통 소제목 */
h3 {
  font-family: 'Archivo Black', sans-serif;
  font-size: 1.4rem;
  margin-bottom: 1rem;
  color: #000;
}
h3.light { color: #fff; }

/* 오시는 길 */
.way-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}

.way-list li {
  display: flex;
  flex-direction: column;
  border-left: 4px solid #ff007f;
  padding-left: 0.75rem;
}

.way-list b {
  font-size: 0.85rem;
  color: #ff007f;
  margin-bottom: 0.2rem;
}

.way-list span {
  font-size: 0.9rem;
  line-height: 1.4;
}

.map-link {
  display: inline-block;
  margin-top: 1.25rem;
  font-weight: 700;
  color: #005ce6;
  text-decoration: underline;
}

/* 아코디언 */
.faq-item {
  border-bottom: 2px solid #000;
}
.faq-item:first-of-type { border-top: 2px solid #000; }

.faq-q {
  width: 100%;
  background: none;
  border: none;
  padding: 0.9rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.75rem;
  font-family: 'Chivo Mono', monospace;
  font-weight: 700;
  font-size: 0.95rem;
  text-align: left;
  cursor: pointer;
  color: #000;
}

.faq-icon {
  font-family: 'Archivo Black', sans-serif;
  font-size: 1.3rem;
  line-height: 1;
  flex-shrink: 0;
}

.faq-a {
  padding: 0 0 1rem;
  font-size: 0.88rem;
  line-height: 1.5;
  color: #0a5c47;
}

/* 방명록 */
.gb-count {
  color: #ffde00;
  font-weight: 700;
  font-size: 0.85rem;
  margin-bottom: 1rem;
  text-align: left;
}

.gb-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  text-align: left;
}

.gb-list li {
  background: #fff;
  color: #000;
  padding: 0.75rem 0.9rem;
  border: 2px solid #000;
}

.gb-list b {
  display: block;
  color: #ff007f;
  font-size: 0.8rem;
  margin-bottom: 0.25rem;
}

.gb-list span {
  font-size: 0.9rem;
  line-height: 1.4;
}

/* RSVP 폼 */
.rsvp-note {
  font-size: 0.85rem;
  margin-bottom: 1.25rem;
  color: #b3560a;
}

.field {
  display: block;
  margin-bottom: 1.1rem;
}

.field > span {
  display: block;
  font-size: 0.8rem;
  font-weight: 700;
  margin-bottom: 0.4rem;
  letter-spacing: 0.03em;
}

.field input,
.field textarea {
  width: 100%;
  border: 3px solid #000;
  padding: 0.7rem;
  font-family: 'Chivo Mono', monospace;
  font-size: 0.9rem;
  background: #fff;
  resize: vertical;
}

.field input:focus,
.field textarea:focus {
  outline: 3px solid #005ce6;
  outline-offset: 1px;
}

.choice-row {
  display: flex;
  gap: 0.5rem;
}

.choice {
  flex: 1;
  border: 3px solid #000;
  background: #fff;
  padding: 0.7rem;
  font-family: 'Chivo Mono', monospace;
  font-weight: 700;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.15s;
}

.choice.on {
  background: #ff007f;
  color: #fff;
  border-color: #ff007f;
}

.counter {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.counter button {
  width: 44px;
  height: 44px;
  border: 3px solid #000;
  background: #ffde00;
  font-family: 'Archivo Black', sans-serif;
  font-size: 1.3rem;
  line-height: 1;
  cursor: pointer;
}

.counter strong {
  font-size: 1.15rem;
  min-width: 60px;
  text-align: center;
}

.btn {
  width: 100%;
  background: #00ffcc;
  color: #000;
  border: 4px solid #000;
  padding: 1.25rem;
  font-family: 'Archivo Black', sans-serif;
  font-size: 1.25rem;
  cursor: pointer;
  transition: all 0.2s;
  margin-top: 0.5rem;
}

.btn:hover:not(:disabled) {
  background: #000;
  color: #00ffcc;
}

.btn:disabled {
  background: #cfcfcf;
  border-color: #cfcfcf;
  cursor: not-allowed;
}

.btn.ghost {
  background: #fff;
  font-size: 1rem;
  padding: 0.9rem;
}

.rsvp-done {
  text-align: center;
  padding: 1rem 0;
}

.done-title {
  font-family: 'Archivo Black', sans-serif;
  font-size: 1.6rem;
  margin-bottom: 0.75rem;
}

.done-body {
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 1.25rem;
}

/* 푸터 */
.footer p {
  color: #fff;
  font-size: 0.9rem;
  line-height: 1.6;
}

@media (max-width: 420px) {
  h1 { font-size: 2.3rem; }
  .block { padding: 1.5rem; }
}
</style>
