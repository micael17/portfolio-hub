<template>
  <div class="ex">
    <!-- ============ HERO ============ -->
    <header class="hero">
      <div class="hero-media">
        <!-- AI-IMG: 어두운 화이트큐브 갤러리에 놓인 대형 추상 설치작, 아방가르드·미니멀 · 3:4 -->
        <!-- prompt: contemporary art gallery, dark white cube space, large abstract installation, avant-garde minimal, dramatic light, 3:4 -->
        <img
          src="https://images.unsplash.com/photo-1536924940846-227afb31e2a5?w=900&q=80"
          alt="어두운 전시장 한가운데 놓인 대형 설치 작품 VOID의 전경"
        >
      </div>
      <div class="hero-type">
        <span class="kicker">GALLERY NEU · EXHIBITION 04</span>
        <h1>VOID</h1>
        <p class="sub">비어있음의 형태</p>
        <div class="hero-meta">
          <span>2026.10.24 &mdash; 12.21</span>
          <span>서울 성수동 · 갤러리 노이</span>
        </div>
      </div>
      <p class="vertical-side">THE SHAPE OF EMPTINESS</p>
    </header>

    <!-- ============ 전시 개요 ============ -->
    <section class="overview reveal">
      <div class="ov-label"><span class="idx">01</span><p class="vertical">OVERVIEW</p></div>
      <div class="ov-body">
        <h2>전시 개요</h2>
        <p class="statement">
          &lsquo;VOID&rsquo;는 물질이 사라진 자리에 남는 감각을 좇는다.
          빛과 소리, 그리고 텅 빈 공간 그 자체를 매체로 삼아
          여덟 명의 작가가 &lsquo;비어있음&rsquo;을 조형 언어로 번역한다.
          관람객은 작품을 보는 것이 아니라, 작품이 만들어낸 공백 속을 걷는다.
        </p>
        <dl class="ov-facts">
          <div><dt>전시명</dt><dd>VOID: 비어있음의 형태</dd></div>
          <div><dt>기간</dt><dd>2026. 10. 24 (토) &mdash; 12. 21 (일)</dd></div>
          <div><dt>장소</dt><dd>갤러리 노이 B1, 제1&middot;2전시실</dd></div>
          <div><dt>주최</dt><dd>갤러리 노이 (Gallery Neu)</dd></div>
          <div><dt>큐레이터</dt><dd>서지원 (Jiwon Suh)</dd></div>
          <div><dt>후원</dt><dd>성수문화재단</dd></div>
        </dl>
      </div>
    </section>

    <!-- ============ 작가 / 작품 소개 ============ -->
    <section class="works reveal">
      <div class="works-head">
        <span class="idx">02</span>
        <h2>작가와 작품</h2>
        <div class="filters" role="group" aria-label="작품 매체별 필터">
          <button
            v-for="f in filters"
            :key="f.key"
            class="chip"
            :class="{ on: filter === f.key }"
            :aria-pressed="filter === f.key"
            @click="filter = f.key"
          >{{ f.label }}</button>
        </div>
      </div>

      <div class="grid">
        <article v-for="w in filteredWorks" :key="w.title" class="work">
          <div class="work-img">
            <!-- AI-IMG: 각 작품별 이미지, 아방가르드 현대미술 · 4:5. 개별 프롬프트는 works 배열 item.prompt 참조 -->
            <img :src="w.img" :alt="`${w.artist}의 작품 ${w.title}`">
            <span class="medium-tag">{{ w.mediumLabel }}</span>
          </div>
          <div class="work-info">
            <h3>{{ w.title }}</h3>
            <p class="artist">{{ w.artist }}</p>
            <p class="detail">{{ w.medium }}, {{ w.year }}</p>
          </div>
        </article>
      </div>
      <p v-if="!filteredWorks.length" class="empty">해당 매체의 작품이 없습니다.</p>
    </section>

    <!-- ============ 전시 섹션 / 동선 ============ -->
    <section class="route reveal">
      <div class="ov-label"><span class="idx">03</span><p class="vertical">ROUTE</p></div>
      <div class="route-body">
        <h2>전시 동선</h2>
        <ol class="route-list">
          <li v-for="(r, i) in route" :key="r.name">
            <span class="rnum">{{ String(i + 1).padStart(2, '0') }}</span>
            <div>
              <h4>{{ r.name }}</h4>
              <p>{{ r.desc }}</p>
            </div>
          </li>
        </ol>
      </div>
    </section>

    <!-- ============ 관람 정보 ============ -->
    <section class="visit reveal">
      <span class="idx">04</span>
      <h2>관람 정보</h2>
      <div class="visit-grid">
        <div class="v-card">
          <h4>운영 시간</h4>
          <p>화 &ndash; 일 11:00 &ndash; 19:00</p>
          <p class="muted">매주 월요일 휴관 · 입장 마감 18:30</p>
        </div>
        <div class="v-card">
          <h4>관람 요금</h4>
          <ul class="fee">
            <li><span>성인</span><b>15,000원</b></li>
            <li><span>학생 / 청소년</span><b>10,000원</b></li>
            <li><span>36개월 이하 · 경로</span><b>무료</b></li>
          </ul>
        </div>
        <div class="v-card">
          <h4>예매</h4>
          <p>온라인 사전 예매 시 2,000원 할인.</p>
          <p class="muted">현장 발권은 매표소에서 가능합니다.</p>
        </div>
      </div>
    </section>

    <!-- ============ 프로그램 / 도슨트 ============ -->
    <section class="program reveal">
      <div class="ov-label"><span class="idx">05</span><p class="vertical">PROGRAM</p></div>
      <div class="program-body">
        <h2>프로그램 &amp; 도슨트</h2>
        <ul class="sched">
          <li v-for="p in programs" :key="p.time + p.title">
            <span class="time">{{ p.time }}</span>
            <div>
              <h4>{{ p.title }}</h4>
              <p>{{ p.desc }}</p>
            </div>
          </li>
        </ul>
      </div>
    </section>

    <!-- ============ 예매 / RSVP ============ -->
    <section class="rsvp-sec reveal">
      <div class="rsvp-type">
        <span class="idx">06</span>
        <h2>오프닝<br>리셉션<br>예약</h2>
        <p class="rsvp-note">10.24 (토) 19:00 &ndash; 22:00<br>큐레이터 토크 &amp; 작가와의 만남</p>
      </div>
      <form class="rsvp-form" @submit.prevent="submit">
        <label>
          <span>성함 *</span>
          <input v-model.trim="form.name" type="text" placeholder="예약자 성함" >
        </label>
        <label>
          <span>인원</span>
          <select v-model="form.count">
            <option v-for="n in 5" :key="n" :value="n">{{ n }}명</option>
          </select>
        </label>
        <label>
          <span>관람 희망일</span>
          <input v-model="form.date" type="date" >
        </label>
        <label>
          <span>연락처</span>
          <input v-model.trim="form.phone" type="tel" placeholder="010-0000-0000" >
        </label>
        <p v-if="error" class="err">{{ error }}</p>
        <p v-if="done" class="ok">
          {{ form.name }}님, {{ form.count }}명 예약이 접수되었습니다. 확인 문자를 보내드립니다.
        </p>
        <button type="submit" class="submit">
          <span>예약하기</span><span>&rarr;</span>
        </button>
      </form>
    </section>

    <!-- ============ 오시는 길 / 문의 ============ -->
    <footer class="foot">
      <div class="foot-col">
        <h4>오시는 길</h4>
        <p>서울 성동구 연무장길 45, 갤러리 노이 B1</p>
        <p class="muted">수인분당선 서울숲역 3번 출구 도보 6분<br>건물 내 주차 불가 · 인근 공영주차장 이용</p>
      </div>
      <div class="foot-col">
        <h4>문의</h4>
        <p>02-462-0244</p>
        <p>hello@galleryneu.kr</p>
        <p class="muted">운영시간 내 응대</p>
      </div>
      <div class="foot-col brand">
        <p class="vertical big">VOID</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
