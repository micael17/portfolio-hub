<template>
  <div class="app-wrap">
    <!-- Top bar -->
    <header class="topbar">
      <div class="inner">
        <div class="logo">TECHCON<span>26</span></div>
        <nav class="topnav">
          <a href="#overview">개요</a>
          <a href="#program">프로그램</a>
          <a href="#speakers">연사</a>
          <a href="#tickets">등록</a>
          <a href="#venue">오시는 길</a>
        </nav>
        <a href="#register" class="topcta">등록하기</a>
      </div>
    </header>

    <!-- Hero -->
    <section class="hero">
      <div class="hero-media">
        <!-- AI-IMG: 대형 IT 컨퍼런스 무대와 조명, 청중석, 네이비 톤·프로페셔널 · 16:9 -->
        <!-- prompt: large tech conference main stage with dramatic lighting and audience, deep navy tones, professional, 16:9 -->
        <img
          src="https://images.unsplash.com/photo-1540575467063-178a50c2df87?auto=format&fit=crop&w=1600&q=80"
          alt="조명이 켜진 대형 컨퍼런스 무대와 청중석 전경"
        >
      </div>
      <div class="hero-content">
        <div class="badge">2026 ENTERPRISE AI SUMMIT</div>
        <h1>기업의 미래를 여는<br>엔터프라이즈 AI 서밋</h1>
        <p class="subtitle">
          생성형 AI가 바꾸는 엔터프라이즈 아키텍처, 보안, 그리고 운영 확장 전략을
          국내외 리더들과 함께 논의합니다.
        </p>
        <div class="hero-facts">
          <div class="fact">
            <span class="k">일시</span>
            <span class="v">2026. 10. 24 – 25 (금·토)</span>
          </div>
          <div class="fact">
            <span class="k">장소</span>
            <span class="v">코엑스 그랜드볼룸, 서울</span>
          </div>
          <div class="fact">
            <span class="k">규모</span>
            <span class="v">1,200석 · 40+ 세션</span>
          </div>
        </div>
        <div class="hero-actions">
          <a href="#register" class="btn-primary">지금 등록하기</a>
          <a href="#program" class="btn-ghost">프로그램 보기</a>
        </div>
      </div>
    </section>

    <!-- Overview -->
    <section id="overview" class="section">
      <div class="section-head">
        <span class="eyebrow">OVERVIEW</span>
        <h2>행사 개요</h2>
      </div>
      <div class="overview-grid">
        <div class="ov-card">
          <div class="ov-num">01</div>
          <h3>주제</h3>
          <p>엔터프라이즈 환경에서의 생성형 AI 도입, 거버넌스, 보안, 비용 최적화를 다루는 실무 중심 세미나.</p>
        </div>
        <div class="ov-card">
          <div class="ov-num">02</div>
          <h3>대상</h3>
          <p>CTO·아키텍트·데이터/플랫폼 리더 및 AI 도입을 준비하는 실무 엔지니어.</p>
        </div>
        <div class="ov-card">
          <div class="ov-num">03</div>
          <h3>구성</h3>
          <p>기조연설, 트랙별 기술 세션, 라이브 데모, 네트워킹 리셉션으로 이틀간 진행.</p>
        </div>
        <div class="ov-card">
          <div class="ov-num">04</div>
          <h3>규모</h3>
          <p>연사 24명, 파트너 18개사, 참가자 1,200명 규모의 국내 최대 엔터프라이즈 AI 컨퍼런스.</p>
        </div>
      </div>
    </section>

    <!-- Program -->
    <section id="program" class="section alt">
      <div class="section-head">
        <span class="eyebrow">PROGRAM</span>
        <h2>프로그램 타임테이블</h2>
        <p class="section-desc">이틀간 진행되는 세션을 Day별로 확인하세요.</p>
      </div>

      <div class="tabs" role="tablist" aria-label="프로그램 일자">
        <button
          v-for="(day, i) in program"
          :key="day.id"
          class="tab"
          :class="{ active: tab === i }"
          role="tab"
          :aria-selected="tab === i"
          @click="tab = i"
        >
          {{ day.label }}
          <span class="tab-date">{{ day.date }}</span>
        </button>
      </div>

      <div class="timetable" role="tabpanel">
        <div v-for="(s, i) in program[tab].sessions" :key="i" class="tt-row">
          <div class="tt-time">{{ s.time }}</div>
          <div class="tt-body">
            <div class="tt-track" :class="s.trackClass">{{ s.track }}</div>
            <h4>{{ s.title }}</h4>
            <p class="tt-speaker">{{ s.speaker }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Speakers -->
    <section id="speakers" class="section">
      <div class="section-head">
        <span class="eyebrow">SPEAKERS</span>
        <h2>연사 소개</h2>
        <p class="section-desc">현장의 최전선에서 AI 전환을 이끄는 리더들이 함께합니다.</p>
      </div>
      <div class="speakers-grid">
        <article v-for="sp in speakers" :key="sp.name" class="sp-card">
          <div class="sp-photo">
            <!-- AI-IMG: 연사 프로필 사진 · 각 연사 생성 프롬프트는 speakers 배열의 item.imgPrompt/imgNote 필드 참조 -->
            <img :src="sp.img" :alt="sp.alt">
          </div>
          <div class="sp-info">
            <h3>{{ sp.name }}</h3>
            <p class="sp-title">{{ sp.title }}</p>
            <p class="sp-org">{{ sp.org }}</p>
            <p class="sp-bio">{{ sp.bio }}</p>
          </div>
        </article>
      </div>
    </section>

    <!-- Benefits -->
    <section class="section alt">
      <div class="section-head">
        <span class="eyebrow">BENEFITS</span>
        <h2>참가 혜택</h2>
      </div>
      <div class="benefits-grid">
        <div v-for="b in benefits" :key="b.title" class="bf-card">
          <div class="bf-icon" aria-hidden="true">{{ b.icon }}</div>
          <h3>{{ b.title }}</h3>
          <p>{{ b.desc }}</p>
        </div>
      </div>
    </section>

    <!-- Tickets -->
    <section id="tickets" class="section">
      <div class="section-head">
        <span class="eyebrow">TICKETS</span>
        <h2>등록 · 티켓 안내</h2>
        <p class="section-desc">얼리버드는 9월 30일까지 한정 판매됩니다.</p>
      </div>
      <div class="tickets-grid">
        <div
          v-for="t in tickets"
          :key="t.name"
          class="tk-card"
          :class="{ featured: t.featured }"
        >
          <div v-if="t.featured" class="tk-flag">추천</div>
          <h3>{{ t.name }}</h3>
          <div class="tk-price">
            <span class="won">₩</span>{{ t.price }}
          </div>
          <p class="tk-note">{{ t.note }}</p>
          <ul class="tk-feats">
            <li v-for="f in t.features" :key="f">{{ f }}</li>
          </ul>
          <button type="button" class="tk-btn" :class="{ solid: t.featured }" @click="selectTicket(t.name)">선택하기</button>
        </div>
      </div>
    </section>

    <!-- Venue -->
    <section id="venue" class="section alt">
      <div class="section-head">
        <span class="eyebrow">VENUE</span>
        <h2>오시는 길</h2>
      </div>
      <div class="venue-grid">
        <div class="venue-media">
          <!-- AI-IMG: 대형 컨벤션 센터 외관, 유리 파사드, 네이비 하늘 톤·프로페셔널 · 4:3 -->
          <!-- prompt: modern convention center exterior with glass facade at dusk, navy sky, professional, 4:3 -->
          <img
            src="https://images.unsplash.com/photo-1519671482749-fd09be7ccebf?auto=format&fit=crop&w=1200&q=80"
            alt="유리 파사드가 있는 현대적인 컨벤션 센터 외관"
          >
        </div>
        <div class="venue-info">
          <div class="vrow">
            <span class="vk">장소</span>
            <span class="vv">코엑스 그랜드볼룸 (지하 1층)</span>
          </div>
          <div class="vrow">
            <span class="vk">주소</span>
            <span class="vv">서울특별시 강남구 영동대로 513</span>
          </div>
          <div class="vrow">
            <span class="vk">지하철</span>
            <span class="vv">2호선 삼성역 5·6번 출구, 도보 5분</span>
          </div>
          <div class="vrow">
            <span class="vk">주차</span>
            <span class="vv">코엑스 지하주차장 이용 (등록자 4시간 무료)</span>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ -->
    <section class="section">
      <div class="section-head">
        <span class="eyebrow">FAQ</span>
        <h2>자주 묻는 질문</h2>
      </div>
      <div class="faq-list">
        <div v-for="(f, i) in faqs" :key="i" class="faq-item">
          <button
            class="faq-q"
            :aria-expanded="openFaq === i"
            @click="openFaq = openFaq === i ? -1 : i"
          >
            <span>{{ f.q }}</span>
            <span class="faq-mark" aria-hidden="true">{{ openFaq === i ? '−' : '+' }}</span>
          </button>
          <div v-show="openFaq === i" class="faq-a">
            <p>{{ f.a }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Register -->
    <section id="register" class="section register-sec">
      <div class="section-head">
        <span class="eyebrow light">REGISTER</span>
        <h2>지금 등록하세요</h2>
        <p class="section-desc light">아래 정보를 입력하시면 담당자가 등록 확인 메일을 보내드립니다.</p>
      </div>

      <form class="reg-form" @submit.prevent="submit">
        <div class="field">
          <label for="name">성함 <span>*</span></label>
          <input id="name" v-model.trim="form.name" type="text" placeholder="홍길동" autocomplete="name">
          <p v-if="errors.name" class="err">{{ errors.name }}</p>
        </div>
        <div class="field">
          <label for="email">이메일 <span>*</span></label>
          <input id="email" v-model.trim="form.email" type="email" placeholder="you@company.com" autocomplete="email">
          <p v-if="errors.email" class="err">{{ errors.email }}</p>
        </div>
        <div class="field">
          <label for="org">소속 <span>*</span></label>
          <input id="org" v-model.trim="form.org" type="text" placeholder="회사 / 부서" autocomplete="organization">
          <p v-if="errors.org" class="err">{{ errors.org }}</p>
        </div>
        <div class="field">
          <label for="ticket">티켓 유형 <span>*</span></label>
          <select id="ticket" v-model="form.ticket">
            <option v-for="t in tickets" :key="t.name" :value="t.name">{{ t.name }}</option>
          </select>
        </div>
        <button type="submit" class="reg-submit" :disabled="submitted">
          {{ submitted ? '등록 신청 완료' : '등록 신청하기' }}
        </button>
        <p v-if="submitted" class="reg-done" role="status">
          {{ form.name }}님, 등록 신청이 접수되었습니다. 확인 메일을 확인해 주세요.
        </p>
      </form>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="ft-inner">
        <div class="logo">TECHCON<span>26</span></div>
        <p class="ft-copy">엔터프라이즈 AI 서밋 · 2026. 10. 24 – 25 · 코엑스 그랜드볼룸</p>
        <p class="ft-sub">주최 TECHCON Organizing Committee · 문의 event@techcon26.example</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
useHead({ title: 'TECHCON 26 — 엔터프라이즈 AI 서밋' })
definePageMeta({ layout: false })

const tab = ref(0)
const openFaq = ref(-1)
const submitted = ref(false)

const program = [
  {
    id: 'day1',
    label: 'Day 1',
    date: '10. 24 (금)',
    sessions: [
      { time: '09:30', track: 'KEYNOTE', trackClass: 'tk-keynote', title: '개회사 및 오프닝 기조연설: 엔터프라이즈 AI의 현재와 다음', speaker: '김도현 · TECHCON 조직위원장' },
      { time: '10:30', track: 'TRACK A', trackClass: 'tk-a', title: 'LLM 기반 사내 지식 검색 플랫폼 구축 사례', speaker: '박서연 · 하나테크 AI플랫폼실장' },
      { time: '11:30', track: 'TRACK B', trackClass: 'tk-b', title: '프로덕션 환경의 AI 보안·거버넌스 프레임워크', speaker: '이준호 · 시큐어랩스 CISO' },
      { time: '13:30', track: 'TRACK A', trackClass: 'tk-a', title: 'RAG 파이프라인 비용 최적화 실전', speaker: '최민아 · 클라우드나인 수석엔지니어' },
      { time: '15:00', track: 'DEMO', trackClass: 'tk-demo', title: '라이브 데모: 멀티에이전트 워크플로 자동화', speaker: '데모 스테이지' },
      { time: '17:00', track: 'NETWORK', trackClass: 'tk-net', title: '네트워킹 리셉션', speaker: '그랜드볼룸 로비' },
    ],
  },
  {
    id: 'day2',
    label: 'Day 2',
    date: '10. 25 (토)',
    sessions: [
      { time: '10:00', track: 'KEYNOTE', trackClass: 'tk-keynote', title: '기조연설: AI 조직 운영과 인재 전략', speaker: '정하늘 · 넥스트데이터 CTO' },
      { time: '11:00', track: 'TRACK A', trackClass: 'tk-a', title: '벡터 데이터베이스 아키텍처 심화', speaker: '박서연 · 하나테크 AI플랫폼실장' },
      { time: '13:30', track: 'TRACK B', trackClass: 'tk-b', title: 'AI 규제 대응과 컴플라이언스 로드맵', speaker: '이준호 · 시큐어랩스 CISO' },
      { time: '15:00', track: 'PANEL', trackClass: 'tk-panel', title: '패널 토크: 엔터프라이즈 AI, 무엇을 먼저 할 것인가', speaker: '연사 전원' },
      { time: '16:30', track: 'CLOSING', trackClass: 'tk-keynote', title: '폐회사 및 우수 사례 시상', speaker: '김도현 · TECHCON 조직위원장' },
    ],
  },
]

const speakers = [
  {
    name: '김도현',
    title: 'TECHCON 조직위원장',
    org: '전 대한AI학회 회장',
    bio: '20년간 엔터프라이즈 소프트웨어와 AI 도입 전략을 이끌어온 국내 대표 기술 리더입니다.',
    img: 'https://images.unsplash.com/photo-1519085360753-af0119f7cbe7?auto=format&fit=crop&w=600&q=80',
    alt: '정장 차림으로 미소 짓는 남성 연사 프로필 사진',
    imgNote: '남성 연사 프로필, 정장·프로페셔널 · 1:1',
    imgPrompt: 'professional headshot of an asian businessman in a suit, neutral background, corporate, 1:1',
  },
  {
    name: '박서연',
    title: 'AI플랫폼실장',
    org: '하나테크',
    bio: '사내 LLM 지식 플랫폼과 RAG 시스템을 설계·운영하며 대규모 검색 인프라를 담당하고 있습니다.',
    img: 'https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?auto=format&fit=crop&w=600&q=80',
    alt: '단정한 정장 차림의 여성 연사 프로필 사진',
    imgNote: '여성 연사 프로필, 정장·프로페셔널 · 1:1',
    imgPrompt: 'professional headshot of an asian businesswoman in business attire, neutral background, corporate, 1:1',
  },
  {
    name: '이준호',
    title: 'CISO',
    org: '시큐어랩스',
    bio: 'AI 보안·거버넌스 프레임워크 전문가로 금융·공공 분야 컴플라이언스 프로젝트를 다수 수행했습니다.',
    img: 'https://images.unsplash.com/photo-1560250097-0b93528c311a?auto=format&fit=crop&w=600&q=80',
    alt: '안경을 쓴 정장 차림 남성 연사 프로필 사진',
    imgNote: '안경 쓴 남성 연사 프로필, 정장·프로페셔널 · 1:1',
    imgPrompt: 'professional headshot of a man with glasses in a suit, neutral background, corporate, 1:1',
  },
  {
    name: '정하늘',
    title: 'CTO',
    org: '넥스트데이터',
    bio: 'AI 조직 운영과 인재 전략을 담당하며, 데이터 기반 프로덕트 조직을 성공적으로 확장한 경험을 공유합니다.',
    img: 'https://images.unsplash.com/photo-1580489944761-15a19d654956?auto=format&fit=crop&w=600&q=80',
    alt: '밝게 웃는 여성 연사 프로필 사진',
    imgNote: '여성 연사 프로필, 밝은 표정·프로페셔널 · 1:1',
    imgPrompt: 'professional headshot of a smiling asian businesswoman, neutral background, corporate, 1:1',
  },
]

const benefits = [
  { icon: '🎟', title: '전 세션 참관', desc: '이틀간 진행되는 40개 이상 세션과 라이브 데모에 자유롭게 참여할 수 있습니다.' },
  { icon: '📎', title: '발표 자료 제공', desc: '행사 종료 후 모든 세션의 발표 자료와 다시보기 영상을 이메일로 받아보실 수 있습니다.' },
  { icon: '🤝', title: '네트워킹 리셉션', desc: '연사·파트너사·참가자와 교류할 수 있는 저녁 네트워킹 세션에 초대됩니다.' },
  { icon: '🎁', title: '참가자 웰컴 키트', desc: '공식 굿즈와 파트너사 크레딧이 포함된 웰컴 키트를 현장에서 제공합니다.' },
]

const tickets = [
  {
    name: '얼리버드',
    price: '99,000',
    note: '9월 30일까지 한정',
    features: ['전 세션 참관', '발표 자료 제공', '웰컴 키트'],
    featured: false,
  },
  {
    name: '일반',
    price: '149,000',
    note: '10월 1일부터',
    features: ['전 세션 참관', '발표 자료 제공', '웰컴 키트', '네트워킹 리셉션'],
    featured: true,
  },
  {
    name: 'VIP',
    price: '299,000',
    note: '한정 100석',
    features: ['전 세션 참관', '앞줄 지정석', '연사 라운지 입장', 'VIP 디너 초대', '1:1 상담 세션'],
    featured: false,
  },
]

const faqs = [
  { q: '현장 등록도 가능한가요?', a: '사전 등록을 원칙으로 하며, 잔여석이 있을 경우에 한해 현장 등록이 가능합니다. 조기 매진이 예상되므로 사전 등록을 권장합니다.' },
  { q: '발표 자료와 다시보기는 제공되나요?', a: '네. 행사 종료 후 등록하신 이메일로 세션 발표 자료와 다시보기 영상 링크를 발송해 드립니다.' },
  { q: '등록을 취소하면 환불되나요?', a: '행사 7일 전까지 100% 환불되며, 이후에는 50% 환불됩니다. 행사 2일 전부터는 환불이 불가합니다.' },
  { q: '단체 등록 할인이 있나요?', a: '5인 이상 단체 등록 시 10% 할인이 적용됩니다. event@techcon26.example 로 문의해 주세요.' },
  { q: '주차 지원이 되나요?', a: '등록자에 한해 코엑스 지하주차장 4시간 무료 주차를 지원합니다. 현장 등록 데스크에서 확인받으시면 됩니다.' },
]

const form = reactive({
  name: '',
  email: '',
  org: '',
  ticket: tickets[0].name,
})

const errors = reactive({
  name: '',
  email: '',
  org: '',
})

function selectTicket(name) {
  form.ticket = name
  if (typeof document !== 'undefined') {
    document.getElementById('register')?.scrollIntoView({ behavior: 'smooth' })
  }
}

function submit() {
  errors.name = form.name ? '' : '성함을 입력해 주세요.'
  errors.email = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email) ? '' : '올바른 이메일을 입력해 주세요.'
  errors.org = form.org ? '' : '소속을 입력해 주세요.'

  if (errors.name || errors.email || errors.org) {
    submitted.value = false
    return
  }
  submitted.value = true
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600;700&display=swap');

.app-wrap {
  background: #f0f4f8;
  color: #0f172a;
  font-family: 'IBM Plex Sans', sans-serif;
  min-height: 100vh;
  line-height: 1.6;
}

/* Topbar */
.topbar {
  position: sticky;
  top: 0;
  z-index: 20;
  background: rgba(15, 23, 42, 0.96);
  border-bottom: 1px solid #1e293b;
}
.topbar .inner {
  max-width: 1120px;
  margin: 0 auto;
  padding: 0.9rem 1.5rem;
  display: flex;
  align-items: center;
  gap: 1.5rem;
}
.logo {
  font-weight: 700;
  font-size: 1.15rem;
  letter-spacing: 1px;
  color: #fff;
}
.logo span { color: #60a5fa; }
.topnav {
  display: flex;
  gap: 1.4rem;
  margin-left: auto;
}
.topnav a {
  color: #cbd5e1;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  transition: color 0.15s;
}
.topnav a:hover { color: #fff; }
.topcta {
  background: #2563eb;
  color: #fff;
  text-decoration: none;
  font-size: 0.85rem;
  font-weight: 600;
  padding: 0.55rem 1rem;
  letter-spacing: 0.5px;
  transition: background 0.15s;
}
.topcta:hover { background: #1d4ed8; }

/* Hero */
.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  background: #0f172a;
  color: #fff;
}
.hero-media { position: relative; min-height: 420px; }
.hero-media img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.55;
}
.hero-content {
  padding: 4rem 3rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.badge {
  display: inline-block;
  align-self: flex-start;
  background: #2563eb;
  color: #fff;
  font-size: 0.7rem;
  font-weight: 600;
  padding: 0.35rem 0.7rem;
  letter-spacing: 1.5px;
  margin-bottom: 1.4rem;
}
.hero-content h1 {
  font-size: 2.6rem;
  line-height: 1.2;
  margin-bottom: 1.1rem;
}
.subtitle {
  color: #94a3b8;
  font-size: 1.05rem;
  margin-bottom: 2rem;
  max-width: 30rem;
}
.hero-facts {
  display: flex;
  flex-direction: column;
  gap: 0;
  border: 1px solid #1e293b;
  margin-bottom: 2rem;
}
.fact {
  display: flex;
  border-bottom: 1px solid #1e293b;
}
.fact:last-child { border-bottom: none; }
.fact .k {
  flex: 0 0 88px;
  background: #1e293b;
  color: #94a3b8;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 1px;
  padding: 0.75rem 1rem;
}
.fact .v {
  flex: 1;
  padding: 0.75rem 1rem;
  font-weight: 600;
}
.hero-actions { display: flex; gap: 0.8rem; flex-wrap: wrap; }
.btn-primary {
  background: #2563eb;
  color: #fff;
  text-decoration: none;
  font-weight: 700;
  padding: 0.9rem 1.6rem;
  transition: background 0.15s;
}
.btn-primary:hover { background: #1d4ed8; }
.btn-ghost {
  border: 1px solid #475569;
  color: #e2e8f0;
  text-decoration: none;
  font-weight: 600;
  padding: 0.9rem 1.6rem;
  transition: border-color 0.15s, color 0.15s;
}
.btn-ghost:hover { border-color: #94a3b8; color: #fff; }

/* Sections */
.section {
  max-width: 1120px;
  margin: 0 auto;
  padding: 4.5rem 1.5rem;
}
.section.alt {
  max-width: none;
  background: #fff;
  border-top: 1px solid #e2e8f0;
  border-bottom: 1px solid #e2e8f0;
}
.section.alt > * {
  max-width: 1120px;
  margin-left: auto;
  margin-right: auto;
}
.section-head { margin-bottom: 2.5rem; }
.eyebrow {
  display: block;
  color: #2563eb;
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 2px;
  margin-bottom: 0.6rem;
}
.eyebrow.light { color: #60a5fa; }
.section-head h2 {
  font-size: 1.9rem;
  font-weight: 700;
}
.section-desc {
  color: #64748b;
  margin-top: 0.6rem;
  font-size: 1rem;
}
.section-desc.light { color: #cbd5e1; }

/* Overview */
.overview-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  background: #e2e8f0;
  border: 1px solid #e2e8f0;
}
.ov-card { background: #fff; padding: 1.8rem 1.5rem; }
.ov-num {
  font-size: 0.9rem;
  font-weight: 700;
  color: #93c5fd;
  margin-bottom: 0.8rem;
}
.ov-card h3 { font-size: 1.1rem; margin-bottom: 0.5rem; }
.ov-card p { color: #475569; font-size: 0.92rem; }

/* Tabs + Timetable */
.tabs { display: flex; gap: 0.5rem; margin-bottom: 1.8rem; flex-wrap: wrap; }
.tab {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
  background: #fff;
  border: 1px solid #cbd5e1;
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 700;
  color: #64748b;
  cursor: pointer;
  transition: all 0.15s;
}
.tab .tab-date { font-size: 0.75rem; font-weight: 500; }
.tab.active {
  background: #0f172a;
  border-color: #0f172a;
  color: #fff;
}
.timetable { border: 1px solid #e2e8f0; background: #fff; }
.tt-row {
  display: flex;
  gap: 1.5rem;
  padding: 1.3rem 1.5rem;
  border-bottom: 1px solid #e2e8f0;
}
.tt-row:last-child { border-bottom: none; }
.tt-time {
  flex: 0 0 60px;
  font-weight: 700;
  color: #0f172a;
  font-size: 1.05rem;
}
.tt-body { flex: 1; }
.tt-track {
  display: inline-block;
  font-size: 0.68rem;
  font-weight: 700;
  letter-spacing: 1px;
  padding: 0.2rem 0.5rem;
  margin-bottom: 0.5rem;
  color: #fff;
}
.tk-keynote { background: #0f172a; }
.tk-a { background: #2563eb; }
.tk-b { background: #7c3aed; }
.tk-demo { background: #0891b2; }
.tk-net { background: #059669; }
.tk-panel { background: #d97706; }
.tt-body h4 { font-size: 1.02rem; margin-bottom: 0.25rem; }
.tt-speaker { color: #64748b; font-size: 0.9rem; }

/* Speakers */
.speakers-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.2rem;
}
.sp-card {
  background: #fff;
  border: 1px solid #e2e8f0;
  overflow: hidden;
}
.sp-photo { aspect-ratio: 1 / 1; overflow: hidden; background: #e2e8f0; }
.sp-photo img { width: 100%; height: 100%; object-fit: cover; }
.sp-info { padding: 1.2rem; }
.sp-info h3 { font-size: 1.15rem; }
.sp-title { color: #2563eb; font-weight: 600; font-size: 0.9rem; margin-top: 0.2rem; }
.sp-org { color: #64748b; font-size: 0.85rem; margin-bottom: 0.7rem; }
.sp-bio { color: #475569; font-size: 0.88rem; }

/* Benefits */
.benefits-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.2rem;
}
.bf-card {
  background: #f8fafc;
  border: 1px solid #e2e8f0;
  padding: 1.8rem 1.5rem;
}
.bf-icon { font-size: 1.8rem; margin-bottom: 0.8rem; }
.bf-card h3 { font-size: 1.08rem; margin-bottom: 0.5rem; }
.bf-card p { color: #475569; font-size: 0.9rem; }

/* Tickets */
.tickets-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.2rem;
}
.tk-card {
  position: relative;
  background: #fff;
  border: 1px solid #cbd5e1;
  padding: 2rem 1.8rem;
  display: flex;
  flex-direction: column;
}
.tk-card.featured {
  border-color: #2563eb;
  box-shadow: 8px 8px 0 #0f172a;
}
.tk-flag {
  position: absolute;
  top: -1px;
  right: -1px;
  background: #2563eb;
  color: #fff;
  font-size: 0.72rem;
  font-weight: 700;
  padding: 0.3rem 0.8rem;
  letter-spacing: 1px;
}
.tk-card h3 { font-size: 1.2rem; margin-bottom: 0.8rem; }
.tk-price {
  font-size: 2rem;
  font-weight: 700;
  color: #0f172a;
}
.tk-price .won { font-size: 1.1rem; font-weight: 600; margin-right: 0.1rem; }
.tk-note { color: #64748b; font-size: 0.85rem; margin-bottom: 1.2rem; }
.tk-feats {
  list-style: none;
  padding: 0;
  margin: 0 0 1.6rem;
  flex: 1;
}
.tk-feats li {
  padding: 0.5rem 0;
  border-bottom: 1px solid #f1f5f9;
  font-size: 0.9rem;
  color: #334155;
}
.tk-feats li::before { content: '✓ '; color: #2563eb; font-weight: 700; }
.tk-btn {
  width: 100%;
  text-align: center;
  text-decoration: none;
  background: transparent;
  border: 1px solid #0f172a;
  color: #0f172a;
  font-family: inherit;
  font-size: 0.95rem;
  font-weight: 700;
  padding: 0.85rem;
  cursor: pointer;
  transition: all 0.15s;
}
.tk-btn:hover { background: #0f172a; color: #fff; }
.tk-btn.solid { background: #2563eb; border-color: #2563eb; color: #fff; }
.tk-btn.solid:hover { background: #1d4ed8; border-color: #1d4ed8; }

/* Venue */
.venue-grid {
  display: grid;
  grid-template-columns: 1.1fr 1fr;
  gap: 2rem;
  align-items: stretch;
}
.venue-media { border: 1px solid #e2e8f0; overflow: hidden; min-height: 280px; }
.venue-media img { width: 100%; height: 100%; object-fit: cover; }
.venue-info {
  border: 1px solid #e2e8f0;
  background: #fff;
  display: flex;
  flex-direction: column;
}
.vrow {
  display: flex;
  border-bottom: 1px solid #e2e8f0;
  flex: 1;
}
.vrow:last-child { border-bottom: none; }
.vk {
  flex: 0 0 90px;
  background: #f8fafc;
  border-right: 1px solid #e2e8f0;
  padding: 1.1rem;
  font-size: 0.82rem;
  font-weight: 600;
  color: #64748b;
  letter-spacing: 0.5px;
}
.vv { flex: 1; padding: 1.1rem; font-weight: 500; }

/* FAQ */
.faq-list { border: 1px solid #e2e8f0; background: #fff; }
.faq-item { border-bottom: 1px solid #e2e8f0; }
.faq-item:last-child { border-bottom: none; }
.faq-q {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  background: none;
  border: none;
  padding: 1.3rem 1.5rem;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 600;
  color: #0f172a;
  text-align: left;
  cursor: pointer;
}
.faq-mark {
  flex: 0 0 auto;
  font-size: 1.4rem;
  color: #2563eb;
  font-weight: 700;
  line-height: 1;
}
.faq-a {
  padding: 0 1.5rem 1.3rem;
  color: #475569;
  font-size: 0.94rem;
}

/* Register */
.register-sec {
  background: #0f172a;
  color: #fff;
  max-width: none;
}
.register-sec > * {
  max-width: 640px;
  margin-left: auto;
  margin-right: auto;
}
.register-sec .section-head h2 { color: #fff; }
.reg-form { display: flex; flex-direction: column; gap: 1.2rem; }
.field { display: flex; flex-direction: column; gap: 0.4rem; }
.field label { font-size: 0.85rem; font-weight: 600; color: #cbd5e1; }
.field label span { color: #f87171; }
.field input,
.field select {
  background: #1e293b;
  border: 1px solid #334155;
  color: #fff;
  padding: 0.8rem 1rem;
  font-family: inherit;
  font-size: 0.95rem;
}
.field input::placeholder { color: #64748b; }
.field input:focus,
.field select:focus { outline: none; border-color: #2563eb; }
.err { color: #f87171; font-size: 0.82rem; }
.reg-submit {
  background: #2563eb;
  color: #fff;
  border: none;
  padding: 1.1rem;
  font-family: inherit;
  font-size: 1.05rem;
  font-weight: 700;
  cursor: pointer;
  transition: background 0.15s;
  margin-top: 0.5rem;
}
.reg-submit:hover:not(:disabled) { background: #1d4ed8; }
.reg-submit:disabled { background: #059669; cursor: default; }
.reg-done {
  color: #6ee7b7;
  font-size: 0.92rem;
  text-align: center;
}

/* Footer */
.footer {
  background: #020617;
  color: #94a3b8;
  padding: 2.5rem 1.5rem;
  text-align: center;
}
.ft-inner { max-width: 1120px; margin: 0 auto; }
.footer .logo { justify-content: center; margin-bottom: 0.8rem; }
.ft-copy { font-size: 0.9rem; color: #cbd5e1; }
.ft-sub { font-size: 0.82rem; margin-top: 0.4rem; }

/* Responsive */
@media (max-width: 900px) {
  .hero { grid-template-columns: 1fr; }
  .hero-media { min-height: 240px; }
  .hero-content { padding: 2.5rem 1.5rem; }
  .overview-grid,
  .speakers-grid,
  .benefits-grid { grid-template-columns: repeat(2, 1fr); }
  .tickets-grid { grid-template-columns: 1fr; }
  .venue-grid { grid-template-columns: 1fr; }
}
@media (max-width: 640px) {
  .topnav { display: none; }
  .hero-content h1 { font-size: 2rem; }
  .overview-grid,
  .speakers-grid,
  .benefits-grid { grid-template-columns: 1fr; }
  .tt-row { flex-direction: column; gap: 0.6rem; }
  .section-head h2 { font-size: 1.6rem; }
}
</style>
