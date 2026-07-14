<template>
  <main class="clinic">
    <header><a href="#top" class="logo">nue<span>clinic</span></a><nav><a href="#care">진료 안내</a><a href="#program">프로그램</a><a href="#doctor">의료진</a><a href="#trust">클리닉 소개</a><a href="#visit">오시는 길</a><a href="#book">예약하기</a></nav><button @click="menu = !menu">{{ menu ? '닫기' : '메뉴' }}</button></header>
    <div v-if="menu" class="drawer"><a href="#care" @click="menu = false">진료 안내</a><a href="#program" @click="menu = false">프로그램</a><a href="#doctor" @click="menu = false">의료진</a><a href="#trust" @click="menu = false">클리닉 소개</a><a href="#visit" @click="menu = false">오시는 길</a><a href="#book" @click="menu = false">예약하기</a></div>

    <section id="top" class="hero">
      <div class="hero-copy"><p>SKIN, SLOWLY.</p><h1>나에게 꼭 맞는<br><em>아름다움의 속도.</em></h1><p>과한 변화보다 오래 편안한 변화. 피부의 시간표를 존중하는 프라이빗 웰니스 클리닉입니다. 피부과 전문의가 상태와 생활 리듬을 함께 읽고, 꼭 필요한 케어만 제안합니다.</p><a href="#book">첫 상담 예약하기 <span>↗</span></a></div>
      <!-- AI-IMG: 차분한 프라이빗 클리닉 대기 공간, 세이지톤·자연광·미니멀 럭셔리 · 16:9 -->
      <!-- prompt: calm private skin wellness clinic waiting room, sage tones, natural light, minimal luxury, 16:9 -->
      <img src="https://images.unsplash.com/photo-1519494026892-80bbd2d6fd0d?auto=format&fit=crop&w=1200&q=85" alt="자연광이 드는 NUE 클리닉의 차분한 대기 공간">
    </section>

    <section class="promise"><div><span>01</span><b>의료진 1:1 상담</b><p>피부 상태와 생활 리듬을 함께 읽습니다.</p></div><div><span>02</span><b>필요한 만큼만</b><p>목표와 예산에 맞는 계획을 제안합니다.</p></div><div><span>03</span><b>회복까지 케어</b><p>시술 뒤의 변화도 세심하게 확인합니다.</p></div></section>

    <section id="care" class="care">
      <p class="kicker">OUR CARE</p><h2>오늘의 피부에<br>필요한 것만.</h2>
      <div class="care-grid">
        <article v-for="item in care" :key="item.name" :class="{ open: careOpen === item.no }">
          <span>{{ item.no }}</span><h3>{{ item.name }}</h3><p class="lead">{{ item.text }}</p>
          <dl>
            <div><dt>주요 효과</dt><dd>{{ item.effect }}</dd></div>
            <div><dt>진행 과정</dt><dd>{{ item.process }}</dd></div>
            <div><dt>소요 시간</dt><dd>{{ item.time }}</dd></div>
            <div><dt>회복 기간</dt><dd>{{ item.recovery }}</dd></div>
          </dl>
          <button @click="careOpen = careOpen === item.no ? '' : item.no">{{ careOpen === item.no ? '접기 −' : '자세히 보기 ↗' }}</button>
        </article>
      </div>
      <p class="care-note">모든 케어는 초진 상담과 피부 진단 후, 개인의 상태에 맞게 강도와 주기를 조정하여 진행합니다.</p>
    </section>

    <section id="program" class="program">
      <p class="kicker">PROGRAM &amp; GUIDE</p><h2>정해진 패키지 대신,<br>당신을 위한 설계.</h2>
      <p class="program-lead">아래 안내는 프로그램의 구성과 대략적인 범위를 돕기 위한 참고 정보입니다. 최종 구성과 비용은 초진 상담에서 피부 상태를 확인한 뒤 함께 결정합니다.</p>
      <div class="program-grid">
        <article v-for="p in programs" :key="p.name">
          <p class="tag">{{ p.tag }}</p><h3>{{ p.name }}</h3><p class="desc">{{ p.desc }}</p>
          <ul><li v-for="f in p.features" :key="f">{{ f }}</li></ul>
          <p class="range"><span>상담 후 결정</span>{{ p.range }}</p>
        </article>
      </div>
      <p class="program-foot">표시된 범위는 구성·횟수에 따라 달라질 수 있으며, 상담 시 정확한 안내를 드립니다.</p>
    </section>

    <section id="doctor" class="doctor">
      <p class="kicker">OUR DOCTORS</p><h2>피부의 시간을<br>함께 읽는 사람들.</h2>
      <div class="doctor-grid">
        <article v-for="d in doctors" :key="d.name">
          <!-- AI-IMG: 세이지톤 배경의 피부과 전문의 프로필 인물사진, 차분한 자연광·미니멀 · 3:4 -->
          <!-- prompt: professional dermatologist portrait, sage-toned neutral background, calm natural light, minimal clean style, 3:4 -->
          <img :src="d.img" :alt="`${d.name} ${d.title} 프로필 사진`">
          <div class="d-body">
            <h3>{{ d.name }}</h3><p class="d-title">{{ d.title }}</p>
            <ul><li v-for="b in d.bio" :key="b">{{ b }}</li></ul>
          </div>
        </article>
      </div>
      <p class="care-note">모든 진료는 피부과 전문의가 직접 상담하고 케어 계획을 설계합니다.</p>
    </section>

    <section id="trust" class="trust numbers">
      <p class="kicker">NUE CLINIC IN NUMBERS</p><h2>천천히, 그러나<br>꾸준히 쌓아온 신뢰.</h2>
      <div class="stat-grid">
        <div v-for="s in stats" :key="s.label"><b>{{ display[s.key] }}<i>{{ s.suffix }}</i></b><p>{{ s.label }}</p></div>
      </div>
    </section>

    <section class="reviews">
      <p class="kicker">VOICES</p><h2>먼저 다녀간<br>분들의 이야기.</h2>
      <div class="review-grid">
        <blockquote v-for="r in reviews" :key="r.name"><p>&ldquo;{{ r.text }}&rdquo;</p><footer><b>{{ r.name }}</b><span>{{ r.meta }}</span></footer></blockquote>
      </div>
    </section>

    <section id="journal" class="journal"><div><p class="kicker">NUE JOURNAL</p><h2>아름다움은<br>정보에서 시작됩니다.</h2><a href="#book">더 읽어보기 →</a></div><div class="journal-note"><p>SEASONAL NOTE / 07</p><h3>여름철 예민해진 피부,<br>무엇부터 줄여야 할까요?</h3><span>피부과 전문의 노트</span></div></section>

    <section id="visit" class="visit">
      <div class="visit-info">
        <p class="kicker">VISIT US</p><h2>오시는 길 &amp;<br>운영 시간.</h2>
        <dl>
          <div><dt>주소</dt><dd>서울 강남구 도산대로 128, NUE빌딩 4F<br><small>지하철 압구정로데오역 5번 출구 도보 6분</small></dd></div>
          <div><dt>운영 시간</dt><dd>월–금 10:00 – 19:00<br>토요일 10:00 – 16:00 · 일요일·공휴일 휴진<br><small>야간 진료(수요일)는 예약제로 20:00까지 운영</small></dd></div>
          <div><dt>주차</dt><dd>건물 지하 주차장 이용 · 진료 시 2시간 무료</dd></div>
          <div><dt>전화</dt><dd>02-540-0128</dd></div>
        </dl>
        <a href="#book">방문 상담 예약하기 →</a>
      </div>
      <!-- AI-IMG: 도산공원 인근 조용한 가로수길, 세이지·베이지 톤 도시 풍경 · 4:5 -->
      <!-- prompt: quiet tree-lined street near Dosan park Seoul, sage and beige tones, soft daylight, calm urban scene, 4:5 -->
      <img src="https://images.unsplash.com/photo-1497366754035-f200968a6e72?auto=format&fit=crop&w=900&q=85" alt="가로수가 늘어선 클리닉 인근 거리 풍경">
    </section>

    <section class="faq">
      <p class="kicker">FAQ</p><h2>자주 묻는<br>질문들.</h2>
      <div class="faq-list">
        <div v-for="(f, i) in faqs" :key="i" class="faq-item" :class="{ open: openFaq === i }">
          <button :aria-expanded="openFaq === i" @click="openFaq = openFaq === i ? -1 : i"><span>{{ f.q }}</span><i>{{ openFaq === i ? '−' : '+' }}</i></button>
          <p v-show="openFaq === i">{{ f.a }}</p>
        </div>
      </div>
    </section>

    <section id="book" class="booking"><p class="kicker">PRIVATE CONSULTATION</p><h2>나를 알아가는<br>첫 번째 시간.</h2><p class="booking-lead">간단한 문의를 남겨주시면 상담 매니저가 희망 시간을 확인해 연락드립니다. 초진 상담은 약 30분간 진행됩니다.</p><button @click="requested = true">{{ requested ? '상담 요청이 접수되었어요. 곧 연락드릴게요.' : '상담 예약 문의하기' }} <span>↗</span></button><p class="booking-hours">월–금 10:00 – 19:00 · 토 10:00 – 16:00 · 서울 강남구 도산대로 128</p></section>

    <footer>
      <div class="foot-top"><a href="#top" class="logo">nue<span>clinic</span></a><nav><a href="#care">진료 안내</a><a href="#program">프로그램</a><a href="#visit">오시는 길</a><a href="#book">예약하기</a></nav></div>
      <div class="foot-biz">
        <p>뉴클리닉의원 · 대표원장 서지원 · 사업자등록번호 128-90-04572</p>
        <p>서울 강남구 도산대로 128, NUE빌딩 4F · 대표전화 02-540-0128</p>
        <p>의료광고 심의필 제2026-000128호 · 진료과목 피부과</p>
        <p class="copy">© 2026 NUE CLINIC. 본 페이지의 시술 정보는 참고용이며, 효과와 회복은 개인에 따라 다를 수 있습니다.</p>
      </div>
    </footer>
  </main>