useHead({ title: 'VOID — Exhibition Opening | Gallery Neu' })
definePageMeta({ layout: false })

const works = [
  {
    title: '無題 (Untitled)', artist: '한소예', medium: '사운드 설치', mediumLabel: 'SOUND',
    mediumKey: 'sound', year: 2026,
    img: 'https://images.unsplash.com/photo-1499781350541-7783f6c6a0c8?w=600&q=80',
    prompt: 'dark sound installation art, suspended speakers and cables in dim gallery, ambient light glow, monochrome moody tone, 4:5'
  },
  {
    title: '흰 방', artist: '도이치 켄지', medium: '공간 설치', mediumLabel: 'INSTALLATION',
    mediumKey: 'install', year: 2025,
    img: 'https://images.unsplash.com/photo-1577720580479-7d839d829c73?w=600&q=80',
    prompt: 'immersive white room installation, empty minimal architectural space, soft diffused light, avant-garde, monochrome, 4:5'
  },
  {
    title: 'Negative 07', artist: '엘사 모로', medium: '아카이벌 프린트', mediumLabel: 'PHOTO',
    mediumKey: 'photo', year: 2026,
    img: 'https://images.unsplash.com/photo-1547891654-e66ed7ebb968?w=600&q=80',
    prompt: 'high-contrast black and white archival fine art photograph, abstract negative space composition, framed print, gallery wall, 4:5'
  },
  {
    title: '중력 없는 방', artist: '진우현', medium: '영상 · 4K, 8분', mediumLabel: 'VIDEO',
    mediumKey: 'video', year: 2026,
    img: 'https://images.unsplash.com/photo-1490312278390-ab64016e0aa9?w=600&q=80',
    prompt: 'video art projection in dark room, floating abstract 4K moving imagery, glowing screen, weightless atmosphere, monochrome, 4:5'
  },
  {
    title: '틈', artist: '한소예', medium: '공간 설치', mediumLabel: 'INSTALLATION',
    mediumKey: 'install', year: 2024,
    img: 'https://images.unsplash.com/photo-1531913764164-f85c52e6e654?w=600&q=80',
    prompt: 'spatial installation of a narrow crevice of light between concrete walls, sculptural gap, minimal avant-garde, monochrome, 4:5'
  },
  {
    title: 'White Noise', artist: '엘사 모로', medium: '사운드 설치', mediumLabel: 'SOUND',
    mediumKey: 'sound', year: 2025,
    img: 'https://images.unsplash.com/photo-1518998053901-5348d3961a04?w=600&q=80',
    prompt: 'sound art installation evoking static white noise, grainy textured surface, subtle vibration visualized, monochrome minimal, 4:5'
  }
]

