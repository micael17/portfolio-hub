<template>
  <main class="studio">
    <header>
      <a href="#top">FORM / FIELD</a>
      <span>ARCHITECTURE STUDIO · SEOUL — JEJU</span>
      <button @click="menu = !menu" :aria-label="menu ? '메뉴 닫기' : '메뉴 열기'">{{ menu ? '×' : '☰' }}</button>
    </header>
    <nav v-if="menu">
      <a href="#work" @click="menu = false">Projects</a>
      <a href="#services" @click="menu = false">Services</a>
      <a href="#office" @click="menu = false">Studio</a>
      <a href="#journal" @click="menu = false">Journal</a>
      <a href="#contact" @click="menu = false">Contact</a>
    </nav>

    <section id="top" class="hero">
      <div class="hero-title">
        <p>2026 SELECTED WORKS</p>
        <h1>공간은<br>살아가는 방식의<br><em>형태가 됩니다.</em></h1>
      </div>
      <div class="hero-image">
        <!-- AI-IMG: 현대 건축물 외관, 노출 콘크리트·자연광·미니멀 · 3:4 세로 -->
        <!-- prompt: modern concrete architecture exterior, minimal, warm natural light, vertical 3:4 -->
        <img src="https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?auto=format&fit=crop&w=1500&q=85" alt="자연광이 스며드는 현대 건축물의 외관">
        <span>01 / 06</span>
      </div>
    </section>

    <section id="work" class="projects">
      <div class="section-top">
        <p>SELECTED PROJECTS</p>
        <span>{{ filtered.length }} WORKS · 2019—2025</span>
      </div>
      <div class="filters">
        <button
          v-for="f in filters"
          :key="f.key"
          :class="{ on: filter === f.key }"
          @click="filter = f.key"
        >{{ f.label }} <em>{{ f.count }}</em></button>
      </div>
      <article v-for="project in filtered" :key="project.no" :class="['project', `project-${project.no}`]">
        <div class="project-meta">
          <span>{{ project.no }}</span>
          <p>{{ project.type }}<br>{{ project.year }}<br>{{ project.area }}</p>
        </div>
        <div class="project-copy">
          <h2>{{ project.name }}</h2>
          <p>{{ project.description }}</p>
          <a href="#contact">PROJECT NOTE ↗</a>
        </div>
        <!-- AI-IMG: 프로젝트별 건축 사진 (아래 각 item.prompt 참조) · 4:3 -->
        <!-- prompt: 아래 projects 배열의 project.prompt 필드 사용 -->
        <img :src="project.image" :alt="project.alt">
      </article>
    </section>

    <section id="services" class="services">
      <div class="section-top light">
        <p>SERVICE SCOPE</p>
        <span>WHAT WE DO</span>
      </div>
      <div class="service-grid">
        <article v-for="service in services" :key="service.no">
          <span>{{ service.no }}</span>
          <h3>{{ service.title }}</h3>
          <p>{{ service.body }}</p>
        </article>
      </div>
    </section>

    <section id="office" class="office">
      <p>OUR APPROACH</p>
      <h2>빛, 재료, 사람의 동선.<br>우리는 이 셋이 오래 편안하게 만나는 지점을 설계합니다.</h2>
      <div class="office-intro">
        <span>FORM / FIELD</span>
        <p>서울과 제주를 기반으로 주거, 문화, 상업 공간을 설계합니다. 2019년 설립 이후 32개의 프로젝트를 완성했으며, 건축의 완성은 준공일이 아니라 그 공간이 일상에 스며든 뒤부터 시작된다고 믿습니다.</p>
      </div>
      <div ref="statsEl" class="stats">
        <div v-for="stat in stats" :key="stat.label">
          <strong>{{ stat.shown }}{{ stat.suffix }}</strong>
          <span>{{ stat.label }}</span>
        </div>
      </div>
      <div class="team">
        <div v-for="member in team" :key="member.name" class="member">
          <!-- AI-IMG: 팀원 인물 사진, 스튜디오 자연광 배경 · 1:1 정방형 -->
          <!-- prompt: 아래 team 배열의 member.prompt 필드 사용 -->
          <img :src="member.image" :alt="member.alt">
          <strong>{{ member.name }}</strong>
          <span>{{ member.role }}</span>
        </div>
      </div>
    </section>

    <section id="process" class="process">
      <div class="section-top">
        <p>HOW WE WORK</p>
        <span>4 STEPS</span>
      </div>
      <ol>
        <li v-for="step in process" :key="step.no">
          <span>{{ step.no }}</span>
          <h3>{{ step.title }}</h3>
          <p>{{ step.body }}</p>
        </li>
      </ol>
    </section>

    <section id="journal" class="journal">
      <div class="section-top">
        <p>STUDIO JOURNAL</p>
        <span>NOTES & THINKING</span>
      </div>
      <a v-for="note in journal" :key="note.title" href="#contact" class="note">
        <div class="note-meta"><span>{{ note.tag }}</span><span>{{ note.date }}</span></div>
        <h3>{{ note.title }}</h3>
        <p>{{ note.excerpt }}</p>
        <em>READ NOTE ↗</em>
      </a>
    </section>

    <section id="contact" class="contact">
      <div class="contact-lead">
        <p>START A PROJECT</p>
        <h2>지어질 공간을<br>함께 상상해 볼까요.</h2>
        <ul>
          <li>hello@formfield.example</li>
          <li>서울 성동구 · 제주 서귀포</li>
          <li>+82 2 000 0000</li>
        </ul>
      </div>
      <form v-if="!sent" @submit.prevent="submit" novalidate>
        <label>이름<input v-model.trim="form.name" type="text" placeholder="성함을 적어주세요" required></label>
        <label>이메일<input v-model.trim="form.email" type="email" placeholder="회신받을 이메일" required></label>
        <label>프로젝트 유형
          <select v-model="form.type">
            <option value="residential">주거 · Residential</option>
            <option value="cultural">문화 · Cultural</option>
            <option value="commercial">상업 · Commercial</option>
            <option value="other">기타 · Other</option>
          </select>
        </label>
        <label>내용<textarea v-model.trim="form.message" rows="3" placeholder="대지 조건, 규모, 예상 일정 등을 자유롭게 적어주세요" required></textarea></label>
        <p v-if="error" class="err">{{ error }}</p>
        <button type="submit">문의 보내기 ↗</button>
      </form>
      <div v-else class="sent">
        <h3>고맙습니다, {{ form.name }}님.</h3>
        <p>문의가 접수되었습니다. 영업일 기준 2일 내 회신드리겠습니다.</p>
        <button type="button" @click="reset">새 문의 작성</button>
      </div>
    </section>

    <footer>
      <dl class="biz">
        <div><dt>상호</dt><dd>폼필드 건축사사무소 (FORM / FIELD ARCHITECTS)</dd></div>
        <div><dt>대표자</dt><dd>정한결</dd></div>
        <div><dt>사업자등록번호</dt><dd>123-45-67890</dd></div>
        <div><dt>주소</dt><dd>서울특별시 성동구 성수이로 00, 3층</dd></div>
        <div><dt>전화</dt><dd>+82 2 000 0000</dd></div>
      </dl>
      <div class="foot-bottom">
        <span>FORM / FIELD ARCHITECTS</span>
        <a href="mailto:hello@formfield.example">hello@formfield.example ↗</a>
        <span>© 2026</span>
      </div>
    </footer>
  </main>
