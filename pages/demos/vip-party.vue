<template>
  <div class="app-wrap">
    <!-- ===== HERO: 초청장 ===== -->
    <header class="hero">
      <div class="hero-bg">
        <!-- AI-IMG: 럭셔리 VIP 갈라 파티 홀, 골드·딥블랙·샴페인 · 16:9 -->
        <!-- prompt: luxury VIP gala party ballroom, gold and deep black, champagne, elegant evening, 16:9 -->
        <img
          src="https://images.unsplash.com/photo-1519671482749-fd09be7ccebf?w=1600&q=80"
          alt="샹들리에가 빛나는 갈라 연회장 전경"
        >
        <div class="hero-scrim"></div>
      </div>

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
              <span class="val">7:00 PM</span>
            </div>
            <div class="row">
              <span class="label">VENUE</span>
              <span class="val">시그니엘 서울</span>
            </div>
            <div class="row">
              <span class="label">DRESS</span>
              <span class="val">BLACK TIE</span>
            </div>
          </div>

          <a href="#rsvp" class="rsvp">ACCEPT INVITATION</a>
        </div>
      </div>
    </header>

    <!-- ===== 지표 카운트업 ===== -->
    <section class="metrics numbers">
      <div class="metric">
        <strong>{{ display.guests }}</strong>
        <span>초청 인원</span>
      </div>
      <div class="metric">
        <strong>{{ display.programs }}</strong>
        <span>프로그램</span>
      </div>
      <div class="metric">
        <strong>{{ display.years }}</strong>
        <span>연속 개최</span>
      </div>
      <div class="metric">
        <strong>{{ display.hours }}</strong>
        <span>운영 시간</span>
      </div>
    </section>

    <!-- ===== 행사 개요 ===== -->
    <section class="overview">
      <p class="eyebrow">THE INVITATION</p>
      <h2>한 해의 마지막 밤,<br>가장 가까운 분들과 함께합니다.</h2>
      <p class="lede">
        THE GALA는 브랜드와 오랜 시간을 함께해 주신 VIP 멤버 200분을 모시는
        연말 초청 행사입니다. 미쉐린 셰프의 코스 디너, 라이브 오케스트라,
        그리고 새해를 맞이하는 카운트다운까지 — 잊지 못할 하룻밤을 준비했습니다.
      </p>

      <div class="ov-grid">
        <div class="ov-item">
          <span class="ov-label">일시</span>
          <p class="ov-val">2026년 12월 31일 (목)</p>
          <p class="ov-sub">오후 7:00 입장 · 오후 8:00 개회</p>
        </div>
        <div class="ov-item">
          <span class="ov-label">장소</span>
          <p class="ov-val">시그니엘 서울 그랜드볼룸</p>
          <p class="ov-sub">서울 송파구 올림픽로 300, 76F</p>
        </div>
        <div class="ov-item">
          <span class="ov-label">드레스코드</span>
          <p class="ov-val">Black Tie</p>
          <p class="ov-sub">남성 턱시도 · 여성 이브닝 가운</p>
        </div>
        <div class="ov-item">
          <span class="ov-label">동반</span>
          <p class="ov-val">1인 동반 가능</p>
          <p class="ov-sub">사전 RSVP 등록 필수</p>
        </div>
      </div>
    </section>

    <!-- ===== 프로그램 타임라인 (탭) ===== -->
    <section class="program">
      <p class="eyebrow center">THE EVENING</p>
      <h2 class="center">프로그램 타임라인</h2>

      <div class="tabs">
        <button
          v-for="(t, i) in tabs"
          :key="t.key"
          :class="['tab', { active: tab === i }]"
          @click="tab = i"
        >
          {{ t.label }}
        </button>
      </div>

      <div class="timeline">
        <div v-for="item in tabs[tab].items" :key="item.time" class="tl-row">
          <span class="tl-time">{{ item.time }}</span>
          <div class="tl-body">
            <strong>{{ item.title }}</strong>
            <p>{{ item.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== 참석 혜택 ===== -->
    <section class="perks">
      <div class="perks-copy">
        <p class="eyebrow">EXCLUSIVE FOR YOU</p>
        <h2>초대받은 분께만<br>드리는 특별함.</h2>
        <ul>
          <li>
            <strong>미쉐린 코스 디너</strong>
            <span>총괄 셰프가 이 밤만을 위해 준비한 5코스 만찬</span>
          </li>
          <li>
            <strong>웰컴 샴페인 &amp; 발렛</strong>
            <span>입장 시 프리미엄 샴페인, 전 좌석 무료 발렛 제공</span>
          </li>
          <li>
            <strong>리미티드 기프트</strong>
            <span>200개 한정 제작된 시그니처 기념 패키지 증정</span>
          </li>
          <li>
            <strong>프라이빗 라운지</strong>
            <span>VVIP 전용 라운지 및 전담 컨시어지 서비스</span>
          </li>
        </ul>
      </div>
      <div class="perks-img">
        <!-- AI-IMG: 골드 톤 샴페인 타워와 미쉐린 코스 디너, 딥블랙 배경 · 16:9 -->
        <!-- prompt: champagne tower and Michelin fine dining plate, gold tones, deep black background, luxury gala, 16:9 -->
        <img
          src="https://images.unsplash.com/photo-1510812431401-41d2bd2722f3?w=1000&q=80"
          alt="골드 조명 아래 샴페인 잔과 코스 디너"
        >
      </div>
    </section>

    <!-- ===== 오시는 길 ===== -->
    <section class="access">
      <p class="eyebrow center">GETTING HERE</p>
      <h2 class="center">오시는 길</h2>
      <div class="access-grid">
        <div class="ac-item">
          <span class="ac-tag">주소</span>
          <p>서울 송파구 올림픽로 300<br>시그니엘 서울 76층 그랜드볼룸</p>
        </div>
        <div class="ac-item">
          <span class="ac-tag">발렛 파킹</span>
          <p>정문 발렛 데스크에서 초청장을 제시해 주세요.<br>전 참석자 무료 발렛이 제공됩니다.</p>
        </div>
        <div class="ac-item">
          <span class="ac-tag">지하철</span>
          <p>2·8호선 잠실역 1·2번 출구 직결<br>롯데월드타워 전용 엘리베이터 이용</p>
        </div>
      </div>
    </section>

    <!-- ===== RSVP ===== -->
    <section id="rsvp" class="rsvp-section">
      <div class="rsvp-frame">
        <p class="eyebrow center">R.S.V.P</p>
        <h2 class="center">참석 여부를 알려주세요</h2>
        <p class="rsvp-note">2026년 12월 20일까지 회신 부탁드립니다.</p>

        <form v-if="!sent" class="rsvp-form" @submit.prevent="sent = true">
          <label>
            성함
            <input type="text" required placeholder="홍길동">
          </label>
          <label>
            연락처
            <input type="tel" required placeholder="010-0000-0000">
          </label>

          <fieldset class="attend">
            <span class="fs-label">참석 여부</span>
            <div class="opts">
              <label class="opt">
                <input type="radio" name="attend" value="yes" checked>
                <span>참석합니다</span>
              </label>
              <label class="opt">
                <input type="radio" name="attend" value="no">
                <span>참석이 어렵습니다</span>
              </label>
            </div>
          </fieldset>

          <label>
            동반 인원
            <select>
              <option value="0">동반 없음 (본인만)</option>
              <option value="1">1인 동반</option>
            </select>
          </label>

          <label>
            식이 요청사항 (선택)
            <input type="text" placeholder="알러지, 채식 등">
          </label>

          <button type="submit" class="rsvp submit">RSVP 제출하기</button>
        </form>

        <div v-else class="rsvp-done">
          <div class="done-mark">✓</div>
          <h3>회신이 접수되었습니다</h3>
          <p>THE GALA 2026에서 뵙기를 기다리겠습니다.<br>확인 안내를 문자로 보내드립니다.</p>
          <button class="rsvp ghost" @click="sent = false">다시 작성하기</button>
        </div>
      </div>
    </section>

    <!-- ===== 문의 (FAQ 아코디언) ===== -->
    <section class="faq">
      <p class="eyebrow center">INQUIRIES</p>
      <h2 class="center">자주 묻는 질문</h2>
      <div class="faq-list">
        <div
          v-for="(f, i) in faqs"
          :key="f.q"
          :class="['faq-item', { open: openFaq === i }]"
        >
          <button class="faq-q" @click="openFaq = openFaq === i ? -1 : i">
            <span>{{ f.q }}</span>
            <span class="faq-icon">{{ openFaq === i ? '−' : '+' }}</span>
          </button>
          <p v-show="openFaq === i" class="faq-a">{{ f.a }}</p>
        </div>
      </div>

      <div class="contact">
        <p>추가 문의는 전담 컨시어지에게 연락 주세요.</p>
        <a href="tel:0215884000">02-1588-4000</a>
        <span>vip@thegala2026.com · 평일 10:00–18:00</span>
      </div>
    </section>

    <footer class="foot">
      <p>THE GALA 2026</p>
      <span>© 2026 THE GALA. Strictly by invitation.</span>
    </footer>
  </div>
</template>

<script setup>
useHead({ title: 'THE GALA 2026 · VIP Invitation' })
definePageMeta({ layout: false })

const tab = ref(0)
const openFaq = ref(-1)
const sent = ref(false)

const tabs = [
  {
    key: 'reception',
    label: '리셉션',
    items: [
      { time: '7:00 PM', title: '입장 & 웰컴 샴페인', desc: '76층 로비에서 웰컴 드링크와 함께 손님을 맞이합니다.' },
      { time: '7:30 PM', title: '포토 & 라운지', desc: '시그니처 포토월과 프라이빗 라운지가 열립니다.' },
    ],
  },
  {
    key: 'dinner',
    label: '갈라 디너',
    items: [
      { time: '8:00 PM', title: '개회 & 환영사', desc: '호스트의 환영 인사로 갈라의 밤이 시작됩니다.' },
      { time: '8:20 PM', title: '미쉐린 5코스 디너', desc: '총괄 셰프가 준비한 시즌 특선 코스가 서빙됩니다.' },
      { time: '9:30 PM', title: '라이브 오케스트라', desc: '현악 앙상블의 라이브 공연이 함께합니다.' },
    ],
  },
  {
    key: 'countdown',
    label: '카운트다운',
    items: [
      { time: '11:30 PM', title: '어워드 세리머니', desc: '올해의 VIP 멤버를 위한 감사의 시간을 갖습니다.' },
      { time: '11:55 PM', title: '뉴이어 카운트다운', desc: '샴페인 타워와 함께 2027년을 맞이합니다.' },
      { time: '12:10 AM', title: '애프터 라운지', desc: '기프트 증정과 함께 자유로운 네트워킹이 이어집니다.' },
    ],
  },
]

const faqs = [
  { q: '초청장 없이 입장할 수 있나요?', a: '본 행사는 초청 전용 행사로, 사전 RSVP를 완료하신 분께만 입장이 가능합니다. 입장 시 성함으로 명단을 확인합니다.' },
  { q: '동반 인원은 몇 명까지 가능한가요?', a: '1인까지 동반이 가능하며, RSVP 등록 시 동반 여부를 반드시 선택해 주셔야 합니다.' },
  { q: '주차는 어떻게 하나요?', a: '전 참석자에게 무료 발렛 파킹이 제공됩니다. 정문 발렛 데스크에서 초청 안내를 제시해 주세요.' },
  { q: '드레스코드를 꼭 지켜야 하나요?', a: 'Black Tie 드레스코드를 권장드립니다. 행사의 격식을 위해 정장 착용을 부탁드립니다.' },
]

const targets = { guests: 200, programs: 8, years: 12, hours: 5 }
const display = ref({ guests: 0, programs: 0, years: 0, hours: 0 })

onMounted(() => {
  const el = document.querySelector('.numbers')
  if (!el) return

  const run = () => {
    const steps = 40
    let frame = 0
    const timer = setInterval(() => {
      frame++
      const p = Math.min(frame / steps, 1)
      display.value = {
        guests: Math.round(targets.guests * p),
        programs: Math.round(targets.programs * p),
        years: Math.round(targets.years * p),
        hours: Math.round(targets.hours * p),
      }
      if (p >= 1) clearInterval(timer)
    }, 25)
  }

  const io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (e.isIntersecting) {
        run()
        io.disconnect()
      }
    })
  }, { threshold: 0.4 })
  io.observe(el)
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700;900&family=Montserrat:wght@300;400;600&display=swap');

