<template>
  <main class="site">
    <header>
      <a class="logo" href="#top">NEXONIC</a>
      <nav><a href="#about">회사소개</a><a href="#business">사업분야</a><a href="#numbers">실적</a><a href="#faq">FAQ</a><a href="#contact">문의하기</a></nav>
      <button @click="open = !open" :aria-expanded="open" aria-label="메뉴 열기">{{ open ? '닫기' : '메뉴' }}</button>
    </header>
    <nav v-if="open" class="mobile"><a href="#about" @click="open = false">회사소개</a><a href="#business" @click="open = false">사업분야</a><a href="#numbers" @click="open = false">실적</a><a href="#faq" @click="open = false">FAQ</a><a href="#contact" @click="open = false">문의하기</a></nav>

    <section id="top" class="hero"><div><p>SMART INDUSTRY PARTNER</p><h1>더 나은 산업의<br><b>내일을 연결합니다.</b></h1><span>기술과 사람, 현장을 잇는 산업 디지털 전환 전문 기업, 넥소닉입니다.</span><a href="#business">사업분야 보기 →</a></div></section>

    <section id="about" class="intro">
      <div class="intro-top">
        <div class="intro-copy">
          <p class="label">ABOUT NEXONIC</p>
          <h2>신뢰할 수 있는 기술로<br>고객의 성장을 돕습니다.</h2>
          <p class="lead">넥소닉은 제조 현장의 데이터를 연결하고, 더 효율적인 운영을 만드는 산업 디지털 전환 전문 기업입니다. 검증된 기술력과 빠른 실행으로 고객의 다음 단계를 함께합니다.</p>
        </div>
        <!-- AI-IMG: 모던 오피스에서 협업하는 엔지니어 팀, 밝고 프로페셔널 · 4:3 -->
        <!-- prompt: engineers collaborating in a bright modern office, professional corporate atmosphere, 4:3 -->
        <img class="intro-img" src="https://images.unsplash.com/photo-1522071820081-009f0129c71c?auto=format&fit=crop&w=1000&q=85" alt="넥소닉 구성원들이 사무실에서 프로젝트를 논의하는 모습">
      </div>
      <div class="timeline">
        <p class="label">OUR HISTORY</p>
        <ol>
          <li v-for="year in history" :key="year.year"><b>{{ year.year }}</b><span>{{ year.text }}</span></li>
        </ol>
      </div>
    </section>

    <section id="business" class="business">
      <div class="heading"><p class="label">BUSINESS</p><h2>주요 사업 분야</h2></div>
      <div class="tabs" role="tablist">
        <button v-for="(item, i) in business" :key="item.title" role="tab" :aria-selected="tab === i" :class="{ active: tab === i }" @click="tab = i">{{ item.title }}</button>
      </div>
      <div class="tab-panel">
        <div class="tab-copy">
          <span class="no">{{ business[tab].no }}</span>
          <h3>{{ business[tab].title }}</h3>
          <p>{{ business[tab].text }}</p>
          <ul>
            <li v-for="point in business[tab].points" :key="point">{{ point }}</li>
          </ul>
        </div>
        <!-- AI-IMG: 스마트 팩토리 생산 라인의 자동화 설비, 첨단 산업 현장 · 4:3 -->
        <!-- prompt: automated smart factory production line, advanced industrial equipment, blue tones, 4:3 -->
        <img :src="business[tab].img" :alt="business[tab].title + ' 관련 산업 현장 이미지'">
      </div>
    </section>

    <section class="process"><div><p class="label">HOW WE WORK</p><h2>현장을 이해하고,<br>성과까지 함께합니다.</h2><p>진단부터 구축, 운영까지 한 팀이 책임집니다. 필요한 단계만 빠르게 실행합니다.</p></div><ol><li v-for="step in process" :key="step.no"><span>{{ step.no }}</span><b>{{ step.title }}</b><p>{{ step.text }}</p></li></ol></section>

    <section id="numbers" ref="numbersEl" class="numbers">
      <div class="heading"><p class="label">BY THE NUMBERS</p><h2>숫자로 보는 넥소닉</h2></div>
      <div class="num-grid">
        <div v-for="metric in metrics" :key="metric.label"><b>{{ counts[metric.key] }}{{ metric.suffix }}</b><span>{{ metric.label }}</span></div>
      </div>
    </section>

    <section class="cases"><div class="heading"><div><p class="label">CASE STUDY</p><h2>고객과 만든 변화</h2></div><a href="#contact">사례 더보기 +</a></div><div class="case-grid"><article v-for="item in cases" :key="item.client"><span>{{ item.category }}</span><h3>{{ item.client }}</h3><p>{{ item.result }}</p><b>{{ item.metric }}</b></article></div></section>

    <section class="clients">
      <p class="label">TRUSTED BY</p>
      <div class="logo-grid"><span v-for="client in clients" :key="client">{{ client }}</span></div>
    </section>

    <section id="faq" class="faq">
      <div class="heading"><p class="label">FAQ</p><h2>자주 묻는 질문</h2></div>
      <div class="faq-list">
        <div v-for="(item, i) in faqs" :key="item.q" class="faq-item" :class="{ open: openFaq === i }">
          <button @click="toggleFaq(i)" :aria-expanded="openFaq === i"><span>{{ item.q }}</span><i>{{ openFaq === i ? '−' : '+' }}</i></button>
          <p v-show="openFaq === i">{{ item.a }}</p>
        </div>
      </div>
    </section>

    <section id="contact" class="contact">
      <div class="contact-copy">
        <p class="label">CONTACT</p>
        <h2>사업 협력이<br>필요하신가요?</h2>
        <p class="lead">담당자가 확인 후 1영업일 이내 안내드리겠습니다.</p>
      </div>
      <form class="contact-form" @submit.prevent="submit">
        <template v-if="!submitted">
          <label>성함 *<input v-model="form.name" type="text" placeholder="홍길동"></label>
          <label>회사명<input v-model="form.company" type="text" placeholder="넥소닉(주)"></label>
          <label>연락처<input v-model="form.phone" type="tel" placeholder="010-0000-0000"></label>
          <label>문의 내용<textarea v-model="form.message" rows="3" placeholder="문의하실 내용을 입력해 주세요."></textarea></label>
          <p v-if="error" class="err">{{ error }}</p>
          <button type="submit">문의 접수하기 →</button>
        </template>
        <div v-else class="done">
          <b>문의가 정상 접수되었습니다.</b>
          <span>{{ form.name }}님, 담당자가 곧 연락드리겠습니다.</span>
        </div>
      </form>
    </section>

    <footer>
      <div class="foot-top"><b>NEXONIC</b><span>기술과 사람, 현장을 잇는 산업 솔루션 기업</span></div>
      <div class="biz">
        <p>상호 : 넥소닉 주식회사 (NEXONIC Co., Ltd.)</p>
        <p>대표 : 김도현 · 사업자등록번호 : 123-45-67890</p>
        <p>주소 : 서울특별시 강남구 테헤란로 000, 15층</p>
        <p>전화 : 02-0000-0000 · 이메일 : contact@nexonic.co.kr</p>
      </div>
      <span class="copy">© 2026 NEXONIC Co., Ltd. All rights reserved.</span>
    </footer>
  </main>