</template>

<script setup lang="ts">
const menu = ref(false)

const projects = [
  { no: '01', type: 'RESIDENTIAL', cat: 'residential', year: '2025', area: '198㎡', name: 'A House, Seongbuk', description: '경사진 대지의 흐름을 따라 빛과 마당을 겹겹이 쌓은 단독주택.', image: 'https://images.unsplash.com/photo-1600607687939-ce8a6c25118c?auto=format&fit=crop&w=1200&q=85', alt: 'A House 성북 단독주택의 겹겹이 쌓인 마당과 빛', prompt: 'stepped hillside house, layered courtyards, natural light, 4:3' },
  { no: '02', type: 'CULTURAL', cat: 'cultural', year: '2024', area: '1,240㎡', name: 'The Archive Hall', description: '동네의 오래된 창고가 열린 기록실이 되는 과정.', image: 'https://images.unsplash.com/photo-1497366754035-f200968a6e72?auto=format&fit=crop&w=1200&q=85', alt: '기록실로 재생된 오래된 창고의 내부 공간', prompt: 'renovated warehouse turned public archive, exposed structure, 4:3' },
  { no: '03', type: 'HOSPITALITY', cat: 'commercial', year: '2023', area: '860㎡', name: 'Slow Tide, Jeju', description: '바다를 향해 천천히 열리는 작은 숙소와 공용 라운지.', image: 'https://images.unsplash.com/photo-1511818966892-d7d671e672a2?auto=format&fit=crop&w=1200&q=85', alt: '바다를 향해 열린 제주 숙소의 라운지', prompt: 'small seaside guesthouse lounge opening to ocean, jeju, 4:3' },
  { no: '04', type: 'RESIDENTIAL', cat: 'residential', year: '2025', area: '320㎡', name: 'Twin Court, Pangyo', description: '두 개의 중정을 사이에 둔 두 세대가 각자의 하늘을 갖는 집.', image: 'https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&w=1200&q=85', alt: '두 개의 중정을 가진 판교 주택 외관', prompt: 'two-household house with twin courtyards, calm modern, 4:3' },
  { no: '05', type: 'CULTURAL', cat: 'cultural', year: '2022', area: '2,100㎡', name: 'Light Museum, Yangju', description: '자연광의 하루를 전시하는 작은 미술관.', image: 'https://images.unsplash.com/photo-1518005020951-eccb494ad742?auto=format&fit=crop&w=1200&q=85', alt: '자연광이 전시가 되는 양주 미술관 외관', prompt: 'minimal art museum, daylight as exhibit, concrete, 4:3' },
  { no: '06', type: 'COMMERCIAL', cat: 'commercial', year: '2024', area: '540㎡', name: 'Fold Flagship, Seongsu', description: '접힌 파사드 뒤로 브랜드의 리듬을 담은 성수동 플래그십.', image: 'https://images.unsplash.com/photo-1481253127861-534498168948?auto=format&fit=crop&w=1200&q=85', alt: '접힌 파사드가 특징인 성수동 상업 플래그십', prompt: 'flagship retail store, folded facade, urban seongsu, 4:3' }
]

