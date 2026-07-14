<template>
  <main class="invite">
    <!-- 플로팅 퀵 내비게이션 (모바일 메뉴) -->
    <nav class="quicknav" :class="{ open: menu }">
      <ul v-show="menu">
        <li v-for="link in navLinks" :key="link.href"><a :href="link.href" @click="menu = false">{{ link.label }}</a></li>
      </ul>
      <button class="fab" :aria-expanded="menu" aria-label="빠른 이동 메뉴" @click="menu = !menu">{{ menu ? '×' : '☰' }}</button>
    </nav>

    <section class="hero">
      <!-- AI-IMG: 호텔 저녁 웨딩 홀 입구의 신랑 신부, 딥톤·샹들리에·따뜻한 조명 · 16:9 -->
      <!-- prompt: elegant hotel evening wedding, bride and groom at grand ballroom entrance, deep tones, chandeliers, warm golden lighting, 16:9 -->
      <img src="https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&amp;fit=crop&amp;w=1200&amp;q=85" alt="호텔 그랜드 볼룸 입구에 선 신랑 신부">
      <div class="hero-shade"></div>
      <div class="hero-title"><p>AN EVENING AT THE</p><h1>ST. MONT<br>SEOUL</h1><span>MINSEO &amp; JIWON · 07 NOV 2026</span></div>
      <button class="sound" @click="playing = !playing">{{ playing ? 'II' : '▶' }} <small>{{ playing ? 'MUSIC ON' : 'PLAY MUSIC' }}</small></button>
    </section>

    <section id="welcome" class="welcome"><p class="label">YOU ARE INVITED</p><h2>저녁이 가장 아름다운 시간,<br>우리의 시작에 초대합니다.</h2><p>깊어가는 가을밤, 가장 아끼는 분들과 식탁을 나누고 싶습니다. 편안한 마음으로 오셔서 두 사람의 첫 건배를 함께해 주세요.</p></section>

    <section class="event-card"><p class="label">THE OCCASION</p><div class="big-date"><span>NOV</span><strong>07</strong><span>2026<br>SAT</span></div><div class="event-line"><b>6:00 PM</b><span>St. Mont Seoul<br>Grand Ballroom, 3F</span></div><p class="dday">민서 ♥ 지원의 결혼식까지 <b>D-{{ dday }}</b></p><a href="#reply">RSVP NOW <i>→</i></a></section>

    <section class="schedule"><p class="label">YOUR EVENING</p><article v-for="item in schedule" :key="item.time"><span>{{ item.time }}</span><div><b>{{ item.title }}</b><p>{{ item.desc }}</p></div></article></section>

    <section id="gallery" class="gallery">
      <p class="label">MOMENTS</p>
      <div class="grid">
        <!-- AI-IMG: 호텔 저녁 웨딩 커플 포트레이트, 딥와인 톤·따뜻한 조명 · 3:4 -->
        <!-- prompt: evening wedding couple portrait in luxury hotel, deep wine tones, warm chandelier light, formal attire, 3:4 -->
        <img class="tall" src="https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&amp;fit=crop&amp;w=700&amp;q=85" alt="호텔 조명 아래 신랑 신부 포트레이트">
        <!-- AI-IMG: 세팅된 저녁 연회 테이블, 캔들·골드 커트러리 · 3:4 -->
        <!-- prompt: elegant set dinner reception table with candles and gold cutlery, deep tones, warm lighting, 3:4 -->
        <img src="https://images.unsplash.com/photo-1519225421980-715cb0215aed?auto=format&amp;fit=crop&amp;w=700&amp;q=85" alt="캔들이 놓인 저녁 연회 테이블">
        <!-- AI-IMG: 샹들리에가 빛나는 그랜드 볼룸 전경 · 16:9 -->
        <!-- prompt: grand ballroom interior with glowing chandeliers, deep warm tones, evening wedding setup, 16:9 -->
        <img class="wide" src="https://images.unsplash.com/photo-1470229722913-7c0e2dbbafd3?auto=format&amp;fit=crop&amp;w=1000&amp;q=85" alt="샹들리에가 빛나는 그랜드 볼룸 전경">
        <!-- AI-IMG: 신부 부케 클로즈업, 딥레드·아이보리 · 3:4 -->
        <!-- prompt: close-up of bridal bouquet, deep red and ivory roses, warm evening light, 3:4 -->
        <img src="https://images.unsplash.com/photo-1511285560929-80b456fea0bc?auto=format&amp;fit=crop&amp;w=700&amp;q=85" alt="딥레드와 아이보리 장미 부케 클로즈업">
        <!-- AI-IMG: 샴페인 건배 순간, 골드 하이라이트 · 3:4 -->
        <!-- prompt: champagne toast moment at evening wedding, golden highlights, deep background, 3:4 -->
        <img class="tall" src="https://images.unsplash.com/photo-1464366400600-7168b8af9bc3?auto=format&amp;fit=crop&amp;w=700&amp;q=85" alt="저녁 예식에서의 샴페인 건배 순간">
      </div>
    </section>

    <section class="dress"><p class="label">DRESS NOTE</p><h2>BLACK TIE<br><em>optional</em></h2><p>블랙, 아이보리, 와인 계열의 단정한 이브닝 룩을 권합니다. 편안하게, 그리고 오래 머물러 주세요.</p></section>

    <section id="location" class="location">
      <p class="label">GETTING HERE</p>
      <h2>St. Mont Seoul</h2>
      <p>서울 중구 소월로 68<br>그랜드 볼룸 3층</p>
      <ul class="floors">
        <li v-for="floor in floors" :key="floor.name"><b>{{ floor.level }}</b><span>{{ floor.name }}</span></li>
      </ul>
      <p class="valet">정문에서 발렛파킹을 무료로 제공합니다. 안내 데스크에 청첩장을 보여 주시면 지하 주차장 3시간 무료 등록도 도와드립니다.</p>
      <div class="directions"><a href="https://www.openstreetmap.org/?mlat=37.5570&amp;mlon=126.9755#map=17/37.5570/126.9755" target="_blank" rel="noopener">지도 보기 ↗</a><button @click="copy('address', '서울 중구 소월로 68 St. Mont Seoul')">{{ copied === 'address' ? '주소 복사됨' : '주소 복사' }}</button></div>
    </section>

    <section id="account" class="account">
      <p class="label">WITH THANKS</p>
      <h2>마음 전하실 곳</h2>
      <article v-for="acc in accounts" :key="acc.side">
        <div><span>{{ acc.side }}</span><b>{{ acc.holder }}</b></div>
        <p>{{ acc.bank }} {{ acc.number }}</p>
        <button @click="copy(acc.side, `${acc.bank} ${acc.number} ${acc.holder}`)">{{ copied === acc.side ? '복사됨' : '계좌 복사' }}</button>
      </article>
    </section>

    <section id="reply" class="reply">
      <p class="label">WILL YOU JOIN US?</p>
      <h2>함께해 주시나요?</h2>
      <div class="answer"><button :class="{ active: reply === 'yes' }" @click="reply = 'yes'">YES, WITH PLEASURE</button><button :class="{ active: reply === 'no' }" @click="reply = 'no'">SENDING LOVE</button></div>
      <input v-model="name" placeholder="성함">
      <select v-model="guests"><option v-for="n in 5" :key="n" :value="n">동반 인원 {{ n }}명</option></select>
      <button class="confirm" :disabled="sent" @click="sent = true">{{ sent ? 'RSVP CONFIRMED · 감사합니다' : 'CONFIRM RSVP' }}</button>
    </section>

    <section class="notice">
      <p class="label">GOOD TO KNOW</p>
      <h2>안내 사항</h2>
      <div class="faq" v-for="(item, i) in notices" :key="item.q">
        <button :aria-expanded="openFaq === i" @click="openFaq = openFaq === i ? -1 : i"><span>{{ item.q }}</span><i>{{ openFaq === i ? '−' : '+' }}</i></button>
        <p v-show="openFaq === i">{{ item.a }}</p>
      </div>
    </section>

    <footer>MINSEO ♥ JIWON</footer>
  </main>