</template>
<script setup lang="ts">
const open = ref(false)
const tab = ref(0)
const openFaq = ref(-1)

const history = [
  { year: '2008', text: '넥소닉 설립, 산업 자동화 SI 사업 시작' },
  { year: '2014', text: '스마트 팩토리 솔루션 자체 플랫폼 출시' },
  { year: '2019', text: '제조 데이터 분석 사업부 신설, 누적 200개 프로젝트 달성' },
  { year: '2023', text: '산업 AI 관제 센터 개소, 글로벌 파트너십 확대' },
  { year: '2026', text: '제조 AI 데이터 플랫폼 고도화, 누적 320개 프로젝트' }
]

const business = [
  {
    no: '01', title: '스마트 팩토리',
    text: '현장의 설비·품질·생산 데이터를 하나로 통합하고, 실시간 모니터링과 분석으로 생산성을 높이는 맞춤형 솔루션을 제공합니다.',
    points: ['설비 데이터 실시간 수집·통합', '생산 지표 대시보드 및 알림', '평균 3개월 내 도입 완료'],
    // AI-IMG: 스마트 팩토리 대시보드가 표시된 산업 현장 · 4:3
    // prompt: smart factory dashboard on industrial floor, monitors with production data, 4:3
    img: 'https://images.unsplash.com/photo-1581091226825-a6a2a5aee158?auto=format&fit=crop&w=1000&q=85'
  },
  {
    no: '02', title: '산업 자동화',
    text: '안정적인 운영을 위한 설비 제어와 공정 자동화를 설계·구축합니다. 검증된 아키텍처로 무중단 전환을 지원합니다.',
    points: ['PLC·MES 연동 자동 제어', '무중단 라인 전환 설계', '가동률 개선 및 불량 저감'],
    // AI-IMG: 로봇 팔이 작동하는 자동화 생산 라인 · 4:3
    // prompt: robotic arms on automated production line, industrial automation, 4:3
    img: 'https://images.unsplash.com/photo-1565043666747-69f6646db940?auto=format&fit=crop&w=1000&q=85'
  },
  {
    no: '03', title: '데이터 분석 · AI',
    text: '축적된 제조 데이터를 기반으로 예지보전, 품질 예측, 수요 예측 모델을 구축해 의사결정을 지원합니다.',
    points: ['예지보전·품질 예측 모델', '설명 가능한 분석 리포트', '운영 데이터 파이프라인 구축'],
    // AI-IMG: 데이터 분석 차트와 AI 시각화 화면 · 4:3
    // prompt: data analytics charts and AI visualization on screens, blue tones, 4:3
    img: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=1000&q=85'
  },
  {
    no: '04', title: '기술 컨설팅',
    text: '사업 목표에 맞춘 단계별 디지털 전환 전략을 설계합니다. 현재 수준 진단부터 로드맵 수립까지 함께합니다.',
    points: ['DX 성숙도 진단', '단계별 도입 로드맵', '투자 대비 효과(ROI) 검토'],
    // AI-IMG: 회의실에서 전략을 논의하는 컨설턴트 · 4:3
    // prompt: consultants discussing strategy in a meeting room, whiteboard, professional, 4:3
    img: 'https://images.unsplash.com/photo-1600880292203-757bb62b4baf?auto=format&fit=crop&w=1000&q=85'
  }
]