</template>
<script setup lang="ts">
const menu = ref(false), requested = ref(false)
const careOpen = ref('')
const openFaq = ref(-1)

const care = [
  { no:'A', name:'Skin Reset', text:'피부 장벽과 결을 다듬는 기초 케어',
    effect:'거칠어진 피부결 정돈, 수분 밸런스 회복, 예민함 완화', process:'클렌징 → 피부 진단 → 저자극 각질·모공 케어 → 진정·보습 마무리', time:'약 50–60분', recovery:'일상 즉시 복귀 · 당일 약간의 홍조가 있을 수 있음' },
  { no:'B', name:'Skin Balance', text:'탄력과 윤곽의 균형을 찾는 리프팅',
    effect:'처진 라인 개선, 탄력 강화, 얼굴 윤곽 균형 정돈', process:'상담 → 부위 설계 → 고주파·초음파 기반 탄력 케어 → 냉각 진정', time:'약 60–80분', recovery:'1–2일 내 미세한 붓기 · 자연스럽게 가라앉음' },
  { no:'C', name:'Skin Glow', text:'칙칙한 안색에 맑은 밀도를 더하는 케어',
    effect:'안색 톤 개선, 색소 완화, 피부 광채와 밀도 향상', process:'진단 → 톤·색소 분석 → 레이저·영양 케어 → 자외선 차단 마무리', time:'약 40–60분', recovery:'2–3일 가벼운 각질 발생 가능 · 보습·자외선 차단 권장' },
]

