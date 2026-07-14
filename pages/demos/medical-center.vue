<template>
  <main class="hospital">
    <header>
      <a class="logo" href="#top">푸른마음<span>병원</span></a>
      <nav>
        <a href="#departments">진료과 안내</a>
        <a href="#doctors">의료진</a>
        <a href="#numbers">병원소개</a>
        <a href="#guide">이용안내</a>
        <a href="#location">오시는길</a>
        <a href="#reserve">진료예약</a>
      </nav>
      <button @click="menu=!menu">{{ menu ? '닫기' : '메뉴' }}</button>
    </header>
    <nav v-if="menu" class="mobile">
      <a href="#departments" @click="menu=false">진료과 안내</a>
      <a href="#doctors" @click="menu=false">의료진</a>
      <a href="#numbers" @click="menu=false">병원소개</a>
      <a href="#guide" @click="menu=false">이용안내</a>
      <a href="#location" @click="menu=false">오시는길</a>
      <a href="#reserve" @click="menu=false">진료예약</a>
    </nav>

    <section id="top" class="hero">
      <div>
        <p>당신의 건강한 일상을 위해</p>
        <h1>가장 가까운 곳에서<br><b>정성을 다하겠습니다.</b></h1>
        <p class="lead">지역 주민의 건강을 책임지는 320병상 규모의 종합병원. 응급실 24시간 운영으로 언제든 곁을 지킵니다.</p>
        <a class="btn" href="#reserve">진료 예약하기 →</a>
      </div>
    </section>

    <section class="quick">
      <a v-for="item in quick" :key="item.title" :href="item.href">
        <i>{{ item.icon }}</i><span>{{ item.title }}</span><small>{{ item.sub }}</small>
      </a>
    </section>

    <section id="departments" class="departments">
      <p class="label">MEDICAL DEPARTMENTS</p>
      <h2>진료과 안내</h2>
      <p class="sub">아래 진료과를 선택하면 주요 진료 내용과 담당 의료진을 확인하실 수 있습니다.</p>
      <div class="tabs">
        <button v-for="(d,i) in departments" :key="d.name" :class="{on:tab===i}" @click="tab=i">{{ d.name }}</button>
      </div>
      <div class="tab-panel">
        <div>
          <h3>{{ departments[tab].name }}</h3>
          <p>{{ departments[tab].desc }}</p>
          <ul>
            <li v-for="it in departments[tab].items" :key="it">{{ it }}</li>
          </ul>
          <p class="doc">담당 의료진 · {{ departments[tab].doctor }}</p>
          <a class="link" href="#reserve">이 진료과 예약하기 →</a>
        </div>
      </div>
    </section>

    <section id="doctors" class="doctors">
      <p class="label">OUR DOCTORS</p>
      <h2>환자를 먼저 생각하는 의료진</h2>
      <div class="doc-grid">
        <article v-for="doc in doctors" :key="doc.name">
          <!-- AI-IMG: 흰 가운 입은 의료진 인물 프로필, 신뢰감·화이트 배경 · 3:4 -->
          <!-- prompt: 각 의료진 이미지 프롬프트는 배열 item.prompt 참조 (과별 의사 특성 반영) -->
          <img :src="doc.img" :alt="doc.name + ' ' + doc.field + ' 프로필 사진'">
          <b>{{ doc.name }}</b>
          <span>{{ doc.field }}</span>
          <p>{{ doc.desc }}</p>
        </article>
      </div>
    </section>

    <section id="numbers" class="numbers">
      <p class="label">WE CARE</p>
      <h2>숫자로 보는 푸른마음병원</h2>
      <div class="stat-grid">
        <article v-for="(s,i) in stats" :key="s.n">
          <b>{{ counts[i] }}<em>{{ s.suffix }}</em></b>
          <span>{{ s.n }}</span>
        </article>
      </div>
    </section>

    <section id="guide" class="guide">
      <p class="label">VISIT GUIDE</p>
      <h2>이용 안내</h2>
      <div class="guide-grid">
        <article v-for="g in guides" :key="g.title">
          <i>{{ g.icon }}</i>
          <b>{{ g.title }}</b>
          <p v-html="g.text"></p>
        </article>
      </div>
      <div class="hours">
        <b>진료시간 안내</b>
        <table>
          <tbody>
            <tr v-for="h in hours" :key="h.d"><th>{{ h.d }}</th><td>{{ h.t }}</td></tr>
          </tbody>
        </table>
        <small>* 응급실은 연중무휴 24시간 운영되며, 진료과별 세부 시간은 예약 시 안내됩니다.</small>
      </div>
    </section>

    <section class="reviews">
      <p class="label">PATIENT VOICE</p>
      <h2>환자분들이 남겨주신 이야기</h2>
      <div class="rev-grid">
        <article v-for="r in reviews" :key="r.name">
          <p class="star">★★★★★</p>
          <p>“{{ r.text }}”</p>
          <span>{{ r.name }} · {{ r.dept }}</span>
        </article>
      </div>
    </section>

    <section id="location" class="location">
      <div>
        <p class="label">DIRECTIONS</p>
        <h2>오시는 길</h2>
        <p class="addr">서울시 마포구 월드컵로 000 (망원동)</p>
        <ul>
          <li v-for="w in ways" :key="w.k"><b>{{ w.k }}</b>{{ w.v }}</li>
        </ul>
        <a class="link" href="#reserve">진료 예약하기 →</a>
      </div>
      <!-- AI-IMG: 밝은 종합병원 외관, 신뢰감·화이트/블루 · 4:3 -->
      <!-- prompt: bright modern general hospital building exterior, daytime, white and blue, trustworthy, 4:3 -->
      <img src="https://images.unsplash.com/photo-1586773860418-d37222d8fce3?auto=format&fit=crop&w=1000&q=85" alt="푸른마음병원 외관 전경">
    </section>

    <section class="faq">
      <p class="label">FAQ</p>
      <h2>자주 묻는 질문</h2>
      <div class="faq-list">
        <article v-for="(f,i) in faqs" :key="f.q" :class="{on:openFaq===i}">
          <button :aria-expanded="openFaq===i" @click="openFaq = openFaq===i ? -1 : i">
            <span>{{ f.q }}</span><i>{{ openFaq===i ? '−' : '+' }}</i>
          </button>
          <p v-show="openFaq===i">{{ f.a }}</p>
        </article>
      </div>
    </section>

    <section id="reserve" class="reserve">
      <p>ONLINE RESERVATION</p>
      <h2>진료 예약 및 상담</h2>
      <p class="lead">원하시는 진료과와 시간을 남겨주시면 담당자가 확인 후 연락드립니다.</p>
      <button @click="reserved=true">{{ reserved ? '예약 신청이 접수되었습니다.' : '빠른 예약 신청하기' }} →</button>
    </section>

    <footer>
      <div>
        <b>푸른마음병원</b>
        <span>지역과 함께하는 건강한 동행</span>
      </div>
      <dl>
        <div><dt>대표자</dt><dd>김도현</dd></div>
        <div><dt>사업자등록번호</dt><dd>000-00-00000</dd></div>
        <div><dt>주소</dt><dd>서울시 마포구 월드컵로 000</dd></div>
        <div><dt>대표전화</dt><dd>02-0000-0000</dd></div>
        <div><dt>이메일</dt><dd>help@pureunmaeum.example</dd></div>
      </dl>
      <span class="copy">© PUREUNMAEUM HOSPITAL. All rights reserved.</span>
    </footer>
  </main>