const process = [
  { no: '01', title: '현장 진단', text: '업무 흐름과 핵심 과제를 함께 확인합니다.' },
  { no: '02', title: '실행 설계', text: '목표와 일정에 맞춘 도입 계획을 만듭니다.' },
  { no: '03', title: '구축 · 운영', text: '안정적인 정착까지 지속적으로 지원합니다.' }
]

const metrics = [
  { key: 'years', label: '업력 (YEARS)', suffix: '' },
  { key: 'projects', label: '누적 프로젝트', suffix: '+' },
  { key: 'clients', label: '고객사', suffix: '+' },
  { key: 'retention', label: '재계약률 (%)', suffix: '%' }
]
const targets: Record<string, number> = { years: 18, projects: 320, clients: 140, retention: 96 }
const counts = reactive<Record<string, number>>({ years: 0, projects: 0, clients: 0, retention: 0 })
const numbersEl = ref<HTMLElement | null>(null)

function runCount() {
  const dur = 1400, start = performance.now(), keys = Object.keys(targets)
  requestAnimationFrame(function step(now) {
    const p = Math.min((now - start) / dur, 1)
    const e = 1 - Math.pow(1 - p, 3)
    keys.forEach(k => { counts[k] = Math.round(targets[k] * e) })
    if (p < 1) requestAnimationFrame(step)
  })
}
onMounted(() => {
  const el = numbersEl.value
  if (!el) return
  const io = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) { runCount(); io.disconnect() }
    })
  }, { threshold: 0.3 })
  io.observe(el)
})