const filter = ref<'all' | 'residential' | 'cultural' | 'commercial'>('all')
const filtered = computed(() => filter.value === 'all' ? projects : projects.filter(p => p.cat === filter.value))
const filters = computed(() => ([
  { key: 'all', label: 'ALL', count: projects.length },
  { key: 'residential', label: '주거', count: projects.filter(p => p.cat === 'residential').length },
  { key: 'cultural', label: '문화', count: projects.filter(p => p.cat === 'cultural').length },
  { key: 'commercial', label: '상업', count: projects.filter(p => p.cat === 'commercial').length }
] as const))

const services = [
  { no: '01', title: '건축 설계', body: '대지 분석부터 기획·계획·실시설계까지. 사는 사람의 하루에서 출발하는 설계.' },
  { no: '02', title: '인허가 · 감리', body: '인허가 협의와 시공 감리를 직접 챙겨, 도면과 현장 사이의 간극을 좁힙니다.' },
  { no: '03', title: '인테리어', body: '가구·조명·마감을 공간의 골격과 하나의 언어로 다듬습니다.' },
  { no: '04', title: '리노베이션', body: '오래된 건물의 구조와 기억을 남기며 새 쓰임을 더합니다.' }
]

const stats = reactive([
  { label: '설립 이후 연차', target: 7, suffix: 'YR', shown: 0 },
  { label: '완성한 프로젝트', target: 32, suffix: '', shown: 0 },
  { label: '수상 · 발표 실적', target: 9, suffix: '', shown: 0 },
  { label: '누적 설계 면적', target: 48, suffix: 'K㎡', shown: 0 }
])