.app-wrap {
  background: #050505;
  min-height: 100vh;
  font-family: 'Montserrat', sans-serif;
  color: #d4af37;
}

/* ===== HERO ===== */
.hero {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 4rem 2rem;
  min-height: 100vh;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
}

.hero-bg img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.35;
}

.hero-scrim {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center, rgba(5,5,5,0.55) 0%, #050505 78%);
}

.luxury-card {
  position: relative;
  z-index: 1;
  max-width: 450px;
  width: 100%;
  background: rgba(10,10,10,0.85);
  padding: 1.5rem;
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
  background: rgba(5,5,5,0.9);
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
  background-clip: text;
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
  margin-bottom: 3rem;
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
  margin-bottom: 3rem;
}

.row {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid rgba(212,175,55,0.3);
  padding: 1.2rem 0;
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
  display: block;
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
  text-align: center;
  text-decoration: none;
}

.rsvp:hover {
  background: #fff;
}

/* ===== METRICS ===== */
.metrics {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  background: rgba(212,175,55,0.25);
  border-top: 1px solid rgba(212,175,55,0.25);
  border-bottom: 1px solid rgba(212,175,55,0.25);
}

.metric {
  background: #050505;
  text-align: center;
  padding: 2.5rem 1rem;
}

.metric strong {
  display: block;
  font-family: 'Cinzel', serif;
  font-size: 2.6rem;
  font-weight: 700;
  color: #fcf6ba;
}