const cases = [
  { category: 'AUTOMOTIVE', client: 'H 모빌리티', result: '생산 데이터 통합 구축', metric: '리드타임 18% 개선' },
  { category: 'CHEMICAL', client: 'K 소재', result: '공정 자동화 고도화', metric: '불량률 22% 감소' },
  { category: 'LOGISTICS', client: 'D 물류', result: '운영 관제 시스템 도입', metric: '처리량 1.6배 향상' }
]

const clients = ['H 모빌리티', 'K 소재', 'D 물류', 'S 전자', 'J 중공업', 'W 화학', 'M 정밀', 'T 에너지']

const faqs = [
  { q: '프로젝트 도입까지 얼마나 걸리나요?', a: '규모에 따라 다르지만 스마트 팩토리 기준 진단부터 구축까지 평균 3~4개월이 소요됩니다. 진단 단계에서 정확한 일정을 안내드립니다.' },
  { q: '기존에 운영 중인 설비와도 연동이 가능한가요?', a: '네. PLC·MES 등 기존 시스템과의 연동을 전제로 설계하며, 무중단 전환을 원칙으로 구축을 진행합니다.' },
  { q: '구축 이후 운영 지원도 제공하나요?', a: '구축 완료 후에도 안정적인 정착까지 유지보수와 운영 지원을 제공합니다. 별도 운영 계약을 통해 지속 관리가 가능합니다.' },
  { q: '소규모 사업장도 도입할 수 있나요?', a: '가능합니다. 필요한 기능만 단계적으로 도입하는 방식을 제안드리며, 초기 투자 부담을 낮춘 구성도 지원합니다.' },
  { q: '견적과 상담 비용이 발생하나요?', a: '초기 상담과 기본 진단은 무상으로 진행합니다. 온라인 문의를 남겨 주시면 담당자가 안내드립니다.' }
]

function toggleFaq(i: number) {
  openFaq.value = openFaq.value === i ? -1 : i
}

const form = reactive({ name: '', company: '', phone: '', message: '' })
const submitted = ref(false)
const error = ref('')
function submit() {
  if (!form.name.trim()) { error.value = '성함을 입력해 주세요.'; return }
  error.value = ''
  submitted.value = true
}