const programs = [
  { tag:'FIRST STEP', name:'초진 상담 + 피부 진단', desc:'처음 방문하는 분을 위한 진단 중심 프로그램. 피부 상태를 함께 확인하고 방향을 설계합니다.', features:['전문의 1:1 상담 (약 30분)','피부 측정·분석','맞춤 케어 로드맵 제안'], range:'상담·진단 위주 구성' },
  { tag:'SIGNATURE', name:'시그니처 케어 코스', desc:'하나의 케어를 주기적으로 이어가는 분을 위한 구성. 상태에 따라 강도를 조정합니다.', features:['Reset · Balance · Glow 중 선택','회차별 상태 점검','홈케어 가이드 제공'], range:'회차·구성에 따라 상이' },
  { tag:'CUSTOM', name:'맞춤 복합 설계', desc:'여러 고민을 함께 다루는 분을 위한 개인 맞춤 설계. 우선순위를 정해 단계적으로 진행합니다.', features:['복합 케어 조합 설계','단계별 진행 계획','정기 경과 확인'], range:'상담 후 개별 견적' },
]

const doctors = [
  { name:'서지원', title:'대표원장 · 피부과 전문의',
    img:'https://images.unsplash.com/photo-1559839734-2b71ea197ec2?auto=format&fit=crop&w=600&q=85',
    bio:['대한피부과학회 정회원','피부 장벽·색소 치료 세부 진료','전) 대학병원 피부과 임상강사'] },
  { name:'이하린', title:'진료원장 · 피부과 전문의',
    img:'https://images.unsplash.com/photo-1594824476967-48c8b964273f?auto=format&fit=crop&w=600&q=85',
    bio:['대한피부과학회 정회원','레이저·탄력 시술 다수 임상 경험','예민 피부 케어 세부 진료'] },
]

