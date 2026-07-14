<template>
  <main class="dental"><header><a class="logo" href="#top">바른<span>치과</span></a><nav><a href="#treatment">진료안내</a><a href="#doctor">의료진소개</a><a href="#trust">병원소개</a><a href="#guide">오시는 길</a><a href="#faq">자주 묻는 질문</a><a href="#reserve">상담예약</a></nav><button @click="open=!open">{{ open?'닫기':'메뉴' }}</button></header><nav v-if="open" class="mobile"><a href="#treatment" @click="open=false">진료안내</a><a href="#doctor" @click="open=false">의료진소개</a><a href="#trust" @click="open=false">병원소개</a><a href="#guide" @click="open=false">오시는 길</a><a href="#faq" @click="open=false">자주 묻는 질문</a><a href="#reserve" @click="open=false">상담예약</a></nav>
    <section id="top" class="hero"><div><p>BAREUN DENTAL CLINIC</p><h1>편안하게,<br><b>오래 웃을 수 있도록.</b></h1><span>과잉 진료 없이, 꼭 필요한 치료만 정직하게 안내합니다.<br>발산역 도보 2분 · 평일 야간진료 · 편안한 상담부터 시작하세요.</span><a href="#reserve">상담 예약하기</a></div>
      <!-- AI-IMG: 밝고 청결한 치과 진료실, 따뜻한 우드톤 · 4:3 -->
      <!-- prompt: bright clean dental clinic interior, warm wood tones, welcoming, natural light, 4:3 -->
      <img src="https://images.unsplash.com/photo-1629909613654-28e377c37b09?auto=format&fit=crop&w=1200&q=85" alt="바른치과의 밝고 청결한 진료실 내부 전경"></section>
    <section class="notice"><b>진료 안내</b><span>평일 야간진료 월·수 20:00까지 · 토요일 14:00까지 · 주차 가능</span><a href="#guide">자세히 보기 →</a></section>
    <section id="treatment" class="treatment"><p class="label">TREATMENT</p><h2>바른치과 진료 안내</h2><p class="lead">각 진료의 방법과 소요 기간, 주의사항까지 미리 안내해 드립니다. 치료 전 충분히 확인하세요.</p>
      <div><article v-for="item in treatments" :key="item.title"><span>{{ item.no }}</span><h3>{{ item.title }}</h3><p class="desc">{{ item.text }}</p><dl><dt>소요 기간</dt><dd>{{ item.duration }}</dd><dt>주의사항</dt><dd>{{ item.caution }}</dd></dl><a href="#reserve">상담하기 →</a></article></div></section>
    <section class="why"><div><p class="label">WHY BAREUN</p><h2>치료 전,<br>충분히 설명합니다.</h2><p>진단 결과와 치료 방법을 직접 보고 이해할 수 있도록 안내합니다.</p></div><article v-for="item in reasons" :key="item.no"><span>{{ item.no }}</span><b>{{ item.title }}</b><p>{{ item.text }}</p></article></section>
    <section id="doctor" class="doctor">
      <!-- AI-IMG: 흰 가운을 입은 치과 의사의 신뢰감 있는 정면 인물 사진 · 세로 3:4 -->
      <!-- prompt: friendly dentist in white coat, warm confident portrait, clinic background, soft light, 3:4 -->
      <img src="https://images.unsplash.com/photo-1612349317150-e413f6a5b16d?auto=format&fit=crop&w=900&q=85" alt="이바른 대표원장의 진료 모습">
      <div><p class="label">DOCTOR</p><h2>환자의 이야기를<br>먼저 듣겠습니다.</h2><b>이바른 대표원장</b><span>치과보존과 전문의 · 대한치과보존학회 정회원</span><p>치료의 필요와 과정, 선택지를 충분히 설명드린 뒤 함께 결정합니다. 내 가족에게 권할 수 있는 진료를 기준으로 합니다.</p><a href="#reserve">의료진 소개 →</a></div></section>
    <section id="trust" class="trust numbers"><p class="label">WITH YOU</p><h2>숫자로 보는 바른치과</h2><div><article v-for="n in stats" :key="n.label"><b>{{ n.prefix }}{{ n.display }}{{ n.suffix }}</b><span>{{ n.label }}</span></article></div></section>
    <section id="review" class="review"><p class="label">PATIENT REVIEW</p><h2>환자분들의 이야기</h2><div><figure v-for="r in reviews" :key="r.name"><p class="stars" aria-label="별점 5점">★★★★★</p><blockquote>{{ r.text }}</blockquote><figcaption>{{ r.name }} · {{ r.treat }}</figcaption></figure></div><small>* 실제 내원 환자분들의 동의를 받아 익명으로 게재한 후기입니다.</small></section>
    <section id="guide" class="guide"><div><p class="label">VISIT US</p><h2>오시는 길</h2><p>서울 강서구 공항대로 00, 3층<br>발산역 5번 출구 도보 2분</p><ul><li>지하철 · 5호선 발산역 5번 출구에서 도보 2분</li><li>버스 · 마곡동세일교회 정류장 하차 후 도보 3분</li><li>주차 · 건물 지하 주차장 이용, 진료 시 2시간 무료</li></ul><a href="#reserve">네이버 지도 보기 ↗</a></div><div><p class="label">OPENING HOURS</p><h2>진료 시간</h2><table><tbody><tr v-for="h in hours" :key="h.day"><th>{{ h.day }}</th><td>{{ h.time }}</td></tr></tbody></table><span>점심시간 13:00 - 14:00 · 일요일·공휴일 휴진</span></div></section>
    <section id="faq" class="faq"><p class="label">FAQ</p><h2>자주 묻는 질문</h2><div><article v-for="(f,i) in faqs" :key="i"><button :aria-expanded="openFaq===i" @click="openFaq=openFaq===i?-1:i"><span>Q. {{ f.q }}</span><i>{{ openFaq===i?'−':'+' }}</i></button><p v-show="openFaq===i">{{ f.a }}</p></article></div></section>
    <section id="reserve" class="reserve"><p>ONLINE CONSULTATION</p><h2>처음이라도 편하게<br>문의해 주세요.</h2><form v-if="!sent" @submit.prevent="submit"><input v-model.trim="form.name" type="text" placeholder="성함" required><input v-model.trim="form.phone" type="tel" placeholder="연락처" required><input v-model.trim="form.memo" type="text" placeholder="상담 희망 내용 (예: 임플란트 상담)"><button type="submit" :disabled="!form.name.trim()">간편 상담 신청하기 →</button></form><p v-else class="done">{{ form.name }}님, 상담 신청이 접수되었습니다.<br><span v-if="form.memo">희망 내용 · {{ form.memo }}<br></span>연락처 {{ form.phone }}로 순차적으로 연락드리겠습니다.</p><small>대표전화 02. 0000. 0000 · 상담 시간 평일 10:00 - 19:00</small></section>
    <footer><b>바른치과의원</b><span>대표원장 이바른 · 사업자등록번호 000-00-00000</span><span>서울 강서구 공항대로 00, 3층 · 대표전화 02.0000.0000</span><span>© BAREUN DENTAL CLINIC. All rights reserved.</span></footer></main>