</template>

<script setup lang="ts">
const menu=ref(false),reserved=ref(false),tab=ref(0),openFaq=ref(-1)

const quick=[
  {icon:'▣',title:'진료 예약',sub:'온라인 예약하기',href:'#reserve'},
  {icon:'♙',title:'의료진 찾기',sub:'전문의 안내',href:'#doctors'},
  {icon:'⌖',title:'오시는 길',sub:'교통·주차 안내',href:'#location'},
  {icon:'☎',title:'전화 상담',sub:'02-0000-0000',href:'#guide'}
]

const departments=[
  {name:'내과',desc:'소화기·호흡기·순환기 등 내과 질환을 정밀하게 진단하고 만성질환을 체계적으로 관리합니다.',items:['위·대장 내시경','고혈압·당뇨 관리','호흡기 질환 진료'],doctor:'김도현 원장'},
  {name:'정형외과',desc:'관절·척추·근골격계 손상과 통증의 원인을 확인하고 치료부터 재활까지 이어서 관리합니다.',items:['척추 클리닉','관절 질환 치료','스포츠 손상'],doctor:'이수민 과장'},
  {name:'소아청소년과',desc:'영유아 예방접종부터 성장·발달 관리까지 아이의 건강을 세심하게 살핍니다.',items:['예방접종','성장 발달 검사','감염성 질환 진료'],doctor:'박지훈 과장'},
  {name:'이비인후과',desc:'코·귀·목 질환과 알레르기, 수면 관련 질환을 정밀 진단하고 치료합니다.',items:['비염·축농증','중이염 치료','수면무호흡 검사'],doctor:'최은영 과장'},
  {name:'영상의학과',desc:'CT·MRI·초음파 등 정밀 영상 장비로 정확한 진단을 지원합니다.',items:['MRI·CT 촬영','초음파 검사','영상 판독 협진'],doctor:'정하늘 과장'},
  {name:'가정의학과',desc:'연령과 생활 습관에 맞춘 종합 건강검진과 만성질환 상담을 제공합니다.',items:['종합 건강검진','금연·비만 클리닉','예방접종 상담'],doctor:'한지우 과장'},
  {name:'신경외과',desc:'뇌·척추·말초신경 질환을 진단하고 필요한 수술적 치료를 시행합니다.',items:['척추 디스크','두통·어지럼','신경통 치료'],doctor:'오세훈 과장'},
  {name:'재활의학과',desc:'통증 치료와 개인별 재활 프로그램으로 빠른 일상 회복을 돕습니다.',items:['도수 치료','물리 치료','운동 재활'],doctor:'서다연 과장'}
]