const team = [
  { name: '정한결', role: 'Principal Architect', image: 'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=600&q=85', alt: '수석 건축가 정한결의 프로필 사진', prompt: 'architect portrait, studio daylight, calm, 1:1' },
  { name: '서윤아', role: 'Project Lead', image: 'https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&w=600&q=85', alt: '프로젝트 리드 서윤아의 프로필 사진', prompt: 'architect woman portrait, studio daylight, 1:1' },
  { name: '문도현', role: 'Design & Interior', image: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?auto=format&fit=crop&w=600&q=85', alt: '디자인·인테리어 담당 문도현의 프로필 사진', prompt: 'designer man portrait, natural light, 1:1' }
]

const process = [
  { no: '01', title: '상담 · 리서치', body: '대지와 삶의 조건을 함께 읽고, 프로젝트의 방향을 정리합니다.' },
  { no: '02', title: '설계', body: '계획안을 함께 검토하며 형태·재료·동선을 구체화합니다.' },
  { no: '03', title: '시공 · 감리', body: '현장을 정기적으로 방문해 도면의 의도를 지킵니다.' },
  { no: '04', title: '준공 · 사후', body: '입주 후에도 공간이 안정되는 과정을 함께 살핍니다.' }
]

const journal = [
  { tag: 'MATERIAL', date: '2026.05', title: '노출 콘크리트가 나이 드는 방식', excerpt: '시간이 지나며 표면에 남는 얼룩과 온기를 설계의 일부로 받아들이는 태도에 대하여.' },
  { tag: 'PROCESS', date: '2026.03', title: '중정을 다시 그리는 이유', excerpt: '도심 협소지에서 마당은 사치가 아니라 빛과 환기를 위한 장치가 됩니다.' },
  { tag: 'FIELD', date: '2026.01', title: '제주에서 배운 바람의 방향', excerpt: 'Slow Tide 프로젝트에서 지역의 바람과 습기를 다룬 기록.' }
]

const form = reactive({ name: '', email: '', type: 'residential', message: '' })
const sent = ref(false)
const error = ref('')
const submit = () => {
  if (!form.name || !form.email || !form.message) {
    error.value = '이름, 이메일, 내용을 모두 입력해 주세요.'
    return
  }
  if (!/^[^@\s]+@[^@\s]+\.[^@\s]+$/.test(form.email)) {
    error.value = '이메일 형식을 확인해 주세요.'
    return
  }
  error.value = ''
  sent.value = true
}
const reset = () => {
  form.name = ''
  form.email = ''
  form.type = 'residential'
  form.message = ''
  sent.value = false
}

const statsEl = ref<HTMLElement | null>(null)
onMounted(() => {
  if (typeof IntersectionObserver === 'undefined' || !statsEl.value) return
  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (!entry.isIntersecting) return
      stats.forEach((stat) => {
        const start = performance.now()
        const tick = (now: number) => {
          const p = Math.min((now - start) / 1100, 1)
          stat.shown = Math.round(stat.target * (1 - Math.pow(1 - p, 3)))
          if (p < 1) requestAnimationFrame(tick)
        }
        requestAnimationFrame(tick)
      })
      io.disconnect()
    })
  }, { threshold: 0.4 })
  io.observe(statsEl.value)
})