const stats = [
  { key:'consult', label:'누적 상담 건수', target:12400, suffix:'+' },
  { key:'revisit', label:'재방문율', target:88, suffix:'%' },
  { key:'doctors', label:'피부과 전문의', target:4, suffix:'명' },
  { key:'years', label:'운영 연차', target:11, suffix:'년' },
]
const display = reactive<Record<string, number>>({ consult:0, revisit:0, doctors:0, years:0 })

const reviews = [
  { text:'무조건 시술부터 권하지 않고 지금은 뭘 줄여야 하는지 먼저 짚어주셔서 신뢰가 갔어요. 피부가 편안해진 게 느껴집니다.', name:'김OO', meta:'Skin Reset · 30대' },
  { text:'과하지 않게, 딱 필요한 만큼만 제안해주셔서 좋았어요. 회복 기간과 주의사항까지 문자로 챙겨주신 점이 인상적이었습니다.', name:'이OO', meta:'Skin Balance · 40대' },
  { text:'상담이 정말 꼼꼼했어요. 예산 이야기를 편하게 나눌 수 있었고, 부담스러운 권유가 없어서 다시 찾게 됩니다.', name:'박OO', meta:'Skin Glow · 20대' },
]

const faqs = [
  { q:'시술 후 회복 기간은 얼마나 걸리나요?', a:'케어 종류에 따라 다릅니다. 기초 케어는 대부분 일상에 바로 복귀할 수 있고, 탄력·레이저 케어는 1–3일 정도 가벼운 붓기나 각질이 있을 수 있습니다. 상담 시 개인 상태에 맞는 회복 안내를 자세히 드립니다.' },
  { q:'부작용이나 통증이 걱정됩니다.', a:'모든 케어는 전문의 진단 후 강도를 조절해 진행하며, 필요 시 냉각·마취 크림으로 자극을 최소화합니다. 홍조·미세 붓기 등 일시적 반응은 자연스럽게 가라앉으며, 이상 반응이 있으면 즉시 내원해 확인해 드립니다.' },
  { q:'시술 주기는 어떻게 잡아야 하나요?', a:'피부는 회복과 재생에 시간이 필요하므로 무리한 반복은 권하지 않습니다. 케어에 따라 보통 2–4주 간격을 권장하며, 상태 변화를 보며 주기를 조정합니다. 필요 이상으로 자주 권유하지 않는 것이 저희의 원칙입니다.' },
  { q:'상담 절차가 궁금해요. 바로 시술을 받아야 하나요?', a:'아닙니다. 첫 방문은 상담과 피부 진단 중심으로 진행되며, 당일 시술을 결정하지 않으셔도 됩니다. 상태와 목표, 예산을 함께 이야기한 뒤 충분히 고민하고 결정하실 수 있도록 안내합니다.' },
  { q:'주차가 가능한가요?', a:'네. 건물 지하 주차장을 이용하실 수 있으며, 진료 시 2시간 무료 주차를 지원합니다. 대중교통 이용 시 압구정로데오역 5번 출구에서 도보 6분 거리입니다.' },
]

