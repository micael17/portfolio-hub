<template>
  <main class="site">
    <header><a class="brand" href="#top">RATIO<span>LAW</span></a><nav><a href="#work">업무 분야</a><a href="#people">구성원</a><a href="#record">자문 실적</a><a href="#insight">인사이트</a><a class="contact" href="#consult">상담 문의 ↗</a></nav><button class="menu" @click="open = !open">{{ open ? 'CLOSE' : 'MENU' }}</button></header>
    <div v-if="open" class="mobile-nav"><a href="#work" @click="open = false">업무 분야</a><a href="#people" @click="open = false">구성원</a><a href="#record" @click="open = false">자문 실적</a><a href="#insight" @click="open = false">인사이트</a><a href="#consult" @click="open = false">상담 문의</a></div>

    <section id="top" class="hero"><div><p class="eyebrow">SEOUL · BUSINESS LAW FIRM</p><h1>판단의 순간,<br><em>더 선명한</em><br>해답을.</h1><p class="intro">기업의 중요한 의사결정마다, 법률을 사업의 언어로 번역하는 파트너가 되겠습니다. 법인 설립부터 투자 유치, 분쟁 대응까지 성장 단계별 리스크를 함께 설계합니다.</p><a href="#consult" class="round-link">상담 시작하기 <span>→</span></a></div><div class="hero-art"><span>EST.</span><strong>2011</strong><p>STRATEGY<br>WITH<br>SUBSTANCE</p></div></section>

    <section class="numbers"><div v-for="(item, i) in numbers" :key="item.label"><b>{{ display[i] }}{{ item.suffix }}</b><span>{{ item.label }}</span></div></section>

    <section id="work" class="practice"><div class="section-label">01 / PRACTICE</div><h2>복잡할수록<br>구조부터 봅니다.</h2><p class="lead">각 분야 전담팀이 사안의 본질을 먼저 정의하고, 실행 가능한 해법으로 좁혀 나갑니다. 아래 분야를 눌러 상세 내용을 확인하세요.</p>
      <div class="practice-list">
        <article v-for="(item, i) in practice" :key="item.no">
          <button class="phead" :aria-expanded="openWork === i" :aria-controls="`work-panel-${i}`" @click="openWork = openWork === i ? -1 : i"><span>{{ item.no }}</span><h3>{{ item.title }}</h3><i :class="{ turn: openWork === i }">↗</i></button>
          <div v-show="openWork === i" :id="`work-panel-${i}`" class="pbody"><p>{{ item.description }}</p><ul><li v-for="w in item.works" :key="w">{{ w }}</li></ul></div>
        </article>
      </div>
    </section>

    <section id="people" class="people"><div class="section-label">02 / PEOPLE</div><h2>사안을 끝까지<br>책임지는 사람들.</h2>
      <div class="people-grid">
        <article v-for="p in partners" :key="p.name">
          <!-- AI-IMG: 로펌 파트너 변호사 프로필(다크·무게감, 4:5) · 각 파트너 생성 프롬프트는 배열 item.prompt 필드 참조 -->
          <img :src="p.img" :alt="p.alt" loading="lazy">
          <div class="pinfo"><h3>{{ p.name }}<em>{{ p.role }}</em></h3><p class="pfield">{{ p.field }}</p><p class="pbio">{{ p.bio }}</p></div>
        </article>
      </div>
    </section>

    <section id="record" class="record"><div class="section-label">03 / RECORD</div><h2>결과로<br>말합니다.</h2><p class="lead">고객사 비밀유지 원칙에 따라 업종과 규모 중심으로만 소개합니다.</p>
      <div class="record-list">
        <article v-for="m in matters" :key="m.title"><div class="rtop"><span>{{ m.tag }}</span><b>{{ m.metric }}</b></div><h3>{{ m.title }}</h3><p>{{ m.summary }}</p></article>
      </div>
    </section>

    <section id="insight" class="insight"><p>VIEWPOINT</p><h2>법률 자문을 넘어<br>결정의 근거를 만듭니다.</h2><div class="quote">“우리는 가장 긴 문서보다, 고객이 다음 회의에서 바로 쓸 수 있는 한 문장을 중요하게 생각합니다.”</div>
      <div class="insight-list">
        <a v-for="a in insights" :key="a.title" class="icard" href="#insight"><span class="idate">{{ a.date }} · {{ a.cat }}</span><h3>{{ a.title }}</h3><p>{{ a.excerpt }}</p><i>자세히 보기 →</i></a>
      </div>
    </section>

    <section id="process" class="process"><div class="section-label">04 / PROCESS</div><h2>상담은<br>이렇게 진행됩니다.</h2>
      <div class="step-list">
        <article v-for="s in steps" :key="s.no"><b>{{ s.no }}</b><h3>{{ s.title }}</h3><p>{{ s.desc }}</p></article>
      </div>
    </section>

    <section id="consult" class="consult"><div class="ctop"><p class="section-label">05 / CONTACT</p><h2>논의가 필요한<br>사안이 있으신가요?</h2><p class="cnote">아래 내용을 남겨 주시면 담당 변호사가 영업일 기준 1일 이내에 회신드립니다. 상담 접수 내용은 비밀유지 원칙에 따라 관리됩니다.</p><a class="cmail" href="mailto:hello@ratiolaw.example">hello@ratiolaw.example <span>↗</span></a><p class="cphone">02 6956 2011 · 서울 강남구 테헤란로 201</p></div>
      <form class="cform" @submit.prevent="submit">
        <label>성함<input v-model.trim="form.name" type="text" placeholder="홍길동" :aria-invalid="!!errors.name"></label>
        <label>연락처<input v-model.trim="form.contact" type="text" placeholder="010-0000-0000 또는 이메일" :aria-invalid="!!errors.contact"></label>
        <label>상담 분야<select v-model="form.field"><option value="">선택해 주세요</option><option v-for="item in practice" :key="item.no" :value="item.title">{{ item.title }}</option><option value="기타">기타</option></select></label>
        <label>상담 내용<textarea v-model.trim="form.message" rows="4" placeholder="사안의 배경과 원하시는 방향을 간단히 적어 주세요."></textarea></label>
        <p v-if="errorText" class="cerr">{{ errorText }}</p>
        <p v-if="sent" class="cok">상담 요청이 접수되었습니다. 담당 변호사가 곧 연락드리겠습니다.</p>
        <button type="submit" :disabled="sent">{{ sent ? '접수 완료' : '상담 요청 보내기 →' }}</button>
      </form>
    </section>

    <footer>
      <div class="fbrand">RATIO<span>LAW</span></div>
      <div class="fbiz"><p>법무법인(유한) 라티오 · 대표변호사 김도현</p><p>서울 강남구 테헤란로 201, 14층 · TEL 02 6956 2011 · FAX 02 6956 2012</p><p>사업자등록번호 214-88-01120 · 광고책임변호사 김도현</p></div>
      <p class="fcopy">© 2011–2026 RATIO LAW. SEOUL / KOREA</p>
    </footer>
  </main>