const doctors=[
  {name:'김도현 원장',field:'내과 전문의',desc:'정확한 진단과 충분한 설명으로 믿을 수 있는 진료를 약속합니다.',img:'https://images.unsplash.com/photo-1622253692010-333f2da6031d?auto=format&fit=crop&w=500&q=85',prompt:'portrait of a senior korean male internal-medicine physician, white coat over shirt, holding a stethoscope, calm reassuring expression, bright white clinic background, 3:4'},
  {name:'이수민 과장',field:'정형외과 전문의',desc:'척추·관절 질환의 원인부터 재활까지 단계별로 함께합니다.',img:'https://images.unsplash.com/photo-1594824476967-48c8b964273f?auto=format&fit=crop&w=500&q=85',prompt:'portrait of a korean female orthopedic surgeon, white coat, confident and steady posture, spine model faintly in background, bright white clinic background, 3:4'},
  {name:'박지훈 과장',field:'소아청소년과 전문의',desc:'아이의 눈높이에 맞춰 편안하고 따뜻한 진료를 지향합니다.',img:'https://images.unsplash.com/photo-1582750433449-648ed127bb54?auto=format&fit=crop&w=500&q=85',prompt:'portrait of a friendly korean male pediatrician, white coat, warm gentle smile, soft pastel-accented clinic background, approachable, 3:4'},
  {name:'정하늘 과장',field:'영상의학과 전문의',desc:'정밀 영상 판독으로 조기 진단과 정확한 치료를 지원합니다.',img:'https://images.unsplash.com/photo-1559839734-2b71ea197ec2?auto=format&fit=crop&w=500&q=85',prompt:'portrait of a focused korean female radiologist, white coat, standing beside medical imaging monitors showing CT scans, cool blue clinic lighting, 3:4'}
]

const stats=[
  {n:'운영 병상',target:320,suffix:'병상'},
  {n:'연간 진료 건수',target:48,suffix:'만 건'},
  {n:'응급실 운영',target:24,suffix:'시간'},
  {n:'전문 의료진',target:42,suffix:'명'}
]
const counts=ref(stats.map(()=>0))

const guides=[
  {icon:'①',title:'예약 방법',text:'온라인 예약 또는 대표전화(02-0000-0000)로 원하시는 진료과와 시간을 예약하세요.'},
  {icon:'②',title:'준비물',text:'신분증, 건강보험증(모바일 가능), 타 병원 진료 기록·영상이 있으면 지참해 주세요.'},
  {icon:'③',title:'진료 절차',text:'<b>초진</b> 접수 → 진료 → 검사 → 수납<br><b>재진</b> 예약 확인 → 진료 → 수납'}
]