let io: IntersectionObserver | null = null
onMounted(() => {
  const el = document.querySelector('.numbers')
  if (!el || typeof IntersectionObserver === 'undefined') return
  io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (!e.isIntersecting) return
      stats.forEach((s) => {
        const step = Math.max(1, Math.round(s.target / 60))
        const timer = setInterval(() => {
          const next = display[s.key] + step
          if (next >= s.target) { display[s.key] = s.target; clearInterval(timer) }
          else display[s.key] = next
        }, 20)
      })
      io?.disconnect()
    })
  }, { threshold: 0.4 })
  io.observe(el)
})
onBeforeUnmount(() => io?.disconnect())

useHead({ title: 'NUE Clinic | Private Skin Wellness' })
definePageMeta({ layout: false })
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono&family=Gowun+Batang:wght@400;700&family=Manrope:wght@400;500;600&display=swap');
.clinic{background:#fbfaf6;color:#313832;min-height:100vh;font-family:Manrope,sans-serif}
header{position:sticky;top:0;z-index:20;height:78px;padding:0 5vw;display:flex;align-items:center;justify-content:space-between;background:rgba(251,250,246,.9);backdrop-filter:blur(8px)}
.logo{color:inherit;text-decoration:none;font:700 27px/1 'Gowun Batang',serif;letter-spacing:-.12em}.logo span{font:11px Manrope,sans-serif;letter-spacing:.14em;margin-left:6px;color:#819177}
header nav{display:flex;gap:27px}header nav a{color:inherit;text-decoration:none;font-size:12px}header button{display:none;background:none;border:0;font:12px Manrope,sans-serif;color:inherit}.drawer{display:none}
.hero{display:grid;grid-template-columns:1fr 1fr;min-height:650px;background:#e8ede3}.hero-copy{padding:10vw 5vw;display:flex;flex-direction:column;justify-content:center}
.hero-copy>p:first-child,.kicker{font:10px 'DM Mono',monospace;letter-spacing:.11em;color:#75886c}
.hero h1,.care h2,.program h2,.doctor h2,.trust h2,.reviews h2,.journal h2,.visit h2,.faq h2,.booking h2{font:400 clamp(38px,5vw,69px)/1.12 'Gowun Batang',serif;letter-spacing:-.09em;margin:25px 0}
.hero h1 em{color:#72906d;font-style:normal}.hero-copy>p:nth-of-type(2){max-width:400px;font-size:14px;line-height:1.85;color:#637061}
.hero-copy a{margin-top:35px;color:inherit;text-decoration:none;font-size:13px;border-bottom:1px solid;width:max-content;padding-bottom:7px}.hero-copy a span{margin-left:40px;font-size:20px}
.hero>img{width:100%;height:100%;object-fit:cover;filter:saturate(.7)}
.promise{display:grid;grid-template-columns:repeat(3,1fr);padding:0 5vw;background:#fff}.promise div{padding:48px 30px;border-right:1px solid #e0e3da}.promise div:first-child{padding-left:0}.promise div:last-child{border:0}
.promise span{display:block;font:10px 'DM Mono',monospace;color:#8a9b80}.promise b{display:block;margin:16px 0 8px;font:700 16px 'Gowun Batang',serif}.promise p{color:#81897f;font-size:13px;line-height:1.6;margin:0}
.care{padding:120px 5vw}.care-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:13px;margin-top:50px}
.care article{padding:25px;background:#ecefe9;display:flex;flex-direction:column}.care article span{font:10px 'DM Mono',monospace;color:#78916e}
.care h3{font:700 22px 'Gowun Batang',serif;margin:40px 0 8px}.care article .lead{font-size:13px;line-height:1.7;color:#657064;margin:0}
.care article dl{max-height:0;overflow:hidden;transition:max-height .45s ease,margin .45s ease;margin:0}
.care article.open dl{max-height:400px;margin:18px 0 0}
.care article dl div{padding:9px 0;border-top:1px solid #d9ded3}.care article dt{font:10px 'DM Mono',monospace;color:#7d9072;letter-spacing:.06em;margin-bottom:4px}.care article dd{margin:0;font-size:12.5px;line-height:1.65;color:#4c554c}
.care article button{margin-top:auto;padding-top:20px;background:none;border:0;color:inherit;font:11px Manrope,sans-serif;text-align:left;cursor:pointer}
.care-note{margin-top:26px;font-size:12px;color:#8a917f;max-width:640px;line-height:1.7}
.program{padding:110px 5vw;background:#fff}.program-lead{max-width:560px;font-size:14px;line-height:1.85;color:#637061;margin:0 0 46px}
.program-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}
.program article{padding:30px 26px;background:#f4f5f0;display:flex;flex-direction:column;border:1px solid #e6e8e0}
.program .tag{font:10px 'DM Mono',monospace;letter-spacing:.12em;color:#a37052;margin:0}.program h3{font:700 20px 'Gowun Batang',serif;margin:14px 0 12px}
.program .desc{font-size:13px;line-height:1.7;color:#657064;margin:0 0 18px}
.program ul{list-style:none;padding:0;margin:0 0 24px}.program li{font-size:12.5px;color:#4c554c;padding:8px 0 8px 18px;border-top:1px solid #e2e5db;position:relative}.program li:before{content:'—';position:absolute;left:0;color:#8aa07e}
.program .range{margin:auto 0 0;font:700 15px 'Gowun Batang',serif;color:#37413a;display:flex;flex-direction:column;gap:3px}.program .range span{font:10px 'DM Mono',monospace;font-weight:400;letter-spacing:.08em;color:#a37052}
.program-foot{margin-top:24px;font-size:11.5px;color:#95998b}
.doctor{padding:115px 5vw}.doctor-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:16px;margin-top:50px}
.doctor article{display:grid;grid-template-columns:.82fr 1fr;background:#ecefe9;overflow:hidden}
.doctor img{width:100%;height:100%;min-height:290px;object-fit:cover;filter:saturate(.72)}
.doctor .d-body{padding:32px 30px;display:flex;flex-direction:column;justify-content:center}
.doctor h3{font:700 24px 'Gowun Batang',serif;margin:0}.doctor .d-title{font:10px 'DM Mono',monospace;letter-spacing:.06em;color:#78916e;margin:10px 0 22px}
.doctor ul{list-style:none;padding:0;margin:0}.doctor li{font-size:12.5px;line-height:1.6;color:#4c554c;padding:8px 0 8px 16px;border-top:1px solid #d9ded3;position:relative}.doctor li:before{content:'—';position:absolute;left:0;color:#8aa07e}
.trust{padding:115px 5vw;background:#344137;color:#f4f4eb}.trust .kicker{color:#c9dbb8}
.stat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;margin-top:52px}
.stat-grid div{border-top:1px solid #4d5b4f;padding-top:22px}.stat-grid b{display:block;font:400 clamp(38px,4vw,54px)/1 'Gowun Batang',serif;color:#dfe9d4}.stat-grid b i{font:400 16px 'Gowun Batang',serif;font-style:normal;margin-left:3px;color:#a9bd9c}
.stat-grid p{margin:14px 0 0;font-size:12px;color:#b7c2ac;letter-spacing:.02em}
.reviews{padding:115px 5vw}.review-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-top:50px}
.reviews blockquote{margin:0;padding:30px 26px;background:#ecefe9;display:flex;flex-direction:column;justify-content:space-between;min-height:230px}
.reviews blockquote p{font:400 16px/1.75 'Gowun Batang',serif;color:#3c463c;margin:0 0 24px}
.reviews footer{display:flex;flex-direction:column;gap:3px}.reviews footer b{font-size:13px;color:#37413a}.reviews footer span{font:10px 'DM Mono',monospace;color:#8a917f}
.journal{padding:100px 5vw;display:grid;grid-template-columns:1fr 1fr;gap:40px;background:#344137;color:#f4f4eb}.journal .kicker{color:#c9dbb8}.journal h2{margin-bottom:35px}.journal a{color:inherit;font-size:13px}
.journal-note{padding:27px;background:#c9d7bd;color:#304031;display:flex;flex-direction:column;justify-content:space-between;min-height:245px}.journal-note p,.journal-note span{font:10px 'DM Mono',monospace}.journal-note h3{font:400 26px/1.4 'Gowun Batang',serif}
.visit{padding:110px 5vw;display:grid;grid-template-columns:1.1fr .9fr;gap:48px;align-items:center;background:#fff}
.visit dl{margin:40px 0 34px}.visit dl div{display:grid;grid-template-columns:110px 1fr;gap:16px;padding:18px 0;border-top:1px solid #e2e5db}
.visit dt{font:10px 'DM Mono',monospace;letter-spacing:.06em;color:#7d9072;padding-top:3px}.visit dd{margin:0;font-size:14px;line-height:1.7;color:#414a41}.visit dd small{color:#8a917f;font-size:12px}
.visit-info>a{color:inherit;text-decoration:none;font-size:13px;border-bottom:1px solid;padding-bottom:6px}
.visit>img{width:100%;height:100%;max-height:520px;object-fit:cover;filter:saturate(.72)}
.faq{padding:110px 5vw;background:#f1ede4}.faq-list{margin-top:46px;max-width:820px}
.faq-item{border-top:1px solid #ddd7c9}.faq-item:last-child{border-bottom:1px solid #ddd7c9}
.faq-item button{width:100%;background:none;border:0;padding:24px 0;display:flex;align-items:center;justify-content:space-between;gap:20px;cursor:pointer;text-align:left;color:inherit}
.faq-item button span{font:700 17px 'Gowun Batang',serif}.faq-item button i{font-style:normal;font-size:22px;color:#8aa07e;flex-shrink:0}
.faq-item p{margin:0;padding:0 40px 26px 0;font-size:13.5px;line-height:1.85;color:#5c6459}
.booking{padding:115px 5vw;background:#f1dcb7}.booking .kicker{color:#a37052}.booking-lead{max-width:460px;font-size:14px;line-height:1.8;color:#7a6b52;margin:0 0 34px}
.booking button{border:0;background:#364138;color:#fff;padding:18px 22px;min-width:300px;text-align:left;font:13px Manrope,sans-serif;cursor:pointer}.booking button span{float:right;font-size:18px}
.booking-hours{font-size:11px;color:#70685e;margin-top:24px}
footer{padding:50px 5vw 40px;background:#364138;color:#d9e0d1}
.foot-top{display:flex;align-items:center;justify-content:space-between;padding-bottom:26px;border-bottom:1px solid #46523f;flex-wrap:wrap;gap:20px}
.foot-top .logo{color:#f4f4eb}.foot-top .logo span{color:#a9bd9c}
.foot-top nav{display:flex;gap:22px}.foot-top nav a{color:#c3ccba;text-decoration:none;font-size:12px}
.foot-biz{margin-top:24px}.foot-biz p{margin:0 0 7px;font:11px/1.7 'DM Mono',monospace;letter-spacing:.03em;color:#aeb9a4}.foot-biz .copy{margin-top:16px;color:#8b9683}
@media(max-width:650px){
  header nav{display:none}header button{display:block}.drawer{display:grid;gap:17px;padding:25px 5vw;background:#e8ede3}.drawer a{color:inherit;text-decoration:none;font:20px 'Gowun Batang',serif}
  .hero,.journal,.visit{grid-template-columns:1fr}.hero{min-height:0}.hero-copy{padding:80px 24px 55px}.hero>img{height:390px}
  .promise{padding:0;grid-template-columns:1fr}.promise div,.promise div:first-child{padding:25px 24px;border-right:0;border-bottom:1px solid #e0e3da}
  .care,.program,.doctor,.trust,.reviews,.visit,.faq,.booking{padding:75px 24px}
  .care-grid,.program-grid,.doctor-grid,.review-grid{grid-template-columns:1fr;margin-top:35px}
  .doctor article{grid-template-columns:1fr}.doctor img{min-height:280px}
  .stat-grid{grid-template-columns:1fr 1fr;gap:16px;margin-top:38px}
  .journal{padding:75px 24px}.journal-note{min-height:210px}
  .visit{gap:34px}.visit dl div{grid-template-columns:88px 1fr;gap:12px}.visit>img{max-height:300px}
  .booking button{min-width:0;width:100%}
  footer{padding:40px 24px 34px}.foot-top nav{gap:16px}
}
</style>