useHead({ title: 'FORM / FIELD | Architecture Studio' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono&family=Instrument+Serif:ital@0;1&family=SUIT:wght@400;500;700&display=swap');
.studio{background:#e9e7df;color:#242724;min-height:100vh;font-family:SUIT,sans-serif}
header{position:sticky;top:0;z-index:4;height:68px;padding:0 3vw;border-bottom:1px solid #242724;background:#e9e7df;display:flex;align-items:center;justify-content:space-between;font:10px 'DM Mono',monospace;letter-spacing:.05em}
header a{color:inherit;text-decoration:none;font-weight:700}
header button{border:0;background:transparent;font:20px 'DM Mono',monospace;color:inherit;cursor:pointer}
nav{position:absolute;z-index:3;left:0;right:0;top:68px;display:flex;flex-wrap:wrap;gap:24px;padding:20px 3vw;background:#de3824}
nav a{color:#fff;text-decoration:none;font:20px 'Instrument Serif',serif}
.hero{display:grid;grid-template-columns:1fr 1fr;min-height:690px}
.hero-title{padding:9vw 4vw;display:flex;flex-direction:column;justify-content:space-between}
.hero-title p,.section-top,.office>p,.services .section-top{font:10px 'DM Mono',monospace;letter-spacing:.07em}
.hero h1{font:400 clamp(48px,6.3vw,94px)/.88 'Instrument Serif',serif;letter-spacing:-.06em;margin:0}
.hero h1 em{color:#de3824}
.hero-image{position:relative}
.hero-image img{width:100%;height:100%;object-fit:cover;filter:saturate(.65)}
.hero-image span{position:absolute;right:18px;bottom:18px;color:#fff;font:10px 'DM Mono',monospace}
.projects{padding:26px 3vw 100px}
.section-top{display:flex;justify-content:space-between;padding-bottom:13px;border-bottom:1px solid #242724}
.section-top p{margin:0}
.section-top.light{border-color:#ffffff55;color:#fff}
.filters{display:flex;flex-wrap:wrap;gap:10px;padding:18px 0 6px}
.filters button{cursor:pointer;background:transparent;border:1px solid #242724;color:#242724;padding:7px 15px;border-radius:40px;font:10px 'DM Mono',monospace;letter-spacing:.05em;transition:.2s}
.filters button em{opacity:.5;font-style:normal}
.filters button.on{background:#de3824;border-color:#de3824;color:#fff}
.filters button.on em{opacity:.7}
.project{display:grid;grid-template-columns:12% 31% 1fr;min-height:470px;border-bottom:1px solid #242724}
.project-meta{padding-top:20px;font:10px 'DM Mono',monospace}
.project-meta p{line-height:1.6}
.project-copy{padding:12vw 25px 25px 0;display:flex;flex-direction:column;align-items:flex-start}
.project h2{font:400 clamp(34px,4vw,60px)/.9 'Instrument Serif',serif;margin:0}
.project-copy>p{font-size:13px;line-height:1.7;max-width:200px}
.project a{margin-top:auto;color:inherit;text-decoration:none;font:10px 'DM Mono',monospace;border-bottom:1px solid;padding-bottom:4px}
.project img{width:100%;height:75%;margin:auto 0;object-fit:cover}
.project-02 img,.project-05 img{height:65%}
.services{padding:80px 3vw;background:#242724;color:#e9e7df}
.service-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:1px;margin-top:26px;background:#ffffff22}
.service-grid article{background:#242724;padding:28px 22px 34px;display:flex;flex-direction:column;min-height:230px}
.service-grid span{font:10px 'DM Mono',monospace;color:#de3824}
.service-grid h3{font:400 27px/1.1 'Instrument Serif',serif;margin:18px 0 14px}
.service-grid p{font-size:13px;line-height:1.7;opacity:.8;margin:0}
.office{padding:11vw 10vw;background:#de3824;color:#fff}
.office h2{max-width:900px;font:400 clamp(38px,5vw,72px)/1 'Instrument Serif',serif;letter-spacing:-.05em;margin:40px 0 60px}
.office-intro{display:grid;grid-template-columns:1fr 1fr;gap:30px;border-top:1px solid #ffffff99;padding-top:16px;font:10px 'DM Mono',monospace}
.office-intro p{margin:0;font:14px/1.8 SUIT,sans-serif}
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;margin:60px 0;border-top:1px solid #ffffff55;padding-top:26px}
.stats strong{display:block;font:400 clamp(42px,5vw,66px)/1 'Instrument Serif',serif}
.stats span{font:10px 'DM Mono',monospace;letter-spacing:.05em;opacity:.8}
.team{display:grid;grid-template-columns:repeat(3,1fr);gap:22px}
.member img{width:100%;aspect-ratio:1;object-fit:cover;filter:saturate(.5);margin-bottom:12px}
.member strong{display:block;font:400 22px 'Instrument Serif',serif}
.member span{font:10px 'DM Mono',monospace;opacity:.8}
.process{padding:80px 3vw}
.process ol{list-style:none;margin:26px 0 0;padding:0;display:grid;grid-template-columns:repeat(4,1fr)}
.process li{padding:24px 22px 30px;border-left:1px solid #242724;min-height:190px}
.process li:first-child{border-left:0;padding-left:0}
.process li span{font:10px 'DM Mono',monospace;color:#de3824}
.process li h3{font:400 26px/1.1 'Instrument Serif',serif;margin:14px 0 12px}
.process li p{font-size:13px;line-height:1.7;margin:0}
.journal{padding:80px 3vw}
.journal .note{display:block;text-decoration:none;color:inherit;border-top:1px solid #242724;padding:22px 0;transition:.2s}
.journal .note:hover{padding-left:14px}
.note-meta{display:flex;justify-content:space-between;font:10px 'DM Mono',monospace;color:#de3824}
.journal h3{font:400 clamp(26px,3vw,40px)/1 'Instrument Serif',serif;margin:12px 0 10px}
.journal p{font-size:13px;line-height:1.7;max-width:560px;margin:0 0 12px}
.journal em{font:10px 'DM Mono',monospace;font-style:normal;border-bottom:1px solid;padding-bottom:3px}
.contact{display:grid;grid-template-columns:1fr 1fr;background:#242724;color:#e9e7df}
.contact-lead{padding:80px 3vw;border-right:1px solid #ffffff22}
.contact-lead p{font:10px 'DM Mono',monospace;color:#de3824;margin:0}
.contact-lead h2{font:400 clamp(38px,4.5vw,62px)/1 'Instrument Serif',serif;letter-spacing:-.05em;margin:22px 0 40px}
.contact-lead ul{list-style:none;margin:0;padding:0;font:12px/2.2 'DM Mono',monospace;opacity:.85}
.contact form,.contact .sent{padding:80px 3vw;display:flex;flex-direction:column;gap:18px}
.contact label{display:flex;flex-direction:column;gap:8px;font:10px 'DM Mono',monospace;letter-spacing:.05em}
.contact input,.contact select,.contact textarea{background:transparent;border:0;border-bottom:1px solid #ffffff55;color:#e9e7df;font:15px SUIT,sans-serif;padding:8px 0;resize:vertical}
.contact input::placeholder,.contact textarea::placeholder{color:#ffffff55}
.contact select option{color:#242724}
.contact input:focus,.contact select:focus,.contact textarea:focus{outline:0;border-color:#de3824}
.contact .err{color:#ffb3a8;font:11px 'DM Mono',monospace;margin:0}
.contact button{align-self:flex-start;cursor:pointer;background:#de3824;border:0;color:#fff;padding:14px 28px;font:11px 'DM Mono',monospace;letter-spacing:.06em;margin-top:8px}
.contact .sent h3{font:400 34px 'Instrument Serif',serif;margin:0}
.contact .sent p{font-size:14px;line-height:1.8;opacity:.85;margin:0}
footer{padding:20px 3vw;font:10px 'DM Mono',monospace}
footer a{color:inherit;text-decoration:none}
.biz{display:grid;grid-template-columns:repeat(3,1fr);gap:8px 30px;margin:0 0 22px;padding-bottom:22px;border-bottom:1px solid #24272433}
.biz div{display:flex;gap:10px;line-height:1.7}
.biz dt{color:#de3824;white-space:nowrap;min-width:78px}
.biz dd{margin:0;opacity:.85}
.foot-bottom{display:flex;justify-content:space-between;gap:15px;flex-wrap:wrap}
@media(max-width:850px){
  .service-grid,.process ol,.team{grid-template-columns:repeat(2,1fr)}
  .stats{grid-template-columns:repeat(2,1fr)}
  .process li:nth-child(-n+2){border-left:0;padding-left:0}
}
@media(max-width:650px){
  header span{display:none}
  .hero{grid-template-columns:1fr;min-height:0}
  .hero-title{height:490px;padding:45px 24px}
  .hero h1{font-size:57px}
  .hero-image{height:430px}
  .projects{padding:20px 16px 65px}
  .project{grid-template-columns:50px 1fr;min-height:0;padding:25px 0}
  .project-meta{grid-row:span 2;padding-top:0}
  .project-copy{padding:0;min-height:185px}
  .project h2{font-size:42px}
  .project img{grid-column:2;height:270px!important;margin-top:20px}
  .services,.process,.journal{padding:60px 24px}
  .service-grid,.process ol,.team,.stats,.contact{grid-template-columns:1fr}
  .service-grid article{min-height:0}
  .process li{border-left:0!important;padding-left:0!important}
  .office{padding:75px 24px}
  .office h2{font-size:43px;margin:30px 0 50px}
  .office-intro{grid-template-columns:1fr}
  .office-intro p{font-size:13px}
  .contact-lead{border-right:0;border-bottom:1px solid #ffffff22;padding:60px 24px}
  .contact form,.contact .sent{padding:60px 24px}
  footer{padding:20px 24px}
  .biz{grid-template-columns:1fr}
}
</style>