const hours=[
  {d:'평일 (월~금)',t:'09:00 - 18:00'},
  {d:'토요일',t:'09:00 - 13:00'},
  {d:'점심시간',t:'13:00 - 14:00'},
  {d:'일요일·공휴일',t:'휴진 (응급실 24시간 운영)'}
]

const reviews=[
  {text:'대기 시간 안내가 정확하고 검사 결과 설명이 자세해서 안심하고 진료받았습니다.',name:'박○○',dept:'내과'},
  {text:'무릎 통증으로 방문했는데 치료부터 재활까지 꼼꼼히 챙겨주셔서 감사했어요.',name:'이○○',dept:'정형외과'},
  {text:'아이가 무서워하지 않도록 친절하게 봐주셔서 다음에도 믿고 오려고 합니다.',name:'최○○',dept:'소아청소년과'}
]

const ways=[
  {k:'지하철',v:'6호선 망원역 2번 출구 도보 3분'},
  {k:'버스',v:'간선 271·604 / 지선 마포08 마을버스 하차'},
  {k:'자가용',v:'지하 1~3층 주차장 (진료 시 3시간 무료)'},
  {k:'셔틀버스',v:'합정역 ↔ 병원 구간 15분 간격 운행'}
]

const faqs=[
  {q:'예약 없이 방문해도 진료가 가능한가요?',a:'가능합니다. 다만 예약 환자 우선 진료로 대기 시간이 길어질 수 있어 온라인·전화 예약을 권장합니다.'},
  {q:'진료 예약은 어떻게 변경하나요?',a:'예약 변경 및 취소는 대표전화 또는 홈페이지 마이페이지에서 진료 전일까지 가능합니다.'},
  {q:'주차 시설이 있나요?',a:'지하 1~3층 주차장을 운영하며, 진료 시 3시간 무료 주차를 제공합니다.'},
  {q:'건강검진 결과는 언제 나오나요?',a:'기본 검진은 3~5일, 정밀 검진은 7~10일 이내 안내되며 결과 상담 일정을 별도로 예약해 드립니다.'},
  {q:'실손보험 청구 서류를 발급받을 수 있나요?',a:'원무과에서 진료비 세부내역서·진단서 등 보험 청구에 필요한 서류를 발급받으실 수 있습니다.'}
]

onMounted(()=>{
  if(typeof window==='undefined'||!('IntersectionObserver' in window))return
  const el=document.querySelector('.numbers')
  if(!el)return
  const io=new IntersectionObserver(entries=>{
    entries.forEach(e=>{
      if(!e.isIntersecting)return
      stats.forEach((s,i)=>{
        const dur=1200,start=performance.now()
        const step=(now:number)=>{
          const p=Math.min((now-start)/dur,1)
          counts.value[i]=Math.round(s.target*p)
          if(p<1)requestAnimationFrame(step)
        }
        requestAnimationFrame(step)
      })
      io.disconnect()
    })
  },{threshold:.4})
  io.observe(el)
})