const filters = [
  { key: 'all', label: '전체' },
  { key: 'install', label: '설치' },
  { key: 'sound', label: '사운드' },
  { key: 'video', label: '영상' },
  { key: 'photo', label: '사진' }
]

const filter = ref('all')
const filteredWorks = computed(() =>
  filter.value === 'all' ? works : works.filter(w => w.mediumKey === filter.value)
)

const route = [
  { name: '제1전시실 — 공백의 입구', desc: '어둠 속에서 시작해 점차 빛이 스며드는 도입부. 소리와 침묵의 대비를 경험한다.' },
  { name: '제2전시실 — 흰 방', desc: '전시의 중심. 대형 공간 설치작을 관통하며 걷는 몰입형 동선.' },
  { name: '아카이브 라운지 — 잔상', desc: '작가 노트와 드로잉, 영상 아카이브로 마무리하는 휴식 구간.' }
]

const programs = [
  { time: '10.24 (토) 19:00', title: '오프닝 리셉션', desc: '큐레이터 서지원의 오프닝 토크와 참여 작가 소개.' },
  { time: '매주 토 15:00', title: '정규 도슨트', desc: '전시 해설사가 함께하는 45분 가이드 투어. 사전 신청 불필요.' },
  { time: '11.08 (일) 14:00', title: '작가와의 대화', desc: '한소예 · 진우현 작가가 참여하는 아티스트 토크.' },
  { time: '11.22 (토) 11:00', title: '어린이 워크숍', desc: '&lsquo;비어있음&rsquo;을 그려보는 8&ndash;12세 대상 드로잉 워크숍.' }
]

const form = reactive({ name: '', count: 1, date: '', phone: '' })
const error = ref('')
const done = ref(false)

function submit() {
  done.value = false
  if (!form.name || form.name.length < 2) {
    error.value = '성함을 2자 이상 입력해 주세요.'
    return
  }
  error.value = ''
  done.value = true
}

onMounted(() => {
  if (typeof IntersectionObserver === 'undefined') return
  const io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (e.isIntersecting) {
        e.target.classList.add('in')
        io.unobserve(e.target)
      }
    })
  }, { threshold: 0.12 })
  document.querySelectorAll('.reveal').forEach(el => io.observe(el))
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&display=swap');

.ex {
  background: #d9d9d9;
  color: #111;
  font-family: 'Syne', sans-serif;
  min-height: 100vh;
  overflow-x: hidden;
}

.idx {
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 3px;
  display: block;
}

h2 {
  font-size: clamp(1.6rem, 4vw, 2.6rem);
  font-weight: 800;
  line-height: 1;
  margin: 0.4rem 0 1.6rem;
}

.vertical, .vertical-side, .vertical.big {
  writing-mode: vertical-rl;
  text-orientation: mixed;
}

/* ---------- HERO ---------- */
.hero {
  position: relative;
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  min-height: 92vh;
  border-bottom: 1px solid #999;
}

.hero-media {
  position: relative;
  border-right: 1px solid #999;
}

.hero-media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(100%) contrast(1.15);
}