</template>
<script setup lang="ts">
const open = ref(false)
const openWork = ref(-1)

const numbers = [
  { target: 14, suffix: '', label: 'PARTNERS' },
  { target: 280, suffix: '+', label: 'MATTERS / YEAR' },
  { target: 12, suffix: '', label: 'INDUSTRIES' }
]
const display = ref(numbers.map(n => n.target))

const practice = [
  { no: '01', title: '기업 자문', description: '투자·지배구조·계약 전반의 의사결정을 함께 설계합니다. 사내 법무 인력을 대신하거나 보완하는 상시 자문으로, 성장 단계별 리스크를 선제적으로 관리합니다.', works: ['이사회·주주총회 운영 및 지배구조 설계', '표준계약서 정비 및 거래 조건 검토', '스톡옵션·임직원 보상 설계와 규정 정비'] },
  { no: '02', title: 'M&A · 투자', description: '거래 구조 검토부터 실사, 계약 협상, 클로징 이후 통합까지 빈틈없이 관리합니다. 재무·세무 자문사와 협업해 거래 리스크를 하나의 관점으로 정리합니다.', works: ['투자유치(SAFE·전환사채·상환전환우선주) 계약 자문', '법률 실사(Legal Due Diligence) 및 리스크 리포트', '주식·영업양수도 계약 협상 및 클로징 관리'] },
  { no: '03', title: '분쟁 · 리스크', description: '분쟁의 본질을 빠르게 파악하고 실질적 해결을 만듭니다. 소송뿐 아니라 협상·조정·중재를 포함해 사업에 미치는 영향을 최소화하는 전략을 우선합니다.', works: ['상사·계약 분쟁 소송 및 가처분 대응', '공정거래·하도급 관련 조사 대응', '내부통제·컴플라이언스 위반 사안 조사 및 대응'] },
  { no: '04', title: '노동 · 인사', description: '조직의 성장과 재편 과정에서 발생하는 인사·노무 리스크를 관리합니다. 취업규칙 정비부터 구조조정, 분쟁 대응까지 일관된 기준으로 지원합니다.', works: ['취업규칙·근로계약서 정비 및 노무 진단', '징계·해고 및 직장 내 괴롭힘 사안 자문', '구조조정·전적/전출 및 노동위원회 대응'] }
]

