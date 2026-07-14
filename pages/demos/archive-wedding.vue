<template>
  <main class="archive">
    <!-- 상단 필름 인덱스 바 + 모바일 메뉴 -->
    <header class="topbar">
      <div class="topbar-in">
        <span class="mono index">ROLL 09 · 26</span>
        <span class="monogram">J&nbsp;+&nbsp;S</span>
        <button class="menu-btn" :aria-expanded="menu" aria-label="메뉴 열기" @click="menu = !menu">
          <span :class="{ open: menu }"></span>
        </button>
      </div>
      <nav :class="['drawer', { show: menu }]">
        <a href="#greeting" @click="menu = false">인사말</a>
        <a href="#info" @click="menu = false">예식 정보</a>
        <a href="#gallery" @click="menu = false">필름 갤러리</a>
        <a href="#way" @click="menu = false">오시는 길</a>
        <a href="#give" @click="menu = false">마음 전하기</a>
        <a href="#rsvp" @click="menu = false">참석 여부</a>
      </nav>
    </header>

    <!-- COVER / 표지 -->
    <section class="cover">
      <p class="mono top">OUR LITTLE WEDDING DAY</p>
      <div class="stamp">J + S<br>FOREVER</div>
      <div class="tape"></div>
      <div class="photo-frame">
        <!-- AI-IMG: 필름 스냅 웨딩, 해질녘 해변에서 마주 보는 신랑 신부, 그레인·세피아 아날로그 무드 · 4:3 -->
        <!-- prompt: analog film snapshot of a wedding couple facing each other at sunset beach, film grain, sepia tone, nostalgic archive mood, 4:3 -->
        <img
          src="https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&fit=crop&w=1200&q=85"
          alt="해질녘 해변에서 마주 보고 웃는 신랑과 신부">
      </div>
      <h1>just<br>married!</h1>
      <span class="mono when">2026. 09. 26 · HAEUNDAE</span>
    </section>

    <!-- 인사말 -->
    <section id="greeting" class="message reveal">
      <p class="hand">hey, friends!</p>
      <h2>우리, 결혼합니다.</h2>
      <p class="body">
        서로의 계절을 몇 번 지나며<br>
        이제는 같은 방향을 보게 되었습니다.<br><br>
        바다가 가까운 곳에서 좋아하는 사람들을 모시고<br>
        작지만 오래 기억될 하루를 열려고 해요.<br>
        한 장면 한 장면, 함께 채워 주세요.
      </p>
      <div class="names">
        <div><small>GROOM</small><b>정성호</b><span>정재만 · 이경희 의 장남</span></div>
        <div class="amp">&amp;</div>
        <div><small>BRIDE</small><b>김지수</b><span>김영수 · 박선영 의 장녀</span></div>
      </div>
      <div class="scribble">♡ see you there</div>
    </section>

    <!-- 예식 정보 + D-Day -->
    <section id="info" class="ticket-wrap reveal">
      <div class="ticket">
        <div class="ticket-head mono"><span>BOARDING PASS</span><span>NO. 0926</span></div>
        <strong>JISU<br>&amp; SEONGHO</strong>
        <div class="ticket-grid">
          <span class="mono">DATE<b>2026. 09. 26 (토)</b></span>
          <span class="mono">TIME<b>오후 2:00 PM</b></span>
          <span class="mono">PLACE<b>웨이브하우스, 해운대</b></span>
          <span class="mono">HALL<b>3F 오션 가든홀</b></span>
        </div>
        <div class="dday mono">
          <span>{{ ddayLabel }}</span>
          <small>2026년 9월 26일 토요일 오후 두 시</small>
        </div>
      </div>
    </section>

    <!-- 필름 갤러리 -->
    <section id="gallery" class="album reveal">
      <div class="album-head mono"><span>CAMERA ROLL</span><span>01 — {{ String(photos.length).padStart(2,'0') }}</span></div>
      <div class="film">
        <figure v-for="(p, i) in photos" :key="p.src" :class="['shot', `shot-${i % 3}`]">
          <!-- AI-IMG: 필름 스냅 웨딩, 그레인·세피아 아날로그 무드 · 4:3 -->
          <!-- prompt: analog film snapshot wedding scene, grain, sepia tone, nostalgic archive mood, 4:3 -->
          <img :src="p.src" :alt="p.alt">
          <figcaption class="mono">FRAME {{ String(i + 1).padStart(2, '0') }}</figcaption>
        </figure>
      </div>
      <p class="film-hint mono">→ 옆으로 넘겨 보세요 · 사진을 누르면 색이 살아나요</p>
    </section>

    <!-- 오시는 길 -->
    <section id="way" class="way reveal">
      <p class="hand light">how to get there</p>
      <h2>오시는 길</h2>
      <div class="place-photo">
        <!-- AI-IMG: 필름 스냅, 해운대 바닷가 예식장 외관, 그레인·세피아 아날로그 무드 · 4:3 -->
        <!-- prompt: analog film snapshot of a seaside wedding venue exterior in Haeundae, grain, sepia tone, nostalgic archive mood, 4:3 -->
        <img
          src="https://images.unsplash.com/photo-1520854221256-17451cc331bf?auto=format&fit=crop&w=1200&q=85"
          alt="바닷가에 자리한 예식장 외관">
      </div>
      <p class="addr">부산 해운대구 달맞이길 62번길 28<br>웨이브하우스 3F 오션 가든홀</p>
      <ul class="way-list">
        <li><b>지하철</b> 2호선 해운대역 7번 출구 → 무료 셔틀 7분 (7분 간격 운행)</li>
        <li><b>버스</b> 해운대해수욕장 정류장 하차 → 도보 6분</li>
        <li><b>자가용</b> 내비 '웨이브하우스 해운대' 검색 · 지하 2층 하객 주차 2시간 무료</li>
      </ul>
      <a class="way-link mono" href="https://www.openstreetmap.org/?mlat=35.1576&mlon=129.1742#map=17/35.1576/129.1742" target="_blank" rel="noopener">지도에서 길 찾기 ↗</a>
    </section>

    <!-- 마음 전하기 / 계좌 -->
    <section id="give" class="give reveal">
      <p class="hand">with love</p>
      <h2>마음 전하기</h2>
      <p class="give-lead">참석이 어려우신 분들을 위해 계좌를 안내드립니다.<br>따뜻한 마음, 소중히 간직하겠습니다.</p>
      <div class="accounts">
        <article v-for="(a, i) in accounts" :key="a.no">
          <div>
            <small>{{ a.side }}</small>
            <b>{{ a.name }}</b>
            <span class="mono">{{ a.bank }} {{ a.no }}</span>
          </div>
          <button class="mono" @click="copyAccount(a, i)">{{ copied === i ? '복사됨 ✓' : '복사' }}</button>
        </article>
      </div>
    </section>

    <!-- 참석 여부 (RSVP) -->
    <section id="rsvp" class="attend reveal">
      <p class="hand light">rsvp time</p>
      <h2>참석 여부 전하기</h2>
      <p class="attend-lead">따뜻한 하루를 준비할 수 있도록<br>참석 여부를 미리 알려 주세요.</p>

      <form v-if="!sent" class="rsvp-form" @submit.prevent="submit">
        <div class="choice">
          <button type="button" :class="{ picked: answer === 'yes' }" @click="answer = 'yes'">참석할게요</button>
          <button type="button" :class="{ picked: answer === 'no' }" @click="answer = 'no'">마음만 보낼게요</button>
        </div>
        <label>성함<input v-model="guest" type="text" placeholder="이름을 적어 주세요" required></label>
        <label>동행 인원<input v-model="count" type="number" min="1" max="10" placeholder="본인 포함 인원"></label>
        <label class="check"><input v-model="mealYes" type="checkbox"> 식사 함께합니다</label>
        <button type="submit" class="send mono">답장 보내기 →</button>
      </form>

      <div v-else class="rsvp-done">
        <span class="mono">RECEIVED · NO. {{ String(Math.floor(Math.random() * 900) + 100) }}</span>
        <p><b>{{ guest || '소중한 하객분' }}</b>님, 마음 잘 전해 받았어요.</p>
        <p class="sub">{{ answer === 'yes' ? '그날 반갑게 뵐게요. 조심히 오세요!' : '멀리서 보내 주신 마음, 오래 간직할게요.' }}</p>
        <button class="again mono" @click="sent = false">다시 작성</button>
      </div>
    </section>

    <!-- 안내 사항 -->
    <section class="notes reveal">
      <p class="hand">notes for the day</p>
      <article v-for="n in notes" :key="n.title">
        <span class="mono">{{ n.no }}</span>
        <div>
          <b>{{ n.title }}</b>
          <p>{{ n.text }}</p>
        </div>
      </article>
    </section>

    <footer>
      <p class="hand">thank you</p>
      <p class="mono">THANKS FOR BEING PART OF OUR STORY</p>
      <p class="mono small">JISU &amp; SEONGHO · 2026. 09. 26 · HAEUNDAE</p>
    </footer>
  </main>