.metric span {
  font-size: 0.7rem;
  letter-spacing: 2px;
  color: #8c7322;
}

/* ===== SHARED ===== */
.eyebrow {
  font-size: 0.65rem;
  letter-spacing: 5px;
  color: #8c7322;
  margin-bottom: 1.2rem;
}

.eyebrow.center,
h2.center {
  text-align: center;
}

section h2 {
  font-family: 'Cinzel', serif;
  font-size: 2rem;
  line-height: 1.3;
  font-weight: 400;
  color: #e8d9a0;
  margin-bottom: 1.5rem;
}

/* ===== OVERVIEW ===== */
.overview {
  max-width: 900px;
  margin: 0 auto;
  padding: 6rem 2rem;
}

.lede {
  font-family: 'Montserrat', sans-serif;
  font-size: 0.95rem;
  line-height: 2;
  color: #b8a97a;
  max-width: 640px;
  margin-bottom: 3.5rem;
}

.ov-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1px;
  background: rgba(212,175,55,0.2);
  border: 1px solid rgba(212,175,55,0.2);
}

.ov-item {
  background: #050505;
  padding: 2rem;
}

.ov-label {
  font-size: 0.7rem;
  letter-spacing: 3px;
  color: #8c7322;
}

.ov-val {
  font-family: 'Cinzel', serif;
  font-size: 1.15rem;
  color: #e8d9a0;
  margin: 0.7rem 0 0.4rem;
}