.hero-type {
  padding: clamp(2rem, 5vw, 5rem);
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: #ececec;
}

.kicker {
  font-size: 0.75rem;
  letter-spacing: 3px;
  font-weight: 700;
}

.hero-type h1 {
  font-size: clamp(4rem, 16vw, 11rem);
  font-weight: 800;
  line-height: 0.82;
  letter-spacing: -0.04em;
  margin: 1rem 0;
}

.sub {
  font-size: 1.4rem;
  font-weight: 600;
}

.hero-meta {
  margin-top: 2.5rem;
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 1px;
  border-top: 1px solid #111;
  padding-top: 1.2rem;
}

.vertical-side {
  position: absolute;
  right: 1rem;
  bottom: 2rem;
  font-size: 0.7rem;
  letter-spacing: 4px;
  color: #fff;
  mix-blend-mode: difference;
  font-weight: 700;
}

/* ---------- shared label rail ---------- */
.ov-label {
  border-right: 1px solid #999;
  padding: 2rem 1.2rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  align-items: center;
  background: #111;
  color: #fff;
}

.ov-label .vertical {
  font-size: 1rem;
  letter-spacing: 6px;
  font-weight: 700;
}

/* ---------- overview ---------- */
.overview, .route, .program {
  display: grid;
  grid-template-columns: auto 1fr;
  border-bottom: 1px solid #999;
}

.ov-body, .route-body, .program-body {
  padding: clamp(2rem, 5vw, 4.5rem);
  background: #ececec;
}

.statement {
  font-size: clamp(1.05rem, 2vw, 1.35rem);
  line-height: 1.7;
  max-width: 46ch;
  margin-bottom: 3rem;
}

.ov-facts {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 0;
  border-top: 1px solid #111;
}

.ov-facts > div {
  padding: 1.2rem 0;
  border-bottom: 1px solid #bbb;
}

.ov-facts dt {
  font-size: 0.7rem;
  letter-spacing: 2px;
  font-weight: 700;
  color: #555;
  margin-bottom: 0.4rem;
}

.ov-facts dd {
  font-size: 1rem;
  font-weight: 700;
}

/* ---------- works ---------- */
.works {
  padding: clamp(2rem, 5vw, 4.5rem);
  background: #d9d9d9;
  border-bottom: 1px solid #999;
}

.works-head {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-end;
  justify-content: space-between;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.filters { display: flex; flex-wrap: wrap; gap: 0.5rem; }

.chip {
  background: transparent;
  border: 1px solid #111;
  color: #111;
  padding: 0.5rem 1.1rem;
  font-family: inherit;
  font-weight: 700;
  font-size: 0.8rem;
  letter-spacing: 1px;
  cursor: pointer;
  transition: all 0.2s;
}

.chip.on, .chip:hover {
  background: #111;
  color: #fff;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 1px;
  background: #999;
  border: 1px solid #999;
}

.work {
  background: #ececec;
  padding: 0;
}

.work-img {
  position: relative;
  aspect-ratio: 4 / 5;
  overflow: hidden;
}

.work-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(100%) contrast(1.1);
  transition: transform 0.5s, filter 0.5s;
}

.work:hover .work-img img {
  transform: scale(1.05);
  filter: grayscale(0%) contrast(1);
}

.medium-tag {
  position: absolute;
  top: 0.8rem;
  left: 0.8rem;
  background: #fff;
  border: 1px solid #000;
  padding: 0.2rem 0.6rem;
  font-size: 0.65rem;
  letter-spacing: 2px;
  font-weight: 700;
}