</template>

<script setup lang="ts">
const playing = ref(false), menu = ref(false), reply = ref('yes'), name = ref(''), guests = ref(2), sent = ref(false), copied = ref(''), openFaq = ref(-1)

const dday = Math.max(0, Math.ceil((new Date(2026, 10, 7).getTime() - Date.now()) / 864e5))

const copy = (key: string, text: string) => {
  if (import.meta.client && navigator.clipboard) navigator.clipboard.writeText(text)
  copied.value = key
  setTimeout(() => { copied.value = '' }, 2000)
}

const navLinks = [
  { label: '인사말', href: '#welcome' },
  { label: '갤러리', href: '#gallery' },
  { label: '오시는 길', href: '#location' },
  { label: '마음 전하기', href: '#account' },
  { label: '참석 여부', href: '#reply' }
]
const schedule = [{ time: '17:30', title: 'WELCOME APERITIF', desc: '샴페인과 작은 인사' }, { time: '18:00', title: 'THE CEREMONY', desc: '두 사람의 약속' }, { time: '18:45', title: 'DINNER & TOASTS', desc: '착석 코스 디너와 축하' }]
const floors = [{ level: '1F', name: '정문 · 발렛파킹' }, { level: '3F', name: '그랜드 볼룸 · 신부 대기실' }, { level: '4F', name: '키즈 라운지' }, { level: 'B2', name: '지하 주차장' }]
const accounts = [{ side: '신랑측', holder: '김민서', bank: '하나은행', number: '287-910123-04567' }, { side: '신부측', holder: '이지원', bank: '신한은행', number: '110-482-905137' }]
const notices = [
  { q: '주차 안내', a: '정문 발렛파킹은 예식 하객에 한해 무료로 제공됩니다. 안내 데스크에 청첩장을 보여 주시면 지하 주차장 3시간 무료 등록도 가능합니다.' },
  { q: '식사 안내', a: '예식 후 같은 3층 그랜드 볼룸에서 착석 코스 디너가 제공됩니다. 알레르기나 식이 요청이 있으시면 RSVP 성함 옆에 남겨 주세요.' },
  { q: '화환 안내', a: '쾌적한 연회를 위해 화환은 정중히 사양합니다. 축하해 주시는 따뜻한 마음만 감사히 받겠습니다.' },
  { q: '아이 동반', a: '가족 단위 하객을 위해 4층에 키즈 라운지를 마련했습니다. 저녁 예식 특성상 편한 복장으로 오셔도 좋습니다.' }
]