</template>

<script setup lang="ts">
const menu = ref(false)
const answer = ref('yes')
const guest = ref('')
const count = ref('')
const mealYes = ref(true)
const sent = ref(false)
const copied = ref<number | null>(null)
const ddayLabel = ref('D-DAY 계산 중…')

const photos = [
  { src: 'https://images.unsplash.com/photo-1465495976277-4387d4b0b4c6?auto=format&fit=crop&w=1200&q=85', alt: '서로를 바라보며 웃는 신랑 신부의 필름 스냅' },
  { src: 'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=1200&q=85', alt: '손을 맞잡고 걷는 두 사람의 뒷모습' },
  { src: 'https://images.unsplash.com/photo-1583939003579-730e3918a45a?auto=format&fit=crop&w=1200&q=85', alt: '햇살 아래 마주 앉아 웃는 커플' },
  { src: 'https://images.unsplash.com/photo-1511285560929-80b456fea0bc?auto=format&fit=crop&w=1200&q=85', alt: '들꽃과 함께 차려진 예식 테이블' },
  { src: 'https://images.unsplash.com/photo-1537633552985-df8429e8048b?auto=format&fit=crop&w=1200&q=85', alt: '바닷가에서 손을 잡고 선 신랑 신부' },
]

const accounts = [
  { side: '신랑 정성호', name: '정성호', bank: '신한', no: '110-234-567890' },
  { side: '신랑 혼주 정재만', name: '정재만', bank: '국민', no: '012-01-0456789' },
  { side: '신부 김지수', name: '김지수', bank: '카카오뱅크', no: '3333-01-2345678' },
  { side: '신부 혼주 박선영', name: '박선영', bank: '농협', no: '302-1234-5678-91' },
]