.work-info { padding: 1.2rem; }
.work-info h3 { font-size: 1.3rem; font-weight: 800; }
.artist { font-weight: 700; margin: 0.2rem 0; }
.detail { font-size: 0.85rem; color: #555; }
.empty { text-align: center; padding: 2rem; font-weight: 700; }

/* ---------- route ---------- */
.route-list { list-style: none; }
.route-list li {
  display: flex;
  gap: 1.5rem;
  padding: 1.6rem 0;
  border-bottom: 1px solid #bbb;
}
.route-list li:last-child { border-bottom: none; }
.rnum { font-size: 2rem; font-weight: 800; line-height: 1; color: #111; }
.route-list h4 { font-size: 1.2rem; font-weight: 800; margin-bottom: 0.3rem; }
.route-list p { line-height: 1.6; max-width: 50ch; }

/* ---------- visit ---------- */
.visit {
  padding: clamp(2rem, 5vw, 4.5rem);
  background: #111;
  color: #fff;
  border-bottom: 1px solid #000;
}
.visit .idx { color: #fff; }
.visit h2 { color: #fff; }
.visit-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1px;
  background: #444;
  border: 1px solid #444;
}
.v-card { background: #111; padding: 2rem; }
.v-card h4 {
  font-size: 0.8rem;
  letter-spacing: 2px;
  border-bottom: 1px solid #555;
  padding-bottom: 0.8rem;
  margin-bottom: 1rem;
}
.v-card p { line-height: 1.6; margin-bottom: 0.3rem; }
.muted { color: #999; font-size: 0.85rem; }
.fee { list-style: none; }
.fee li {
  display: flex;
  justify-content: space-between;
  padding: 0.6rem 0;
  border-bottom: 1px solid #333;
  font-weight: 700;
}
.fee li:last-child { border-bottom: none; }

/* ---------- program ---------- */
.sched { list-style: none; }
.sched li {
  display: grid;
  grid-template-columns: 180px 1fr;
  gap: 1.5rem;
  padding: 1.4rem 0;
  border-bottom: 1px solid #bbb;
}
.sched li:last-child { border-bottom: none; }
.time { font-weight: 800; letter-spacing: 1px; }
.sched h4 { font-size: 1.1rem; font-weight: 800; margin-bottom: 0.3rem; }
.sched p { line-height: 1.6; }

/* ---------- rsvp ---------- */
.rsvp-sec {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  border-bottom: 1px solid #999;
}
.rsvp-type {
  background: #111;
  color: #fff;
  padding: clamp(2rem, 5vw, 4.5rem);
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.rsvp-type .idx { color: #fff; }
.rsvp-type h2 {
  color: #fff;
  font-size: clamp(2.5rem, 6vw, 4.5rem);
  line-height: 0.9;
}
.rsvp-note { line-height: 1.6; color: #ccc; font-weight: 700; }
.rsvp-form {
  background: #ececec;
  padding: clamp(2rem, 5vw, 4.5rem);
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}
.rsvp-form label { display: flex; flex-direction: column; gap: 0.4rem; }
.rsvp-form span { font-size: 0.75rem; letter-spacing: 2px; font-weight: 700; }
.rsvp-form input, .rsvp-form select {
  background: transparent;
  border: none;
  border-bottom: 1px solid #111;
  padding: 0.7rem 0;
  font-family: inherit;
  font-size: 1rem;
  color: #111;
}
.rsvp-form input:focus, .rsvp-form select:focus { outline: none; border-bottom-width: 2px; }
.err { color: #b00020; font-weight: 700; font-size: 0.9rem; }
.ok { color: #0a5c2b; font-weight: 700; font-size: 0.9rem; }
.submit {
  background: #111;
  color: #fff;
  border: 1px solid #111;
  padding: 1.1rem 1.5rem;
  font-family: inherit;
  font-weight: 800;
  letter-spacing: 1px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  transition: background 0.3s, color 0.3s;
}
.submit:hover { background: transparent; color: #111; }

/* ---------- footer ---------- */
.foot {
  display: grid;
  grid-template-columns: 1fr 1fr auto;
  background: #ececec;
}
.foot-col {
  padding: clamp(2rem, 5vw, 4rem);
  border-right: 1px solid #999;
}
.foot-col h4 {
  font-size: 0.8rem;
  letter-spacing: 2px;
  margin-bottom: 1rem;
}
.foot-col p { line-height: 1.6; margin-bottom: 0.3rem; font-weight: 600; }
.brand {
  background: #111;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  border-right: none;
}
.vertical.big {
  font-size: clamp(3rem, 8vw, 6rem);
  font-weight: 800;
  letter-spacing: 0.1em;
}

/* ---------- reveal ---------- */
.reveal {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.reveal.in { opacity: 1; transform: none; }

/* ---------- responsive ---------- */
@media (max-width: 820px) {
  .hero { grid-template-columns: 1fr; min-height: auto; }
  .hero-media { border-right: none; border-bottom: 1px solid #999; aspect-ratio: 3/4; }
  .overview, .route, .program, .rsvp-sec, .foot { grid-template-columns: 1fr; }
  .ov-label { flex-direction: row; border-right: none; border-bottom: 1px solid #999; padding: 1rem; }
  .ov-label .vertical { writing-mode: horizontal-tb; }
  .foot-col { border-right: none; border-bottom: 1px solid #999; }
  .brand { padding: 3rem; }
  .vertical.big { writing-mode: horizontal-tb; }
  .sched li { grid-template-columns: 1fr; gap: 0.4rem; }
  .vertical-side { display: none; }
}
@media (prefers-reduced-motion: reduce) {
  .reveal { opacity: 1; transform: none; transition: none; }
}
</style>