.ov-sub {
  font-size: 0.8rem;
  color: #7a6d4a;
  line-height: 1.6;
}

/* ===== PROGRAM ===== */
.program {
  max-width: 780px;
  margin: 0 auto;
  padding: 5rem 2rem;
}

.tabs {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin: 2.5rem 0 3rem;
  flex-wrap: wrap;
}

.tab {
  background: transparent;
  border: 1px solid rgba(212,175,55,0.35);
  color: #8c7322;
  padding: 0.7rem 1.6rem;
  font-family: 'Montserrat', sans-serif;
  font-size: 0.75rem;
  letter-spacing: 2px;
  cursor: pointer;
  transition: all 0.3s;
}

.tab.active {
  background: #d4af37;
  color: #050505;
  border-color: #d4af37;
}

.timeline {
  border-left: 1px solid rgba(212,175,55,0.3);
  padding-left: 2rem;
}

.tl-row {
  display: flex;
  gap: 1.5rem;
  padding: 1.4rem 0;
  border-bottom: 1px solid rgba(212,175,55,0.12);
  position: relative;
}

.tl-row::before {
  content: '';
  position: absolute;
  left: calc(-2rem - 4px);
  top: 1.9rem;
  width: 7px;
  height: 7px;
  background: #d4af37;
  border-radius: 50%;
}