const notes = [
  { no: '01', title: '옷차림은 편하게', text: '바람이 조금 부는 바닷가예요. 얇은 겉옷 한 장 챙기시면 좋아요.' },
  { no: '02', title: '사진은 마음껏', text: '플래시도, 필름 카메라도 환영이에요. 그날을 많이 남겨 주세요.' },
  { no: '03', title: '화환은 사양합니다', text: '마음만 감사히 받겠습니다. 화환 없이 편히 와 주세요.' },
  { no: '04', title: '식사와 셔틀', text: '예식 후 3층 가든홀에서 뷔페가 준비됩니다. 셔틀은 해운대역 7번 출구에서 운행해요.' },
]

async function copyAccount(a: { bank: string; no: string }, i: number) {
  try {
    await navigator.clipboard.writeText(`${a.bank} ${a.no}`)
    copied.value = i
    setTimeout(() => { if (copied.value === i) copied.value = null }, 1600)
  } catch {
    copied.value = i
  }
}

function submit() {
  sent.value = true
}

onMounted(() => {
  // D-Day: 클라이언트에서만 계산해 hydration 불일치 방지
  const target = new Date('2026-09-26T14:00:00+09:00').getTime()
  const today = new Date()
  const start = new Date(today.getFullYear(), today.getMonth(), today.getDate()).getTime()
  const diff = Math.round((target - start) / 86400000)
  ddayLabel.value = diff > 0 ? `D-${diff}` : diff === 0 ? 'D-DAY' : `D+${Math.abs(diff)}`

  // 스크롤 리빌 (SSR 안전)
  if (typeof window === 'undefined' || !('IntersectionObserver' in window)) {
    document.querySelectorAll('.reveal').forEach((el) => el.classList.add('in'))
    return
  }
  const io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (e.isIntersecting) {
        e.target.classList.add('in')
        io.unobserve(e.target)
      }
    })
  }, { threshold: 0.12 })
  document.querySelectorAll('.reveal').forEach((el) => io.observe(el))
})