useHead({ title: 'NEXONIC | 산업 솔루션 기업' })
definePageMeta({ layout: false })
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+KR:wght@400;500;600;700&family=Manrope:wght@600;700;800&display=swap');
.site{font-family:'IBM Plex Sans KR',sans-serif;color:#17213b;background:#fff;min-height:100vh}
header{height:76px;padding:0 6vw;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #e5e8ed;position:sticky;top:0;background:#fff;z-index:10}
.logo{font:800 23px Manrope,sans-serif;letter-spacing:-.08em;color:#1b5bb6;text-decoration:none}
header nav{display:flex;gap:34px}header nav a{font-size:14px;color:inherit;text-decoration:none}
header button{display:none;border:0;background:none;font:14px inherit;cursor:pointer}
.mobile{display:none}
.hero{min-height:570px;background:linear-gradient(90deg,#071a38b8,#071a3820),url('https://images.unsplash.com/photo-1497366811353-6870744d04b2?auto=format&fit=crop&w=1600&q=85') center/cover;display:flex;align-items:center;padding:0 10vw;color:#fff}
.hero p,.label{color:#477fd0;font:700 11px Manrope,sans-serif;letter-spacing:.08em}
.hero p{color:#92b7f1}
.hero h1{font-size:clamp(38px,5vw,68px);line-height:1.3;letter-spacing:-.08em;margin:21px 0}.hero h1 b{color:#91b9fb}
.hero span{display:block;font-size:16px}
.hero a{display:inline-block;margin-top:38px;padding:14px 22px;background:#2867c5;color:#fff;text-decoration:none;font-size:14px}
.intro,.business,.cases,.numbers,.faq,.clients{padding:100px 10vw}
.intro h2,.heading h2,.contact h2,.process h2{font-size:clamp(27px,3vw,42px);letter-spacing:-.07em;line-height:1.4;margin:15px 0 25px}
.intro-top{display:grid;grid-template-columns:1.1fr .9fr;gap:60px;align-items:center}
.lead{max-width:730px;color:#5e6776;font-size:15px;line-height:1.9}
.intro-img{width:100%;height:340px;object-fit:cover;border-radius:4px}
.timeline{margin-top:80px;border-top:1px solid #dde2e9;padding-top:40px}
.timeline ol{list-style:none;margin:24px 0 0;padding:0;display:grid;grid-template-columns:repeat(5,1fr);gap:20px}
.timeline li{position:relative;padding-top:22px;border-top:3px solid #1b5bb6}
.timeline b{display:block;font:700 22px Manrope,sans-serif;color:#1b5bb6;margin-bottom:10px}
.timeline span{font-size:13px;line-height:1.6;color:#5e6776}
.business{background:#f4f7fb}
.heading{display:flex;justify-content:space-between;align-items:end}.heading h2{margin-bottom:0}.heading>a{font-size:13px;color:inherit;text-decoration:none}
.tabs{display:flex;flex-wrap:wrap;gap:10px;margin:38px 0 30px}
.tabs button{padding:11px 20px;border:1px solid #d3dbe6;background:#fff;font:600 14px inherit;color:#5e6776;cursor:pointer;border-radius:2px}
.tabs button.active{background:#1b5bb6;border-color:#1b5bb6;color:#fff}
.tab-panel{display:grid;grid-template-columns:1fr 1fr;gap:50px;align-items:center;background:#fff;border:1px solid #e4e8ee;padding:40px}
.tab-copy .no{color:#2867c5;font:700 13px Manrope,sans-serif}
.tab-copy h3{font-size:26px;margin:14px 0 16px;letter-spacing:-.05em}
.tab-copy p{font-size:15px;line-height:1.8;color:#5e6776}
.tab-copy ul{margin:22px 0 0;padding:0;list-style:none;display:grid;gap:11px}
.tab-copy li{padding-left:24px;position:relative;font-size:14px;color:#37445c}
.tab-copy li::before{content:'✓';position:absolute;left:0;color:#1b5bb6;font-weight:700}
.tab-panel img{width:100%;height:300px;object-fit:cover;border-radius:4px}
.process{padding:100px 10vw;display:grid;grid-template-columns:1fr 1fr;gap:70px;background:#173a76;color:#fff}
.process .label{color:#9fbff4}.process h2{margin-top:15px}
.process>div>p:last-child{font-size:14px;line-height:1.8;color:#c7d6ec}
.process ol{list-style:none;margin:0;padding:0;border-top:1px solid #ffffff55}
.process li{display:grid;grid-template-columns:45px 1fr;gap:3px;padding:20px 0;border-bottom:1px solid #ffffff55}
.process li span{font:700 11px Manrope,sans-serif;color:#9fbff4}.process li b{font-size:16px}
.process li p{grid-column:2;margin:6px 0 0;font-size:13px;color:#c7d6ec}
.num-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:18px;margin-top:44px}
.num-grid div{padding:34px 26px;background:#f4f7fb;border:1px solid #e4e8ee;text-align:center}
.num-grid b{display:block;font:700 clamp(34px,4vw,52px) Manrope,sans-serif;color:#1b5bb6;letter-spacing:-.03em}
.num-grid span{display:block;margin-top:8px;font-size:11px;color:#7c8491;letter-spacing:.04em}
.case-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;margin-top:38px}
.case-grid article{padding:28px;background:#f4f7fb}
.case-grid span{font:700 10px Manrope,sans-serif;color:#2867c5}
.case-grid h3{font-size:20px;margin:35px 0 9px}.case-grid p{font-size:13px;color:#697383}
.case-grid b{display:block;margin-top:30px;font-size:15px;color:#1c5dbb}
.clients{text-align:center;padding:70px 10vw;border-top:1px solid #eef1f5;border-bottom:1px solid #eef1f5}
.logo-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:1px;margin-top:28px;background:#e7ebf1;border:1px solid #e7ebf1}
.logo-grid span{background:#fff;padding:30px 10px;font:700 16px Manrope,sans-serif;color:#9aa4b3;letter-spacing:-.02em}
.faq-list{margin-top:38px;border-top:1px solid #e2e5e9}
.faq-item{border-bottom:1px solid #e2e5e9}
.faq-item button{width:100%;display:flex;justify-content:space-between;align-items:center;gap:20px;padding:24px 0;background:none;border:0;font:600 16px inherit;color:#17213b;text-align:left;cursor:pointer}
.faq-item i{font:400 26px Manrope,sans-serif;color:#1b5bb6;line-height:1}
.faq-item p{margin:0 0 24px;font-size:14px;line-height:1.9;color:#5e6776;max-width:800px}
.faq-item.open button{color:#1b5bb6}
.contact{padding:90px 10vw;background:#183c7a;color:#fff;display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:center}
.contact .label{color:#a9c7f5}.contact h2{margin-bottom:14px}
.contact .lead{font-size:14px;color:#c9d6eb}
.contact-form{display:grid;gap:14px;background:#fff;padding:34px;border-radius:4px}
.contact-form label{display:grid;gap:7px;font-size:13px;font-weight:600;color:#37445c}
.contact-form input,.contact-form textarea{padding:12px 14px;border:1px solid #d3dbe6;border-radius:3px;font:15px inherit;color:#17213b;resize:vertical}
.contact-form input:focus,.contact-form textarea:focus{outline:none;border-color:#1b5bb6}
.contact-form button{margin-top:6px;padding:15px;background:#1b5bb6;color:#fff;border:0;font:700 15px inherit;cursor:pointer;border-radius:3px}
.err{margin:0;color:#c62828;font-size:13px;font-weight:600}
.done{text-align:center;padding:30px 10px}
.done b{display:block;font-size:19px;color:#1b5bb6;margin-bottom:10px}
.done span{font-size:14px;color:#5e6776}
footer{padding:44px 10vw;background:#102a56;color:#b8c5da;font-size:12px;display:grid;gap:20px}
.foot-top{display:flex;align-items:baseline;gap:16px;flex-wrap:wrap}
.foot-top b{color:#fff;font:800 20px Manrope,sans-serif;letter-spacing:-.06em}
.biz{display:grid;gap:5px;line-height:1.5}.biz p{margin:0}
.copy{color:#7488a8;font-size:11px}
@media(max-width:850px){
  .intro-top{grid-template-columns:1fr;gap:34px}
  .tab-panel{grid-template-columns:1fr;gap:28px}
  .timeline ol{grid-template-columns:repeat(2,1fr)}
  .num-grid{grid-template-columns:repeat(2,1fr)}
  .contact{grid-template-columns:1fr;gap:32px}
}
@media(max-width:650px){
  header{padding:0 24px}header nav{display:none}header button{display:block}
  .mobile{display:grid;gap:15px;padding:22px 24px;background:#f3f7fd;position:sticky;top:76px;z-index:9}.mobile a{color:inherit;text-decoration:none}
  .hero{min-height:500px;padding:0 24px}.hero span{font-size:14px}
  .intro,.business,.cases,.numbers,.faq,.clients{padding:70px 24px}
  .intro-img{height:240px}
  .timeline{margin-top:50px}.timeline ol{grid-template-columns:1fr;gap:16px}
  .tabs{margin:28px 0 22px}
  .num-grid{grid-template-columns:1fr;margin-top:30px}
  .case-grid{grid-template-columns:1fr;margin-top:28px}
  .logo-grid{grid-template-columns:repeat(2,1fr)}
  .process{padding:70px 24px;grid-template-columns:1fr;gap:35px}
  .contact{padding:60px 24px}
  footer{padding:34px 24px}
}
</style>