useHead({title:'푸른마음병원 | 지역 종합병원'})
definePageMeta({layout:false})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;700&family=Noto+Serif+KR:wght@500;600;700&display=swap');
.hospital{font-family:'Noto Sans KR',sans-serif;color:#25343a;background:#fff;min-height:100vh}
header{height:80px;padding:0 7vw;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid #dce5e8;position:sticky;top:0;background:#fff;z-index:20}
.logo{font:700 24px 'Noto Serif KR',serif;color:#197c9b;text-decoration:none}
.logo span{font:500 18px 'Noto Sans KR',sans-serif;margin-left:3px}
header nav{display:flex;gap:26px}
header nav a{color:inherit;text-decoration:none;font-size:14px}
header button{display:none;border:0;background:0;font:14px inherit}
.mobile{display:none}
.hero{min-height:520px;background:linear-gradient(90deg,#e8f4f6ee,#e8f4f630),url('https://images.unsplash.com/photo-1584982751601-97dcc096659c?auto=format&fit=crop&w=1600&q=85') center/cover;display:flex;align-items:center;padding:0 12vw}
.hero p,.label{color:#27809a;font-size:12px;font-weight:700;letter-spacing:.04em}
.hero h1{font:600 clamp(33px,4.5vw,56px)/1.4 'Noto Serif KR',serif;letter-spacing:-.09em;margin:18px 0 20px}
.hero h1 b{color:#167b99}
.hero .lead{font-size:15px;font-weight:400;color:#4a5c62;line-height:1.8;max-width:460px;margin-bottom:28px;letter-spacing:0}
.btn,.hero .btn,.reserve button{background:#167b99;border:0;color:#fff;padding:16px 25px;font:700 14px inherit;cursor:pointer;text-decoration:none;display:inline-block}
.quick{max-width:1180px;margin:-35px auto 0;position:relative;z-index:1;background:#fff;box-shadow:0 8px 30px #28616c1c;display:grid;grid-template-columns:repeat(4,1fr)}
.quick a{padding:26px;border-right:1px solid #e4eaeb;text-decoration:none;color:inherit;display:grid;grid-template-columns:40px 1fr;align-items:center}
.quick a:last-child{border:0}
.quick i{font-size:21px;color:#2184a0;font-style:normal;grid-row:span 2}
.quick span{font-size:14px;font-weight:700}
.quick small{font-size:11px;color:#849197;margin-top:5px}
section h2{font:600 clamp(27px,3.2vw,40px)/1.4 'Noto Serif KR',serif;letter-spacing:-.07em;margin:14px 0 12px}
.departments{padding:100px 12vw}
.departments .sub{font-size:14px;color:#66777b;margin-bottom:30px}
.tabs{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px}
.tabs button{border:1px solid #cbdadd;background:#fff;color:#3a4c52;padding:11px 18px;font:500 14px inherit;cursor:pointer;border-radius:2px}
.tabs button.on{background:#167b99;border-color:#167b99;color:#fff;font-weight:700}
.tab-panel{background:#f0f7f7;padding:40px}
.tab-panel h3{font:600 22px 'Noto Serif KR',serif;color:#167b99;margin-bottom:12px}
.tab-panel p{font-size:15px;line-height:1.8;color:#4a5c62}
.tab-panel ul{display:flex;flex-wrap:wrap;gap:10px;margin:20px 0}
.tab-panel li{list-style:none;background:#fff;border:1px solid #d7e5e7;padding:8px 16px;font-size:13px;border-radius:20px}
.tab-panel .doc{font-size:13px;color:#207e99;font-weight:700;margin-bottom:16px}
.link{color:#167b99;font-size:14px;font-weight:700;text-decoration:none}
.doctors{padding:90px 12vw;background:#edf6f7}
.doc-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:22px;margin-top:30px}
.doc-grid article{background:#fff;padding-bottom:22px;overflow:hidden}
.doc-grid img{width:100%;height:250px;object-fit:cover;display:block}
.doc-grid b{display:block;font-size:16px;margin:18px 22px 0}
.doc-grid span{display:block;color:#21819d;font-size:13px;font-weight:500;margin:5px 22px}
.doc-grid p{font-size:13px;line-height:1.7;color:#637276;margin:8px 22px 0}
.numbers{padding:90px 12vw;text-align:center;background:#167b99;color:#fff}
.numbers .label{color:#bfe2ea}
.numbers h2{color:#fff}
.stat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;margin-top:36px}
.stat-grid b{font:600 clamp(34px,4vw,52px) 'Noto Serif KR',serif;display:block}
.stat-grid em{font-size:17px;font-style:normal;font-weight:500;margin-left:4px}
.stat-grid span{font-size:14px;color:#cdeaf0;display:block;margin-top:8px}
.guide{padding:100px 12vw}
.guide-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:20px;margin-top:30px}
.guide-grid article{padding:30px 26px;background:#f6f8f8}
.guide-grid i{font-style:normal;font:700 20px 'Noto Serif KR',serif;color:#167b99}
.guide-grid b{display:block;font-size:17px;margin:14px 0 10px}
.guide-grid p{font-size:14px;line-height:1.9;color:#627176}
.hours{margin-top:26px;background:#f0f7f7;padding:30px 34px}
.hours>b{font-size:17px}
.hours table{width:100%;border-collapse:collapse;margin:16px 0 10px}
.hours th{text-align:left;font-weight:500;color:#3a4c52;padding:11px 0;border-bottom:1px solid #d7e5e7;width:40%}
.hours td{text-align:right;padding:11px 0;border-bottom:1px solid #d7e5e7;font-weight:700;color:#207e99}
.hours small{font-size:12px;color:#849197}
.reviews{padding:90px 12vw;background:#edf6f7}
.rev-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:20px;margin-top:30px}
.rev-grid article{background:#fff;padding:28px 26px}
.rev-grid .star{color:#f2b134;font-size:14px;letter-spacing:2px}
.rev-grid p{font-size:14px;line-height:1.8;color:#3a4c52;margin:12px 0 16px}
.rev-grid span{font-size:13px;color:#849197}
.location{padding:90px 12vw;display:grid;grid-template-columns:1fr 1fr;gap:50px;align-items:center}
.location .addr{font-size:15px;color:#207e99;font-weight:700;margin:12px 0 22px}
.location ul{margin-bottom:24px}
.location li{list-style:none;display:grid;grid-template-columns:90px 1fr;padding:13px 0;border-bottom:1px solid #e4eaeb;font-size:14px;color:#4a5c62}
.location li b{color:#167b99}
.location img{width:100%;height:340px;object-fit:cover}
.faq{padding:90px 12vw}
.faq-list{margin-top:30px;border-top:1px solid #cbdadd}
.faq article{border-bottom:1px solid #dfe8ea}
.faq button{width:100%;display:flex;justify-content:space-between;align-items:center;gap:16px;background:0;border:0;padding:22px 4px;font:500 16px inherit;color:#25343a;text-align:left;cursor:pointer}
.faq article.on button{color:#167b99;font-weight:700}
.faq button i{font-style:normal;font-size:22px;color:#167b99;flex-shrink:0}
.faq p{padding:0 4px 22px;font-size:14px;line-height:1.8;color:#627176}
.reserve{text-align:center;padding:90px 24px;background:#167b99;color:#fff}
.reserve p{font-size:11px;letter-spacing:.1em}
.reserve .lead{font-size:14px;letter-spacing:0;color:#cdeaf0;margin:14px 0 0;line-height:1.7}
.reserve button{margin-top:22px;background:#fff;color:#167b99}
footer{padding:44px 8vw;background:#253c44;color:#9fb4bc;font-size:12px}
footer>div{display:flex;align-items:baseline;gap:12px;margin-bottom:20px}
footer b{color:#fff;font:700 18px 'Noto Serif KR',serif}
footer dl{display:flex;flex-wrap:wrap;gap:8px 28px;margin-bottom:16px}
footer dl div{display:flex;gap:8px}
footer dt{color:#7c949d}
footer dd{color:#cbdade}
footer .copy{font-size:11px;color:#6f888f}
@media(max-width:860px){
  .doc-grid,.stat-grid{grid-template-columns:repeat(2,1fr)}
  .guide-grid,.rev-grid{grid-template-columns:1fr}
  .location{grid-template-columns:1fr;gap:30px}
  .location img{height:260px}
}
@media(max-width:680px){
  header{padding:0 24px}
  header nav{display:none}
  header button{display:block}
  .mobile{display:grid;gap:15px;padding:22px 24px;background:#eaf4f5}
  .mobile a{color:inherit;text-decoration:none}
  .hero{padding:0 24px;min-height:480px}
  .quick{margin:0;grid-template-columns:1fr 1fr}
  .quick a{padding:20px 16px}
  .quick a:nth-child(2){border-right:0}
  .quick a:nth-child(-n+2){border-bottom:1px solid #e4eaeb}
  .departments,.doctors,.numbers,.guide,.reviews,.location,.faq{padding:64px 24px}
  .tab-panel{padding:26px}
  .doc-grid,.stat-grid{grid-template-columns:1fr}
  .hours{padding:24px}
  footer{padding:36px 24px}
  footer dl{flex-direction:column;gap:6px}
}
</style>