useHead({ title: 'Jisu & Seongho | Archive Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Gowun+Dodum&family=Permanent+Marker&family=Space+Mono:wght@400;700&display=swap');

.archive{
  max-width:540px;margin:auto;overflow:hidden;color:#182e48;
  font-family:'Gowun Dodum',sans-serif;position:relative;
  background:#f4efe2;
  background-image:
    radial-gradient(#00000006 1px, transparent 1px),
    radial-gradient(#00000004 1px, transparent 1px);
  background-size:5px 5px, 9px 9px;
  background-position:0 0, 3px 3px;
}
.mono{font-family:'Space Mono',monospace;letter-spacing:.06em}

/* ── 상단 바 / 모바일 메뉴 ── */
.topbar{position:sticky;top:0;z-index:20;background:#f4efe2ee;backdrop-filter:blur(6px);border-bottom:1px solid #d8cdb4}
.topbar-in{display:flex;align-items:center;justify-content:space-between;padding:11px 18px}
.topbar .index{font-size:9px;color:#8a7e64}
.monogram{font:700 16px 'Space Mono',monospace;color:#182e48}
.menu-btn{width:34px;height:30px;background:none;border:0;cursor:pointer;display:grid;place-items:center;padding:0}
.menu-btn span,.menu-btn span::before,.menu-btn span::after{content:'';display:block;width:22px;height:2px;background:#182e48;transition:.25s;position:relative}
.menu-btn span::before{position:absolute;top:-7px}
.menu-btn span::after{position:absolute;top:7px}
.menu-btn span.open{background:transparent}
.menu-btn span.open::before{top:0;transform:rotate(45deg)}
.menu-btn span.open::after{top:0;transform:rotate(-45deg)}
.drawer{max-height:0;overflow:hidden;transition:max-height .3s ease;background:#182e48}
.drawer.show{max-height:340px}
.drawer a{display:block;padding:14px 20px;color:#f4efe2;text-decoration:none;font-size:14px;border-top:1px solid #ffffff14}

/* ── 표지 ── */
.cover{height:100svh;min-height:640px;background:#e8d8bb;position:relative;padding:22px;box-sizing:border-box;overflow:hidden}
.cover .top{position:absolute;z-index:2;top:20px;left:22px;font-size:10px;color:#5f5540}
.cover .when{position:absolute;z-index:2;bottom:26px;right:24px;font-size:10px;color:#5f5540}
.photo-frame{position:absolute;inset:70px 22px 66px;background:#f7f1e5;padding:10px 10px 34px;box-sizing:border-box;transform:rotate(-2.5deg);box-shadow:5px 9px 0 #bd7059}
.photo-frame img{width:100%;height:100%;object-fit:cover;filter:sepia(.45) contrast(1.03) brightness(1.02)}
.cover h1{position:absolute;z-index:2;bottom:58px;left:28px;margin:0;font:50px/.84 'Permanent Marker',cursive;color:#d84832;transform:rotate(-7deg);text-shadow:2px 2px 0 #f4efe2}
.stamp{position:absolute;z-index:3;top:74px;right:27px;border:2px solid #172f4b;border-radius:50%;width:62px;height:62px;display:grid;place-items:center;text-align:center;font:8px/1.3 'Space Mono',monospace;transform:rotate(13deg);opacity:.8}
.tape{position:absolute;z-index:2;top:60px;left:52%;width:96px;height:26px;background:#f5d389b8;transform:rotate(15deg);box-shadow:0 1px 2px #0000001a}

/* ── 공통 헤딩 ── */
.hand{font:22px 'Permanent Marker',cursive;margin:0 0 8px;color:#d84832;transform:rotate(-3deg)}
.hand.light{color:#f4efe2}
h2{font-size:30px;margin:0;line-height:1.15}

/* 스크롤 리빌 */
.reveal{opacity:0;transform:translateY(26px);transition:opacity .7s ease,transform .7s ease}
.reveal.in{opacity:1;transform:none}

/* ── 인사말 ── */
.message{padding:66px 27px 58px;text-align:center}
.message .body{font-size:14px;line-height:1.95;margin:22px 0 30px;color:#3a4658}
.names{display:flex;align-items:center;justify-content:center;gap:14px;margin:8px 0 22px}
.names div{display:grid;gap:3px}
.names small{font:9px 'Space Mono',monospace;color:#a08a63;letter-spacing:.1em}
.names b{font-size:19px}
.names span{font-size:11px;color:#67718290;color:#6b7280}
.names .amp{font:26px 'Permanent Marker',cursive;color:#d84832}
.scribble{font:18px 'Permanent Marker',cursive;color:#d84832}

/* ── 티켓 / 예식 정보 ── */
.ticket-wrap{padding:8px 18px 46px}
.ticket{background:#f9f7ee;border:2px dashed #d26048;padding:22px;position:relative;box-shadow:7px 7px 0 #92b4b2}
.ticket-head{display:flex;justify-content:space-between;font-size:9px}
.ticket strong{display:block;font:700 36px/.9 'Space Mono',monospace;margin:26px 0}
.ticket-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;border-top:1px solid #cfc7b4;padding:16px 0}
.ticket-grid span{display:grid;gap:3px;font-size:9px;color:#8a7e64}
.ticket-grid b{font-size:12px;color:#182e48}
.dday{border-top:1px solid #cfc7b4;padding-top:16px;text-align:center}
.dday span{display:block;font:700 30px 'Space Mono',monospace;color:#d84832}
.dday small{display:block;margin-top:6px;font-size:11px;color:#7a6f56;font-family:'Gowun Dodum',sans-serif}

/* ── 필름 갤러리 ── */
.album{padding:70px 0 40px;background:#1c334c;color:#f7efde}
.album-head{display:flex;justify-content:space-between;font-size:9px;padding:0 22px;margin-bottom:18px;color:#c7d2df}
.film{display:flex;gap:14px;overflow-x:auto;padding:0 22px 10px;scroll-snap-type:x mandatory}
.shot{flex:0 0 210px;background:#f5eee2;padding:9px 9px 30px;margin:0;color:#172f4b;scroll-snap-align:center;box-shadow:4px 6px 0 #00000030}
.shot-0{transform:rotate(-3deg)}
.shot-1{transform:rotate(3deg);margin-top:22px}
.shot-2{transform:rotate(-1deg)}
.shot img{display:block;width:100%;height:262px;object-fit:cover;filter:sepia(.5) contrast(1.05);transition:filter .5s ease}
.shot img:hover,.shot img:focus{filter:none}
.shot figcaption{margin-top:9px;font-size:9px;color:#3a4658}
.film-hint{padding:16px 22px 0;font-size:10px;color:#9fb0c1}

/* ── 오시는 길 ── */
.way{padding:64px 27px 58px;background:#95bdba;color:#132b40}
.place-photo{margin:18px 0 20px;background:#f7f1e5;padding:9px 9px 22px;transform:rotate(1.5deg);box-shadow:5px 6px 0 #ffffff55}
.place-photo img{width:100%;height:190px;object-fit:cover;filter:sepia(.35) contrast(1.03)}
.addr{font-size:14px;line-height:1.7;margin:0 0 18px;font-weight:600}
.way-list{list-style:none;padding:0;margin:0 0 20px;display:grid;gap:12px}
.way-list li{font-size:12.5px;line-height:1.6;padding-left:2px}
.way-list b{display:inline-block;margin-right:6px;color:#0f2233}
.way-link{display:inline-block;color:#0f2233;font-size:12px;text-decoration:none;border-bottom:2px solid;padding-bottom:4px;font-weight:700}

/* ── 마음 전하기 / 계좌 ── */
.give{padding:64px 27px 58px;text-align:center}
.give-lead{font-size:13px;line-height:1.8;color:#4b5666;margin:14px 0 26px}
.accounts{display:grid;gap:10px;text-align:left}
.accounts article{display:flex;align-items:center;justify-content:space-between;gap:10px;background:#f9f7ee;border:1px solid #e0d6bf;padding:14px 15px}
.accounts small{display:block;font:9px 'Space Mono',monospace;color:#a08a63;letter-spacing:.08em;margin-bottom:4px}
.accounts b{font-size:14px}
.accounts .mono{display:block;font-size:12px;color:#4b5666;margin-top:3px}
.accounts button{flex:0 0 auto;padding:9px 13px;font-size:10px;background:#182e48;color:#f4efe2;border:0;cursor:pointer;letter-spacing:.05em}

/* ── RSVP ── */
.attend{padding:62px 27px 58px;background:#182e48;color:#f4efe2}
.attend-lead{font-size:13px;line-height:1.8;color:#c7d2df;margin:14px 0 26px}
.rsvp-form{display:grid;gap:14px}
.choice{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.choice button{padding:15px 8px;border:1px solid #6d84a2;background:transparent;color:#f4efe2;font:13px 'Gowun Dodum',sans-serif;cursor:pointer;transition:.2s}
.choice .picked{background:#d84832;border-color:#d84832;color:#fff}
.rsvp-form label{display:grid;gap:6px;font-size:12px;color:#c7d2df;text-align:left}
.rsvp-form input[type=text],.rsvp-form input[type=number]{box-sizing:border-box;width:100%;padding:13px 14px;border:1px solid #6d84a2;background:#ffffff08;color:#f4efe2;font:13px 'Gowun Dodum',sans-serif}
.rsvp-form input::placeholder{color:#8a9cb3}
.check{flex-direction:row;align-items:center;display:flex;gap:9px}
.check input{width:16px;height:16px;accent-color:#d84832}
.send{margin-top:6px;padding:16px;background:#d84832;color:#fff;border:0;cursor:pointer;font-size:12px;letter-spacing:.06em}
.rsvp-done{text-align:center;padding:22px 6px}
.rsvp-done .mono{display:inline-block;font-size:9px;color:#9fb0c1;border:1px solid #40567215;background:#ffffff12;padding:6px 12px;margin-bottom:18px;letter-spacing:.1em}
.rsvp-done p{margin:8px 0;font-size:15px}
.rsvp-done .sub{font-size:13px;color:#c7d2df}
.again{margin-top:16px;background:none;border:1px solid #6d84a2;color:#c7d2df;padding:10px 18px;font-size:10px;cursor:pointer}

/* ── 안내 사항 ── */
.notes{padding:62px 27px 46px}
.notes article{display:grid;grid-template-columns:38px 1fr;gap:10px;border-top:1px dashed #c4bba4;padding:18px 0}
.notes article>span{font-size:11px;color:#d84832}
.notes b{font-size:14px}
.notes p{font-size:12.5px;line-height:1.7;margin:7px 0 0;color:#536174}

/* ── 푸터 ── */
footer{padding:44px 25px 40px;background:#e8d8bb;text-align:center}
footer .hand{margin-bottom:14px}
footer .mono{font-size:10px;color:#7a6f56;letter-spacing:.08em;margin:6px 0}
footer .small{font-size:9px;color:#9a8f74}

@media(min-width:541px){.archive{box-shadow:0 0 60px #0002}}
@media(prefers-reduced-motion:reduce){.reveal{transition:none}}
</style>