useHead({ title: 'Minseo & Jiwon | Signature Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono&family=Manrope:wght@400;600;700&family=Playfair+Display:ital,wght@0,500;1,500&display=swap');
.invite{max-width:540px;margin:auto;background:#161514;color:#f3ede5;min-height:100vh;font-family:Manrope,sans-serif;position:relative}
.hero{height:100svh;min-height:650px;position:relative;overflow:hidden}.hero img{width:100%;height:100%;object-fit:cover}.hero-shade{position:absolute;inset:0;background:linear-gradient(180deg,#0a080533,transparent 45%,#090806cc)}.hero-title{position:absolute;left:25px;bottom:34px}.hero-title p,.label{margin:0 0 14px;font:10px 'DM Mono',monospace;letter-spacing:.16em;color:#c6a97f}.hero-title h1{margin:0 0 15px;font:500 clamp(52px,15vw,76px)/.83 'Playfair Display',serif;letter-spacing:-.07em}.hero-title span{font:10px 'DM Mono',monospace;letter-spacing:.07em}.sound{position:absolute;top:23px;right:20px;border:0;background:#ffffff20;border-radius:30px;color:#fff;padding:10px 12px;font:12px 'DM Mono',monospace;backdrop-filter:blur(8px);cursor:pointer}.sound small{font-size:9px;margin-left:4px}
.welcome,.schedule,.location,.gallery,.account,.notice{padding:68px 25px}.welcome h2,.reply h2,.location h2,.account h2,.notice h2{font:500 30px/1.24 'Playfair Display',serif;letter-spacing:-.04em;margin:0}.welcome>p:last-child,.dress>p:last-child,.location>p:nth-of-type(2){font-size:14px;line-height:1.9;color:#c8c0b7;margin:26px 0 0}
.event-card{margin:0 15px;padding:30px 22px;background:#31221d;border:1px solid #876b4a}.big-date{display:flex;align-items:center;gap:15px;padding:8px 0 25px;border-bottom:1px solid #886f50}.big-date strong{font:500 78px/.8 'Playfair Display',serif}.big-date span{font:10px/1.5 'DM Mono',monospace;color:#d4bd99}.event-line{display:flex;justify-content:space-between;align-items:center;padding:24px 0;font-size:13px;line-height:1.5}.event-line span{text-align:right;color:#ded3c5}.dday{text-align:center;font-size:12px;color:#e2cca8;letter-spacing:.04em;margin:0 0 20px;padding-bottom:20px;border-bottom:1px solid #886f50}.dday b{font:500 15px 'Playfair Display',serif;color:#f3ede5}.event-card a{display:flex;justify-content:space-between;color:#f3ede5;text-decoration:none;font:10px 'DM Mono',monospace;letter-spacing:.1em}.event-card i{font-style:normal;font-size:17px}
.schedule article{display:grid;grid-template-columns:78px 1fr;gap:13px;padding:18px 0;border-top:1px solid #373432}.schedule article>span{font:10px 'DM Mono',monospace;color:#c6a97f}.schedule b{font-size:13px}.schedule p{font-size:12px;color:#aaa39b;margin:7px 0 0}
.gallery .grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:24px}.gallery img{width:100%;height:100%;aspect-ratio:3/4;object-fit:cover;display:block}.gallery img.wide{grid-column:1/-1;aspect-ratio:16/9}
.dress{padding:65px 25px;background:#e8dccb;color:#261d18}.dress .label{color:#8d6243}.dress h2{font:500 50px/.86 'Playfair Display',serif;margin:0}.dress h2 em{font-size:32px}.dress>p:last-child{color:#59493d}
.location .floors{list-style:none;padding:0;margin:28px 0 0;border-top:1px solid #373432}.location .floors li{display:flex;gap:16px;align-items:center;padding:13px 0;border-bottom:1px solid #2a2826;font-size:13px}.location .floors b{font:10px 'DM Mono',monospace;color:#c6a97f;min-width:32px}.location .floors span{color:#ded3c5}.location .valet{font-size:13px;line-height:1.8;color:#a49c93;margin:20px 0 0}.directions{display:flex;gap:9px;margin-top:25px}.directions>*{flex:1;text-align:center;padding:14px 4px;border:1px solid #777069;background:transparent;color:inherit;text-decoration:none;font:11px Manrope,sans-serif}.directions button{cursor:pointer}
.account{background:#201f1e}.account article{margin-top:16px;padding:20px;background:#2a2826;border:1px solid #3a3734}.account article div{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:8px}.account article span{font:10px 'DM Mono',monospace;letter-spacing:.1em;color:#c6a97f}.account article b{font:500 17px 'Playfair Display',serif}.account article p{font-size:13px;color:#ded3c5;letter-spacing:.02em}.account button{margin-top:14px;width:100%;padding:11px;border:1px solid #6c5a44;background:transparent;color:#e2cca8;font:10px 'DM Mono',monospace;letter-spacing:.08em;cursor:pointer}
.reply{padding:66px 25px;background:#711d1c}.reply .label{color:#ebbaa5}.reply h2{font-size:35px}.answer{display:grid;gap:8px;margin:27px 0 10px}.answer button,.reply input,.reply select,.confirm{box-sizing:border-box;width:100%;padding:16px;border:1px solid #ffffff77;background:transparent;color:#fff;font:11px 'DM Mono',monospace;letter-spacing:.05em}.answer button,.confirm,.reply select{cursor:pointer}.answer .active{background:#f4e9db;color:#3a1918}.reply input,.reply select{font-family:Manrope,sans-serif;letter-spacing:0;margin-bottom:10px}.reply input::placeholder{color:#f4cfc5}.reply select option{color:#161514}.confirm{border:0;background:#191313}.confirm:disabled{background:#3a1918;color:#f4cfc5;cursor:default}
.notice .faq{border-top:1px solid #373432}.notice .faq:last-child{border-bottom:1px solid #373432}.notice .faq button{width:100%;display:flex;justify-content:space-between;align-items:center;padding:19px 2px;background:transparent;border:0;color:#f3ede5;font:13px Manrope,sans-serif;cursor:pointer;text-align:left}.notice .faq i{font-style:normal;font-size:18px;color:#c6a97f}.notice .faq p{font-size:13px;line-height:1.85;color:#aaa39b;margin:0;padding:0 2px 20px}
.quicknav{position:fixed;bottom:24px;right:24px;z-index:20;display:flex;flex-direction:column;align-items:flex-end;gap:10px}.quicknav ul{list-style:none;margin:0;padding:10px;background:#221c19f2;border:1px solid #6c5a44;border-radius:14px;backdrop-filter:blur(8px);display:grid;gap:2px}.quicknav li a{display:block;padding:9px 16px;color:#f3ede5;text-decoration:none;font:11px 'DM Mono',monospace;letter-spacing:.06em;border-radius:8px}.quicknav li a:hover{background:#ffffff14;color:#e2cca8}.fab{width:52px;height:52px;border-radius:50%;border:1px solid #6c5a44;background:#31221d;color:#f3ede5;font-size:20px;cursor:pointer;box-shadow:0 8px 24px #0009}
footer{text-align:center;padding:26px;font:10px 'DM Mono',monospace;letter-spacing:.15em;color:#c6a97f}
@media(min-width:541px){.invite{box-shadow:0 0 60px #0008}.quicknav{right:calc(50% - 246px)}}
</style>