.tl-time {
  font-family: 'Cinzel', serif;
  font-size: 0.9rem;
  color: #fcf6ba;
  min-width: 80px;
  padding-top: 0.1rem;
}

.tl-body strong {
  display: block;
  color: #e8d9a0;
  font-size: 1rem;
  margin-bottom: 0.4rem;
}

.tl-body p {
  font-size: 0.85rem;
  color: #8c7322;
  line-height: 1.6;
}

/* ===== PERKS ===== */
.perks {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 4rem;
  max-width: 1100px;
  margin: 0 auto;
  padding: 6rem 2rem;
}

.perks-copy ul {
  list-style: none;
  margin-top: 2rem;
}

.perks-copy li {
  border-top: 1px solid rgba(212,175,55,0.25);
  padding: 1.4rem 0;
}

.perks-copy li strong {
  display: block;
  color: #e8d9a0;
  font-size: 1.05rem;
  margin-bottom: 0.4rem;
}

.perks-copy li span {
  font-size: 0.85rem;
  color: #8c7322;
  line-height: 1.6;
}

.perks-img img {
  width: 100%;
  height: 100%;
  max-height: 520px;
  object-fit: cover;
  border: 1px solid rgba(212,175,55,0.3);
}

/* ===== ACCESS ===== */
.access {
  max-width: 1000px;
  margin: 0 auto;
  padding: 5rem 2rem;
  text-align: center;
}

.access-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background: rgba(212,175,55,0.2);
  border: 1px solid rgba(212,175,55,0.2);
  margin-top: 2.5rem;
  text-align: left;
}

.ac-item {
  background: #050505;
  padding: 2rem;
}

.ac-tag {
  display: inline-block;
  font-size: 0.7rem;
  letter-spacing: 2px;
  color: #050505;
  background: #d4af37;
  padding: 0.3rem 0.8rem;
  margin-bottom: 1rem;
}

.ac-item p {
  font-size: 0.9rem;
  color: #b8a97a;
  line-height: 1.8;
}

/* ===== RSVP SECTION ===== */
.rsvp-section {
  padding: 6rem 2rem;
  display: flex;
  justify-content: center;
}

.rsvp-frame {
  max-width: 520px;
  width: 100%;
  border: 1px solid #d4af37;
  padding: 3.5rem 2.5rem;
  background: rgba(10,10,10,0.6);
}

.rsvp-note {
  text-align: center;
  font-size: 0.8rem;
  color: #8c7322;
  margin-bottom: 2.5rem;
}

.rsvp-form {
  display: flex;
  flex-direction: column;
  gap: 1.3rem;
}

.rsvp-form label {
  display: flex;
  flex-direction: column;
  font-size: 0.7rem;
  letter-spacing: 2px;
  color: #8c7322;
  gap: 0.6rem;
}

.rsvp-form input,
.rsvp-form select {
  background: #050505;
  border: 1px solid rgba(212,175,55,0.35);
  color: #e8d9a0;
  padding: 0.9rem 1rem;
  font-family: 'Montserrat', sans-serif;
  font-size: 0.9rem;
  letter-spacing: normal;
}

.rsvp-form input:focus,
.rsvp-form select:focus {
  outline: none;
  border-color: #d4af37;
}

.rsvp-form input::placeholder {
  color: #55492c;
}