</template>
<script setup lang="ts">
const open=ref(false),sent=ref(false),openFaq=ref(-1)
const form=reactive({name:'',phone:'',memo:''})
const submit=()=>{if(!form.name.trim())return;sent.value=true}
const treatments=[
  {no:'01',title:'일반 진료',text:'충치·잇몸 치료부터 정기 검진까지 구강 건강의 기본을 살핍니다.',duration:'1~3회 내원',caution:'치료 후 하루 정도 시린 증상이 있을 수 있습니다.'},
  {no:'02',title:'임플란트',text:'정밀 진단을 바탕으로 뼈 상태에 맞춰 진행하는 맞춤 치료입니다.',duration:'약 3~6개월 (뼈이식 필요 시 연장)',caution:'수술 후 부기가 있을 수 있어 정기 내원이 필요합니다.'},
  {no:'03',title:'교정 치료',text:'치아와 얼굴 균형을 함께 고려해 계획하는 교정 치료입니다.',duration:'약 18~30개월',caution:'주기적 조정과 구강 위생 관리가 결과를 좌우합니다.'},
  {no:'04',title:'심미 치료',text:'자연스러운 미소를 위한 라미네이트·보철·미백 치료입니다.',duration:'2~4회 내원',caution:'미백 후 일시적으로 이가 시릴 수 있습니다.'}
]
const reasons=[
  {no:'01',title:'정밀 진단',text:'3D CT와 구강 스캐너로 필요한 부분을 확인합니다.'},
  {no:'02',title:'단계별 안내',text:'치료 기간과 비용을 먼저 설명드리고 시작합니다.'},
  {no:'03',title:'사후 관리',text:'치료 후 정기 검진까지 책임 있게 이어갑니다.'}
]
const stats=reactive([
  {label:'년 개원 이래 한자리에서',target:14,prefix:'',suffix:'년',display:0},
  {label:'누적 진료 환자 수',target:32000,prefix:'',suffix:'명+',display:0},
  {label:'환자 재방문율',target:92,prefix:'',suffix:'%',display:0},
  {label:'누적 방문 후기',target:480,prefix:'',suffix:'건+',display:0}
])
const reviews=[
  {name:'김○○님',treat:'임플란트',text:'치료 전에 뼈 상태와 기간을 그림으로 하나하나 설명해 주셔서 불안했던 마음이 놓였어요. 과하게 권하지 않아 믿음이 갑니다.'},
  {name:'박○○님',treat:'충치 치료',text:'아이가 치과를 무서워했는데 원장님이 천천히 설명해 주시니 스스로 입을 벌리더라고요. 야간진료가 있어 퇴근 후 오기도 편했습니다.'},
  {name:'이○○님',treat:'치아 교정',text:'교정 상담부터 비용 안내가 투명해서 좋았습니다. 정기 조정 때마다 진행 상황을 사진으로 보여주셔서 믿고 맡겼어요.'}
]
const hours=[
  {day:'월·수요일',time:'10:00 - 20:00 (야간)'},
  {day:'화·목·금요일',time:'10:00 - 19:00'},
  {day:'토요일',time:'10:00 - 14:00'},
  {day:'일요일·공휴일',time:'휴진'}
]
const faqs=[
  {q:'진료비는 어떻게 되나요?',a:'검진과 상담 후 치료 계획과 함께 예상 비용을 먼저 안내해 드립니다. 동의하신 뒤에 치료를 시작하므로 예상치 못한 비용은 없습니다.'},
  {q:'건강보험이 적용되나요?',a:'충치·잇몸 치료, 만 65세 이상 임플란트·틀니 등 급여 항목은 건강보험이 적용됩니다. 심미 치료 등 비급여 항목은 상담 시 별도로 안내드립니다.'},
  {q:'치료가 많이 아픈가요?',a:'표면 마취 후 최소한의 자극으로 진행하며, 통증에 민감한 분은 미리 말씀해 주시면 속도를 조절합니다. 치료 중에도 손을 들어 언제든 멈출 수 있습니다.'},
  {q:'야간이나 주말에도 진료하나요?',a:'월·수요일은 20:00까지 야간진료, 토요일은 14:00까지 진료합니다. 직장인·학생분들도 부담 없이 방문하실 수 있습니다.'},
  {q:'주차가 가능한가요?',a:'건물 지하 주차장을 이용하실 수 있으며, 진료 시 2시간 무료 주차를 지원합니다. 발산역 5번 출구에서 도보 2분 거리입니다.'}
]
onMounted(()=>{
  const el=document.querySelector('.numbers')
  if(!el)return
  const io=new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(!e.isIntersecting)return
      stats.forEach(s=>{
        const step=Math.max(1,Math.ceil(s.target/60))
        const t=setInterval(()=>{
          const next=s.display+step
          if(next>=s.target){s.display=s.target;clearInterval(t)}
          else s.display=next
        },24)
      })
      io.disconnect()
    })
  },{threshold:.4})
  io.observe(el)
})
useHead({title:'바른치과 | 동네 치과'})
definePageMeta({layout:false})
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Gowun+Batang:wght@400;700&family=Gowun+Dodum&display=swap');
.dental{font-family:'Gowun Dodum',sans-serif;color:#45413e;background:#fffdf9;min-height:100vh}header{height:78px;padding:0 8vw;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #e9e2d9;position:sticky;top:0;background:#fffdf9;z-index:20}.logo{font:700 23px 'Gowun Batang',serif;color:#a86d4a;text-decoration:none}.logo span{color:#45413e;margin-left:2px}header nav{display:flex;gap:26px}header nav a{color:inherit;text-decoration:none;font-size:14px}header button{display:none;border:0;background:none;font:14px inherit}.mobile{display:none}.hero{display:grid;grid-template-columns:1fr 1fr;min-height:540px;background:#f6eee4}.hero>div{padding:9vw 8vw;display:flex;flex-direction:column;justify-content:center}.hero p,.label{margin:0;color:#aa7254;font-size:11px;font-weight:700;letter-spacing:.08em}.hero h1{font:400 clamp(37px,4.7vw,59px)/1.3 'Gowun Batang',serif;letter-spacing:-.09em;margin:20px 0}.hero h1 b{color:#ad7251}.hero span{font-size:14px;line-height:1.8}.hero a{margin-top:30px;width:max-content;padding:14px 23px;background:#a96f4e;color:#fff;text-decoration:none;font-size:14px}.hero>img{width:100%;height:100%;object-fit:cover}.notice{padding:21px 8vw;display:flex;gap:30px;align-items:center;background:#a96f4e;color:#fff;font-size:13px}.notice a{margin-left:auto;color:inherit;text-decoration:none;font-size:12px}.treatment{padding:105px 8vw}.treatment h2,.doctor h2,.guide h2,.reserve h2,.why h2,.trust h2,.review h2,.faq h2{font:400 clamp(27px,3vw,40px) 'Gowun Batang',serif;letter-spacing:-.08em;margin:15px 0 35px}.lead{font-size:14px;line-height:1.8;color:#766f68;margin:-18px 0 35px;max-width:640px}.treatment>div{display:grid;grid-template-columns:repeat(4,1fr);border-top:1px solid #ddd3c8}.treatment article{padding:24px 17px 25px 0;border-bottom:1px solid #ddd3c8;display:flex;flex-direction:column}.treatment span{font-size:11px;color:#ae7654}.treatment h3{font-size:17px;margin:30px 0 10px}.treatment .desc{font-size:13px;line-height:1.7;color:#766f68;min-height:66px}.treatment dl{margin:8px 0 16px;font-size:12px}.treatment dt{color:#ae7654;margin-top:9px}.treatment dd{margin:2px 0 0;line-height:1.6;color:#6e6760}.treatment a,.doctor a,.guide a{font-size:12px;color:#9d684c;text-decoration:none;margin-top:auto}.why{padding:90px 8vw;background:#f8f4ed;display:grid;grid-template-columns:1.3fr repeat(3,1fr);gap:28px}.why>div>p:last-child{font-size:13px;line-height:1.8;color:#766f68}.why article{border-left:1px solid #ded3c5;padding-left:20px}.why article span{font-size:11px;color:#ad7251}.why article b{display:block;margin:28px 0 10px;font:700 17px 'Gowun Batang',serif}.why article p{font-size:13px;line-height:1.7;color:#766f68}.doctor{display:grid;grid-template-columns:1fr 1fr;background:#f4ebe0}.doctor>img{width:100%;height:100%;min-height:510px;object-fit:cover}.doctor>div{padding:9vw 10vw;display:flex;flex-direction:column;align-items:start;justify-content:center}.doctor h2{line-height:1.4}.doctor b{font-size:17px}.doctor>div>span{font-size:13px;color:#ae7654;margin-top:7px}.doctor>div>p:last-of-type{font-size:14px;line-height:1.9;color:#706760;margin:25px 0}.trust{padding:90px 8vw;text-align:center}.trust>div{display:grid;grid-template-columns:repeat(4,1fr);gap:24px;margin-top:10px}.trust article{padding:28px 12px;border:1px solid #e6ddd0;background:#faf5ee}.trust b{display:block;font:400 clamp(28px,3.4vw,42px) 'Gowun Batang',serif;color:#a96f4e}.trust span{display:block;margin-top:12px;font-size:12px;line-height:1.6;color:#766f68}.review{padding:95px 8vw;background:#f8f4ed;text-align:center}.review>div{display:grid;grid-template-columns:repeat(3,1fr);gap:24px;text-align:left}.review figure{margin:0;padding:30px 26px;background:#fffdf9;border:1px solid #e6ddd0}.review .stars{margin:0;color:#c99a5a;font-size:15px;letter-spacing:2px}.review blockquote{margin:16px 0;font-size:13.5px;line-height:1.9;color:#5f5952}.review figcaption{font-size:12px;color:#ae7654}.review small{display:block;margin-top:26px;font-size:11px;color:#9b938b}.guide{display:grid;grid-template-columns:1fr 1fr;padding:85px 8vw;gap:50px}.guide>div{border-top:1px solid #d9cfc2;padding-top:20px}.guide h2{margin:14px 0}.guide>div>p{font-size:14px;line-height:2;color:#6e6964}.guide ul{margin:18px 0 0;padding:0;list-style:none;font-size:13px;line-height:1.9;color:#6e6964}.guide ul li{padding-left:14px;position:relative}.guide ul li::before{content:'·';position:absolute;left:2px;color:#ae7654}.guide table{width:100%;border-collapse:collapse;margin-top:6px;font-size:14px}.guide th,.guide td{text-align:left;padding:11px 0;border-bottom:1px solid #ece4d9}.guide th{width:42%;color:#8a5f43;font-weight:400}.guide td{color:#6e6964}.guide span{display:block;margin-top:14px;font-size:12px;color:#9b938b}.faq{padding:95px 8vw;max-width:900px;margin:0 auto}.faq article{border-bottom:1px solid #e2d9cd}.faq button{width:100%;display:flex;align-items:center;justify-content:space-between;gap:16px;padding:22px 2px;background:none;border:0;cursor:pointer;text-align:left;font:15px 'Gowun Dodum',sans-serif;color:#45413e}.faq button span{font-weight:400}.faq i{font-style:normal;font-size:22px;color:#a96f4e;line-height:1}.faq p{margin:0 2px 24px;font-size:13.5px;line-height:1.9;color:#6e6760}.reserve{padding:90px 24px;text-align:center;background:#a96f4e;color:#fff}.reserve p{font-size:11px;letter-spacing:.1em}.reserve h2{line-height:1.4}.reserve form{display:flex;flex-direction:column;gap:12px;max-width:400px;margin:0 auto}.reserve input{padding:14px 16px;border:0;font:14px 'Gowun Dodum',sans-serif;background:#fff;color:#45413e}.reserve button{border:0;background:#403e3b;color:#fff;padding:16px 28px;font:700 14px inherit;cursor:pointer;margin-top:4px}.reserve button:disabled{opacity:.45;cursor:not-allowed}.reserve .done{font-size:15px;line-height:1.9;background:#fff;color:#935f43;max-width:400px;margin:0 auto;padding:26px 20px}.reserve small{display:block;margin-top:19px;color:#f7ddd0;font-size:12px}footer{padding:30px 8vw;background:#403e3b;color:#d7d0c8;display:flex;flex-direction:column;gap:7px;font-size:11px;line-height:1.7}footer b{color:#fff;font:700 14px 'Gowun Batang',serif;margin-bottom:4px}@media(max-width:650px){header{padding:0 24px}header nav{display:none}header button{display:block}.mobile{display:grid;gap:15px;padding:22px 24px;background:#f6eee4}.mobile a{color:inherit;text-decoration:none}.hero{grid-template-columns:1fr}.hero>div{padding:75px 24px 55px}.hero>img{height:330px}.notice{padding:18px 24px;display:grid;gap:5px}.notice a{margin-left:0}.treatment{padding:75px 24px}.treatment>div{grid-template-columns:1fr}.treatment .desc{min-height:0}.why{padding:70px 24px;grid-template-columns:1fr;gap:0}.why article{padding:20px 0;border-top:1px solid #ded3c5;border-left:0}.why article b{margin:10px 0}.doctor{grid-template-columns:1fr}.doctor>img{height:380px;min-height:0}.doctor>div{padding:75px 24px}.trust{padding:70px 24px}.trust>div{grid-template-columns:1fr 1fr;gap:14px}.review{padding:70px 24px}.review>div{grid-template-columns:1fr;gap:16px}.guide{grid-template-columns:1fr;padding:70px 24px;gap:35px}.faq{padding:70px 24px}.reserve{padding:70px 24px}footer{padding:26px 24px}}
</style>