const partners = [
  { name: '김도현', role: '대표변호사', field: '기업 자문 · M&A', bio: '대형 로펌 기업금융팀을 거쳐 라티오를 설립. 성장기업의 투자유치와 인수합병 자문을 200건 이상 수행했습니다.', prompt: 'prestigious male korean lawyer portrait, dark suit, moody studio lighting, dark background, confident, 4:5', img: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?auto=format&fit=crop&w=800&q=85', alt: '김도현 대표변호사 프로필 사진' },
  { name: '이서연', role: '파트너변호사', field: '분쟁 · 리스크', bio: '판사 출신으로 상사분쟁과 경영권 분쟁을 다수 대리. 소송 이전 단계의 협상 전략 설계에 강점이 있습니다.', prompt: 'professional female korean lawyer portrait, dark blazer, moody studio lighting, dark background, composed, 4:5', img: 'https://images.unsplash.com/photo-1573497019940-1c28c88b4f3e?auto=format&fit=crop&w=800&q=85', alt: '이서연 파트너변호사 프로필 사진' },
  { name: '박준혁', role: '파트너변호사', field: '노동 · 인사', bio: '노동위원회 사건과 기업 구조조정 자문을 전담. 인사제도 설계 단계부터 분쟁 예방 관점을 반영합니다.', prompt: 'senior male korean lawyer portrait, glasses, dark suit, moody studio lighting, dark background, 4:5', img: 'https://images.unsplash.com/photo-1560250097-0b93528c311a?auto=format&fit=crop&w=800&q=85', alt: '박준혁 파트너변호사 프로필 사진' },
  { name: '정하윤', role: '변호사', field: '기업 자문 · 컴플라이언스', bio: '스타트업 사내변호사 경력을 바탕으로 규제 대응과 내부통제 체계 구축을 지원합니다.', prompt: 'young female korean lawyer portrait, dark professional attire, moody studio lighting, dark background, 4:5', img: 'https://images.unsplash.com/photo-1594744803329-e58b31de8bf5?auto=format&fit=crop&w=800&q=85', alt: '정하윤 변호사 프로필 사진' }
]

const matters = [
  { tag: 'SaaS · 시리즈B', metric: '320억', summary: '국내 B2B SaaS 기업의 시리즈B 투자유치 전 과정 자문. 텀시트 협상부터 상환전환우선주 계약 클로징까지 60일 내 완료.', title: '성장기업 투자유치 자문' },
  { tag: '제조 · 경영권', metric: '3년', summary: '중견 제조사의 경영권 분쟁을 협상·가처분·본안 병행 전략으로 대응. 소수주주 간 합의로 3년간 이어진 분쟁을 종결.', title: '경영권 분쟁 대리' },
  { tag: '유통 · M&A', metric: '18개월', summary: '유통 플랫폼 사업부 영업양수도 거래의 법률 실사와 계약 협상 수행. 인수 후 통합 과정의 노무 리스크까지 일괄 관리.', title: '사업부 인수 자문' },
  { tag: '핀테크 · 규제', metric: '상시', summary: '핀테크 스타트업의 전자금융·개인정보 규제 대응을 상시 자문으로 지원. 서비스 출시 일정에 맞춘 규제 검토 체계 구축.', title: '규제 대응 상시 자문' }
]

const insights = [
  { date: '2026.06', cat: 'M&A', title: '투자계약서의 진술·보장 조항, 어디까지 협상해야 하나', excerpt: '창업자가 놓치기 쉬운 진술·보장(R&W) 조항의 실무 쟁점과, 손해배상 한도 설정 시 확인할 세 가지 기준을 정리했습니다.' },
  { date: '2026.05', cat: 'LABOR', title: '주 52시간과 유연근무제, 취업규칙에 무엇을 담아야 하나', excerpt: '탄력·선택적 근로시간제를 도입할 때 취업규칙과 근로자대표 서면합의에서 반드시 짚어야 할 요건을 사례 중심으로 살펴봅니다.' },
  { date: '2026.04', cat: 'GOVERNANCE', title: '스타트업 지배구조, 초기 라운드에서 정해두어야 할 것들', excerpt: '주주간계약과 정관 사이의 역할 분담, 그리고 후속 투자에서 문제되지 않을 의결권·거부권 설계 방향을 제안합니다.' }
]

const steps = [
  { no: '01', title: '상담 신청', desc: '아래 문의 폼 또는 유선으로 사안을 접수합니다. 초기 정보만으로도 방향을 가늠할 수 있도록 안내합니다.' },
  { no: '02', title: '담당 배정', desc: '사안의 성격에 맞는 담당 변호사를 배정하고, 영업일 기준 1일 이내에 회신드립니다.' },
  { no: '03', title: '초기 검토', desc: '자료 확인과 1차 미팅을 통해 쟁점과 리스크, 예상 일정과 비용을 투명하게 공유합니다.' },
  { no: '04', title: '자문 진행', desc: '합의된 범위에 따라 자문을 진행하며, 진행 상황과 결정 근거를 정기적으로 보고합니다.' }
]

const form = reactive({ name: '', contact: '', field: '', message: '' })
const errors = reactive<{ name?: boolean; contact?: boolean }>({})
const errorText = ref('')
const sent = ref(false)

function submit() {
  errors.name = form.name.length < 2
  errors.contact = form.contact.length < 5
  if (errors.name || errors.contact) {
    errorText.value = '성함(2자 이상)과 연락처(5자 이상)를 정확히 입력해 주세요.'
    sent.value = false
    return
  }
  errorText.value = ''
  sent.value = true
}

onMounted(() => {
  if (typeof window === 'undefined') return
  const section = document.querySelector('.numbers')
  if (!section || !('IntersectionObserver' in window)) return
  const run = () => {
    numbers.forEach((n, i) => {
      const start = performance.now()
      const dur = 1400
      const tick = (now: number) => {
        const p = Math.min((now - start) / dur, 1)
        const eased = 1 - Math.pow(1 - p, 3)
        display.value[i] = Math.round(n.target * eased)
        if (p < 1) requestAnimationFrame(tick)
      }
      display.value[i] = 0
      requestAnimationFrame(tick)
    })
  }
  const io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (e.isIntersecting) { run(); io.disconnect() }
    })
  }, { threshold: 0.4 })
  io.observe(section)
})