.attend {
  border: none;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.fs-label {
  font-size: 0.7rem;
  letter-spacing: 2px;
  color: #8c7322;
}

.opts {
  display: flex;
  gap: 1rem;
}

.opt {
  flex: 1;
  flex-direction: row !important;
  align-items: center;
  gap: 0.5rem !important;
  border: 1px solid rgba(212,175,55,0.35);
  padding: 0.8rem 1rem;
  cursor: pointer;
  letter-spacing: normal !important;
  color: #b8a97a !important;
}

.opt span {
  font-size: 0.85rem;
}

.opt input {
  accent-color: #d4af37;
}

.submit {
  margin-top: 0.5rem;
}

.rsvp-done {
  text-align: center;
  padding: 1rem 0;
}

.done-mark {
  width: 64px;
  height: 64px;
  line-height: 64px;
  margin: 0 auto 1.5rem;
  border: 1px solid #d4af37;
  border-radius: 50%;
  color: #d4af37;
  font-size: 1.6rem;
}

.rsvp-done h3 {
  font-family: 'Cinzel', serif;
  font-size: 1.4rem;
  color: #e8d9a0;
  font-weight: 400;
  margin-bottom: 1rem;
}

.rsvp-done p {
  font-size: 0.85rem;
  color: #8c7322;
  line-height: 1.8;
  margin-bottom: 2rem;
}

.rsvp.ghost {
  background: transparent;
  color: #d4af37;
  border: 1px solid #d4af37;
  width: auto;
  padding: 0.9rem 2rem;
  margin: 0 auto;
}

.rsvp.ghost:hover {
  background: #d4af37;
  color: #050505;
}

/* ===== FAQ ===== */
.faq {
  max-width: 760px;
  margin: 0 auto;
  padding: 5rem 2rem 6rem;
  text-align: center;
}

.faq-list {
  margin-top: 2.5rem;
  text-align: left;
}

.faq-item {
  border-bottom: 1px solid rgba(212,175,55,0.25);
}

.faq-q {
  width: 100%;
  background: transparent;
  border: none;
  color: #e8d9a0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.4rem 0;
  font-family: 'Montserrat', sans-serif;
  font-size: 0.95rem;
  cursor: pointer;
  text-align: left;
}

.faq-icon {
  color: #d4af37;
  font-size: 1.3rem;
  margin-left: 1rem;
}

.faq-a {
  font-size: 0.88rem;
  color: #8c7322;
  line-height: 1.8;
  padding: 0 0 1.4rem;
}

.contact {
  margin-top: 3.5rem;
  border: 1px solid rgba(212,175,55,0.3);
  padding: 2.5rem;
}

.contact p {
  font-size: 0.85rem;
  color: #8c7322;
  margin-bottom: 0.8rem;
}

.contact a {
  display: block;
  font-family: 'Cinzel', serif;
  font-size: 1.6rem;
  color: #fcf6ba;
  text-decoration: none;
  margin-bottom: 0.6rem;
}

.contact span {
  font-size: 0.78rem;
  color: #7a6d4a;
}

/* ===== FOOT ===== */
.foot {
  text-align: center;
  padding: 3rem 2rem;
  border-top: 1px solid rgba(212,175,55,0.2);
}

.foot p {
  font-family: 'Cinzel', serif;
  font-size: 1.1rem;
  letter-spacing: 4px;
  color: #d4af37;
  margin-bottom: 0.6rem;
}

.foot span {
  font-size: 0.72rem;
  color: #55492c;
  letter-spacing: 1px;
}

/* ===== RESPONSIVE ===== */
@media (max-width: 820px) {
  .perks {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }
  .perks-img {
    order: -1;
  }
  .access-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 640px) {
  h1 {
    font-size: 3rem;
  }
  .metrics {
    grid-template-columns: repeat(2, 1fr);
  }
  .metric strong {
    font-size: 2rem;
  }
  .ov-grid {
    grid-template-columns: 1fr;
  }
  section h2 {
    font-size: 1.6rem;
  }
  .gold-frame {
    padding: 3rem 1.3rem;
  }
  .opts {
    flex-direction: column;
  }
  .perks, .overview, .program, .access, .faq {
    padding-left: 1.3rem;
    padding-right: 1.3rem;
  }
}
</style>