useHead({ title: 'RATIO LAW | Business Law Firm' })
definePageMeta({ layout: false })
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono&family=Nanum+Myeongjo:wght@400;700&family=Plus+Jakarta+Sans:wght@400;600;700&display=swap');
.site{background:#111513;color:#e7e5de;min-height:100vh;font-family:'Plus Jakarta Sans',sans-serif}
header{height:74px;box-sizing:border-box;padding:0 5vw;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #ffffff25;position:sticky;top:0;background:#111513f2;backdrop-filter:blur(8px);z-index:20}
.brand{color:inherit;text-decoration:none;font:700 20px 'DM Mono',monospace;letter-spacing:-.12em}.brand span{color:#a9b650;margin-left:4px}
nav{display:flex;align-items:center;gap:26px}nav a{color:inherit;text-decoration:none;font-size:12px}.contact{border:1px solid #a9b650;padding:10px 15px;color:#cbd985}
.menu,.mobile-nav{display:none}
.hero{min-height:690px;padding:10vw 5vw 5vw;display:grid;grid-template-columns:1.4fr .6fr;gap:20px}
.eyebrow,.section-label{font:10px 'DM Mono',monospace;letter-spacing:.1em;color:#a9b650}
.hero h1{font:400 clamp(52px,8vw,112px)/.88 'Nanum Myeongjo',serif;letter-spacing:-.08em;margin:27px 0}.hero h1 em{font-style:italic;color:#b9c76b}
.intro{max-width:400px;font-size:15px;line-height:1.8;color:#bfc2b9}
.round-link{display:flex;justify-content:space-between;align-items:center;margin-top:45px;max-width:220px;padding:15px 0;border-bottom:1px solid #e7e5de;color:inherit;text-decoration:none;font-size:13px}.round-link span{font-size:21px}
.hero-art{border:1px solid #ffffff24;display:flex;flex-direction:column;justify-content:space-between;padding:18px;background:linear-gradient(140deg,#1b211d,#596632)}
.hero-art span,.hero-art p{font:10px 'DM Mono',monospace;letter-spacing:.1em}.hero-art strong{font:400 clamp(100px,15vw,190px)/.7 'Nanum Myeongjo',serif;color:#e9e8dd;writing-mode:vertical-rl;align-self:center}
.numbers{display:grid;grid-template-columns:repeat(3,1fr);border-top:1px solid #ffffff24;border-bottom:1px solid #ffffff24}
.numbers div{padding:42px 5vw;border-right:1px solid #ffffff24}.numbers div:last-child{border:0}
.numbers b{display:block;font:400 clamp(36px,5vw,65px)/1 'Nanum Myeongjo',serif}.numbers span{display:block;margin-top:8px;color:#a9b650;font:10px 'DM Mono',monospace}
.practice h2,.people h2,.record h2,.insight h2,.process h2,.consult h2{font:400 clamp(38px,5vw,72px)/1.1 'Nanum Myeongjo',serif;letter-spacing:-.07em;margin:25px 0 22px}
.lead{max-width:560px;color:#bfc2b9;font-size:14px;line-height:1.8;margin:0 0 48px}
.practice{padding:120px 5vw}
.practice-list{border-top:1px solid #ffffff24}
.practice-list article{border-bottom:1px solid #ffffff24}
.phead{width:100%;display:grid;grid-template-columns:70px 1fr auto;gap:20px;align-items:center;padding:26px 0;background:none;border:0;color:inherit;text-align:left;cursor:pointer;font-family:inherit}
.phead span{font:10px 'DM Mono',monospace;color:#a9b650}
.phead h3{font:600 clamp(18px,2.5vw,24px) 'Plus Jakarta Sans',sans-serif;margin:0}
.phead i{font-style:normal;font-size:22px;color:#a9b650;transition:transform .3s}.phead i.turn{transform:rotate(90deg)}
.pbody{padding:0 90px 30px 90px}
.pbody p{margin:0 0 16px;color:#cbcec6;font-size:15px;line-height:1.8;max-width:640px}
.pbody ul{margin:0;padding:0;list-style:none;display:grid;gap:10px;max-width:640px}
.pbody li{padding-left:20px;position:relative;color:#bfc2b9;font-size:14px;line-height:1.6}.pbody li::before{content:'—';position:absolute;left:0;color:#a9b650}
.people{padding:120px 5vw}
.people-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;margin-top:40px}
.people-grid article{border:1px solid #ffffff20;background:#161b18}
.people-grid img{width:100%;aspect-ratio:4/5;object-fit:cover;display:block;filter:grayscale(.35) brightness(.92)}
.pinfo{padding:20px 18px 24px}
.pinfo h3{font:600 18px 'Plus Jakarta Sans',sans-serif;margin:0;display:flex;flex-direction:column;gap:3px}.pinfo h3 em{font-style:normal;font:10px 'DM Mono',monospace;color:#a9b650;letter-spacing:.08em}
.pfield{margin:12px 0 8px;font-size:12px;color:#c6d774}
.pbio{margin:0;font-size:13px;line-height:1.7;color:#a9ada3}
.record{padding:120px 5vw}
.record-list{display:grid;grid-template-columns:repeat(2,1fr);gap:1px;background:#ffffff24;border:1px solid #ffffff24;margin-top:40px}
.record-list article{background:#111513;padding:34px 30px}
.rtop{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:16px}
.rtop span{font:10px 'DM Mono',monospace;color:#a9b650;letter-spacing:.06em}
.rtop b{font:400 clamp(28px,4vw,44px)/1 'Nanum Myeongjo',serif;color:#e9e8dd}
.record-list h3{font:600 18px 'Plus Jakarta Sans',sans-serif;margin:0 0 10px}
.record-list p{margin:0;color:#bfc2b9;font-size:14px;line-height:1.75}
.insight{padding:110px 5vw;background:#b7c36b;color:#172014}
.insight p{font:10px 'DM Mono',monospace}.insight h2{margin-bottom:40px;color:#172014}
.quote{max-width:540px;font:400 25px/1.5 'Nanum Myeongjo',serif;margin-bottom:64px}
.insight-list{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:#17201430;border:1px solid #17201430}
.icard{background:#b7c36b;padding:28px 26px;text-decoration:none;color:#172014;display:flex;flex-direction:column;transition:background .2s}
.icard:hover{background:#c2ce7c}
.idate{font:10px 'DM Mono',monospace;letter-spacing:.06em;opacity:.7}
.icard h3{font:700 20px/1.35 'Nanum Myeongjo',serif;margin:14px 0 12px}
.icard p{margin:0 0 20px;font-size:13px;line-height:1.7;color:#243019;flex:1}
.icard i{font-style:normal;font:600 12px 'Plus Jakarta Sans',sans-serif}
.process{padding:120px 5vw}
.step-list{display:grid;grid-template-columns:repeat(4,1fr);border-top:1px solid #ffffff24;margin-top:40px}
.step-list article{padding:36px 26px 0 0;border-right:1px solid #ffffff24}.step-list article:last-child{border:0}
.step-list b{display:block;font:400 clamp(34px,4vw,52px)/1 'Nanum Myeongjo',serif;color:#a9b650}
.step-list h3{font:600 17px 'Plus Jakarta Sans',sans-serif;margin:18px 0 12px}
.step-list p{margin:0;color:#bfc2b9;font-size:13px;line-height:1.75}
.consult{padding:110px 5vw;display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:start}
.consult h2{margin-bottom:26px}
.cnote{max-width:420px;font-size:14px;line-height:1.8;color:#bfc2b9;margin:0 0 40px}
.cmail{display:flex;justify-content:space-between;max-width:520px;color:#c6d774;text-decoration:none;font:400 clamp(20px,4vw,40px)/1.2 'Nanum Myeongjo',serif;border-bottom:1px solid #ffffff55;padding-bottom:14px}
.cphone{font-size:12px;color:#a9ada3;margin-top:20px}
.cform{display:grid;gap:18px}
.cform label{display:grid;gap:8px;font:10px 'DM Mono',monospace;letter-spacing:.08em;color:#a9b650}
.cform input,.cform select,.cform textarea{background:#161b18;border:1px solid #ffffff28;color:#e7e5de;padding:13px 14px;font:400 14px 'Plus Jakarta Sans',sans-serif;border-radius:0;box-sizing:border-box;width:100%}
.cform textarea{resize:vertical}
.cform input:focus,.cform select:focus,.cform textarea:focus{outline:none;border-color:#a9b650}
.cform [aria-invalid="true"]{border-color:#d47a6a}
.cerr{color:#e79b8d;font-size:12px;margin:0}
.cok{color:#c6d774;font-size:13px;margin:0}
.cform button{margin-top:6px;background:#a9b650;color:#111513;border:0;padding:15px 20px;font:700 13px 'Plus Jakarta Sans',sans-serif;cursor:pointer;justify-self:start}
.cform button:disabled{background:#596632;color:#cbd985cc;cursor:default}
footer{padding:48px 5vw 40px;border-top:1px solid #ffffff24;display:grid;gap:20px}
.fbrand{font:700 22px 'DM Mono',monospace;letter-spacing:-.12em}.fbrand span{color:#a9b650;margin-left:4px}
.fbiz p{margin:4px 0;color:#8d9288;font-size:12px;line-height:1.7}
.fcopy{color:#6f746b;font:10px 'DM Mono',monospace;margin:0}
@media(max-width:900px){.people-grid{grid-template-columns:repeat(2,1fr)}.record-list,.insight-list,.step-list{grid-template-columns:1fr}.step-list article{border-right:0;border-bottom:1px solid #ffffff24;padding:30px 0}.consult{grid-template-columns:1fr;gap:44px}}
@media(max-width:680px){nav{display:none}.menu{display:block;border:0;background:none;color:inherit;font:10px 'DM Mono',monospace}.mobile-nav{display:grid;gap:18px;padding:25px 5vw;background:#b7c36b}.mobile-nav a{color:#172014;text-decoration:none;font:700 20px 'Nanum Myeongjo',serif}.hero{min-height:620px;padding:70px 24px 24px;grid-template-columns:1fr}.hero-art{min-height:130px;display:grid;grid-template-columns:1fr auto 1fr;align-items:center}.hero-art strong{font-size:85px;writing-mode:initial}.numbers div{padding:26px 15px}.numbers b{font-size:32px}.practice,.people,.record,.process,.consult{padding:75px 24px}.insight{padding:75px 24px}.phead{grid-template-columns:38px 1fr auto}.pbody{padding:0 0 26px}.people-grid{grid-template-columns:1fr}.record-list article{padding:26px 22px}.quote{font-size:22px}}
</style>
