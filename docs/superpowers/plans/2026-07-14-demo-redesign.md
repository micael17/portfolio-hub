# 데모 사이트 재설계 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** portfolio-hub 의 데모 19개를 실제 서비스처럼 보이도록 콘텐츠·섹션 밀도와 가벼운 인터랙션을 강화하고, 세트 전체가 대중적↔스타일리쉬 스펙트럼을 고르게 커버하게 만든다.

**Architecture:** 각 데모는 `pages/demos/<name>.vue` 단일 파일(`definePageMeta({layout:false})`) 유지. 데모별 기존 시각 아이덴티티를 보존하면서, 공통 블루프린트(섹션 밀도 + 가벼운 인터랙션 + 이미지 주석 마커)에 맞춰 확장한다. 공통 컴포넌트 추출은 하지 않는다(다양성 유지). 카테고리별 4개 배치로 진행하고 배치 종료 시 사용자 확인.

**Tech Stack:** Nuxt 3, Vue 3 `<script setup>`, scoped CSS. 빌드/검증은 `pnpm`.

---

## 도메인 적응 (이 계획서의 태스크 형식)

이 작업은 정적 디자인/콘텐츠 작업이라 표준 TDD(유닛테스트 red→green)가 적합하지 않다. 따라서:

- 각 태스크는 **완전한 콘텐츠 스펙**을 담는다: 정확한 섹션 목록, 채울 데이터 필드와 현실적 샘플 값, 인터랙션 동작, 이미지 마커 목록. (placeholder "적당히 채움" 금지)
- 실행자는 **먼저 해당 `.vue` 파일을 읽고** 기존 스타일(폰트·컬러·레이아웃 언어)을 파악한 뒤, 그 언어를 유지하며 스펙대로 확장한다.
- 검증(verify) = ① `pnpm build` 로 전체 SFC 컴파일 통과 ② 스펙 섹션 체크리스트 충족 ③ 배치당 최소 1개 데모를 dev 서버로 실제 렌더 확인.

## 공통 블루프린트 (모든 데모 공통 기준)

콘텐츠:
- placeholder식 짧은 문구 제거 → 현실적 카피·가격·수치·기간·주의사항·후기(가상이되 그럴듯)
- 숫자 기반 신뢰지표 포함 (누적 건수/만족도/운영 연차 등)

섹션 밀도 (타입별 가감): Hero → 핵심가치 3~4 → 상세 서비스/상품 → 실적·신뢰지표 → 후기/사례 → FAQ → CTA/문의 → 푸터(사업자정보 형식: 상호·주소·전화·사업자번호 형식 문구)

가벼운 인터랙션 (데모당 1~2개): 탭 전환 / 아코디언 FAQ / 폼 제출 상태 토글 / 스크롤 리빌 / 카운트업 / 갤러리 필터. 무거운 라우팅 없음.

반응형·접근성: 모바일 메뉴 유지, 모든 `<img>` 에 의미있는 `alt`, 명도 대비 확보.

이미지 마커 (주석만, `src` 는 기존 URL 유지):
```html
<!-- AI-IMG: [주제] · [스타일/무드] · [비율] -->
<!-- prompt: (GPT 이미지 생성용 영문 프롬프트) -->
<img src="(기존 Unsplash URL 유지)" alt="..." >
```

스타일 지점: 각 태스크 상단에 명시된 지점(대중형/중간/스타일리쉬)에 커밋. 대중형은 더 정돈된 검증 UX, 스타일리쉬형은 시그니처 표현 강화(단 정보 접근성 유지).

## 공통 인터랙션 구현 레시피 (재사용, 컴포넌트화는 안 함)

각 데모에 필요 시 아래 패턴을 인라인으로 복제해 쓴다. 스타일 클래스명은 데모별로 맞춘다.

**아코디언 FAQ**
```vue
<!-- template -->
<section class="faq">
  <h2>자주 묻는 질문</h2>
  <div v-for="(f,i) in faqs" :key="i" class="faq-item" :class="{open: openFaq===i}">
    <button @click="openFaq = openFaq===i ? -1 : i" :aria-expanded="openFaq===i">
      <span>{{ f.q }}</span><i>{{ openFaq===i ? '−' : '+' }}</i>
    </button>
    <p v-show="openFaq===i">{{ f.a }}</p>
  </div>
</section>
<!-- script -->
const openFaq = ref(-1)
const faqs = [{ q:'...', a:'...' }]
```

**탭 전환**
```vue
<div class="tabs">
  <button v-for="t in tabs" :key="t.key" :class="{active: tab===t.key}" @click="tab=t.key">{{ t.label }}</button>
</div>
<div v-for="t in tabs" :key="t.key" v-show="tab===t.key" class="tab-panel">{{ t.body }}</div>
<!-- script --> const tab = ref(tabs[0].key)
```

**폼 제출 상태 토글** (기존 데모에 이미 있는 `sent`/`requested` 패턴 따름)
```vue
<button @click="sent = true">{{ sent ? '접수되었습니다.' : '신청하기' }}</button>
<!-- script --> const sent = ref(false)
```

**스크롤 리빌** (의존성 없이 IntersectionObserver)
```vue
<script setup>
import { onMounted } from 'vue'
onMounted(() => {
  const io = new IntersectionObserver((es) => es.forEach(e => { if (e.isIntersecting) e.target.classList.add('in') }), { threshold: 0.15 })
  document.querySelectorAll('.reveal').forEach(el => io.observe(el))
})
</script>
<!-- css --> .reveal{opacity:0;transform:translateY(24px);transition:.7s} .reveal.in{opacity:1;transform:none}
```

**카운트업** (숫자 신뢰지표)
```vue
<script setup>
import { onMounted, ref } from 'vue'
const shown = ref([0,0,0])
const targets = [280, 98, 14]
onMounted(() => {
  const io = new IntersectionObserver((es) => { if (es[0].isIntersecting) { run(); io.disconnect() } }, { threshold: 0.4 })
  const el = document.querySelector('.numbers'); if (el) io.observe(el)
  function run(){ targets.forEach((t,i)=>{ let n=0; const step=Math.ceil(t/40); const id=setInterval(()=>{ n+=step; if(n>=t){n=t;clearInterval(id)} shown.value[i]=n },24) }) }
})
</script>
```
> 주의: `layout:false` 페이지에서 SSR 시 `document` 접근은 `onMounted` 내부에서만. `import.meta.client` 가드가 필요하면 추가.

---

# 배치 1 — 웨딩군 (8)

웨딩 대중 골격: 인사말/초대문구 → 예식 정보(날짜·시각·장소) → 갤러리 → 오시는 길 → 계좌/마음 전하실 곳 → RSVP(참석 의사) → 방명록/축하 메시지. FAQ 대신 "안내사항"으로 대체 가능.

## Task 1: classic-wedding (대중형)

**Files:** Modify `pages/demos/classic-wedding.vue` (현재 468줄, 이미 풍부)

**Style commit:** 대중형 — 세리프·크림톤 유지, 실험 최소, 가장 안정적인 정통 청첩장.

- [ ] **Step 1: 현재 파일 읽고 갭 파악**
  기존 섹션 목록을 확인하고 아래 대중 골격 대비 누락분을 식별한다: 인사말 / 예식정보 / 갤러리 / 오시는길 / 계좌안내 / RSVP / 안내사항(FAQ형).

- [ ] **Step 2: 누락 섹션 보강**
  누락된 것만 추가한다(중복 생성 금지). 최소 포함 목표:
  - 예식 정보 블록: 날짜(예: 2026년 10월 17일 토요일 오후 12시), 장소(예: 그랜드 웨딩홀 5F 그레이스홀), D-Day 표기
  - 오시는 길: 주소 + 지하철/버스/주차 안내 텍스트, "지도 보기" 버튼(동작은 앵커/외부링크 텍스트로)
  - 계좌 안내: 신랑측/신부측 계좌 항목(가상: 예금주·은행·번호 형식)

- [ ] **Step 3: 인터랙션 — 아코디언 안내사항 + RSVP 폼 상태**
  "안내사항" 아코디언(주차/식사/화환/포토부스 등 4항목)과 RSVP 참석여부 폼 제출 상태 토글(`sent`) 추가. 레시피의 아코디언·폼 패턴을 이 데모 클래스명으로 복제.

- [ ] **Step 4: 이미지 마커**
  모든 `<img>` 위에 AI-IMG 주석 추가. 예:
  ```html
  <!-- AI-IMG: 클래식 스튜디오 웨딩 커플, 크림톤 정장/드레스 · 우아하고 정적인 필름 무드 · 3:4 -->
  <!-- prompt: elegant classic Korean wedding couple studio portrait, cream tones, soft film grain, timeless editorial, vertical 3:4 -->
  ```
  (public/images/wedding-ai/*.png 가 이미 존재하므로, 해당 이미지를 쓰는 곳은 로컬 경로 유지하고 주석만 보강)

- [ ] **Step 5: verify**
  `pnpm build` 통과 확인. 아코디언/RSVP 토글이 템플릿 상 바인딩 오류 없는지 확인.

- [ ] **Step 6: commit**
  ```bash
  git add pages/demos/classic-wedding.vue
  git commit -m "feat(demo): classic-wedding 콘텐츠·안내 아코디언·RSVP 보강"
  ```

## Task 2: botanical-wedding (대중형)

**Files:** Modify `pages/demos/botanical-wedding.vue` (555줄)

**Style commit:** 대중형 — 그린 보태니컬 톤 유지, 야외 가든 웨딩의 편안한 정보 전달 중심.

- [ ] **Step 1:** 현재 파일 읽고 대중 골격 대비 갭 파악(예식정보/갤러리/오시는길/계좌/RSVP/안내사항).
- [ ] **Step 2:** 누락 섹션 보강 — Task 1과 동일 필드 세트(날짜·장소·오시는길·계좌). 카피는 보태니컬/가든 톤으로.
- [ ] **Step 3:** 인터랙션 — 갤러리 스크롤 리빌(`.reveal`) + RSVP 폼 상태. FAQ형 안내사항 아코디언 1개.
- [ ] **Step 4:** 모든 `<img>` 에 AI-IMG 주석. 예: `<!-- AI-IMG: 야외 가든 웨딩, 그린 식물·따뜻한 자연광 · 4:3 -->` / `<!-- prompt: outdoor garden wedding, lush greenery, warm natural light, botanical, 4:3 -->`
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/botanical-wedding.vue && git commit -m "feat(demo): botanical-wedding 콘텐츠·갤러리 리빌·RSVP 보강"`

## Task 3: signature-wedding (중간)

**Files:** Modify `pages/demos/signature-wedding.vue` (현재 29줄, 얇음 → 대폭 확장)

**Style commit:** 중간 — 호텔 브로슈어 톤. 저녁 예식/호텔 웨딩의 정돈된 고급감, 과하지 않은 포인트.

- [ ] **Step 1:** 현재 파일 읽기(29줄, 골격만 있음).
- [ ] **Step 2:** 대중 골격 전체 구축 — 인사말/예식정보(저녁 예식 시각)/갤러리/오시는길(호텔 발렛·연회장 층안내)/계좌/RSVP/안내사항. 호텔명·홀명 가상 값 사용.
- [ ] **Step 3:** 신뢰/디테일 요소 — 예식 타임라인(개식·예식·피로연 시각), 드레스코드 안내 1줄.
- [ ] **Step 4:** 인터랙션 — 안내사항 아코디언 + RSVP 폼 상태.
- [ ] **Step 5:** 모든 `<img>` AI-IMG 주석(호텔 저녁 웨딩, 딥톤·샹들리에 무드, 3:4/16:9).
- [ ] **Step 6:** `pnpm build` 통과.
- [ ] **Step 7:** `git add pages/demos/signature-wedding.vue && git commit -m "feat(demo): signature-wedding 실서비스 수준 섹션·인터랙션 구축"`

## Task 4: kids-birthday (중간)

**Files:** Modify `pages/demos/kids-birthday.vue` (123줄)

**Style commit:** 중간 — 파스텔 팝. 돌잔치/생일 초대의 밝고 친근한 톤 유지.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 보강 — 행사 정보(일시·장소), 오시는 길, 안내(주차/포토테이블/답례품), 방명록/축하메시지 영역, RSVP.
- [ ] **Step 3:** 인터랙션 — RSVP(참석 인원 선택) 폼 상태 + 안내 아코디언. 선택 시 카운트/요약 표시.
- [ ] **Step 4:** 모든 `<img>` AI-IMG 주석(파스텔 생일파티/돌상, 밝고 컬러풀, 1:1/4:3).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/kids-birthday.vue && git commit -m "feat(demo): kids-birthday 콘텐츠·RSVP·안내 보강"`

## Task 5: modern-wedding (스타일리쉬)

**Files:** Modify `pages/demos/modern-wedding.vue` (513줄)

**Style commit:** 스타일리쉬 — 흑백 대비·과감한 타이포 강화(시그니처). 정보 접근성은 유지.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 누락 섹션 보강(예식정보/오시는길/계좌/RSVP/안내). 카피는 미니멀·도시적.
- [ ] **Step 3:** 시그니처 강화 — 대형 타이포 헤딩/섹션 인덱스 번호, 흑백 그리드. 스크롤 리빌(`.reveal`)로 등장 연출.
- [ ] **Step 4:** 인터랙션 — 스크롤 리빌 + RSVP 폼 상태 + 안내 아코디언.
- [ ] **Step 5:** 모든 `<img>` AI-IMG 주석(흑백 모던 웨딩 화보, 강한 대비, 3:4).
- [ ] **Step 6:** `pnpm build` 통과.
- [ ] **Step 7:** `git add pages/demos/modern-wedding.vue && git commit -m "feat(demo): modern-wedding 콘텐츠·타이포 연출·인터랙션 보강"`

## Task 6: editorial-wedding (스타일리쉬)

**Files:** Modify `pages/demos/editorial-wedding.vue` (71줄)

**Style commit:** 스타일리쉬 — 화보/매거진 레이아웃, 큰 여백·비대칭 그리드(시그니처).

- [ ] **Step 1:** 현재 파일 읽기.
- [ ] **Step 2:** 대중 골격 채우되 매거진 편집 레이아웃으로 — 인사말(에디토리얼 카피)/예식정보/화보 갤러리/오시는길/계좌/RSVP/안내.
- [ ] **Step 3:** 시그니처 — 매거진식 페이지 인덱스(예: EDITORIAL 01), 비대칭 2단 그리드, 캡션 타이포.
- [ ] **Step 4:** 인터랙션 — 갤러리 스크롤 리빌 + RSVP 폼 상태.
- [ ] **Step 5:** 모든 `<img>` AI-IMG 주석(에디토리얼 스튜디오 웨딩, 매거진 화보, 3:4/16:9).
- [ ] **Step 6:** `pnpm build` 통과.
- [ ] **Step 7:** `git add pages/demos/editorial-wedding.vue && git commit -m "feat(demo): editorial-wedding 매거진 섹션·갤러리·RSVP 구축"`

## Task 7: archive-wedding (스타일리쉬)

**Files:** Modify `pages/demos/archive-wedding.vue` (25줄, 얇음)

**Style commit:** 스타일리쉬 — 필름 스냅·종이 질감·아카이브 무드(시그니처).

- [ ] **Step 1:** 현재 파일 읽기(25줄).
- [ ] **Step 2:** 대중 골격 전체 구축(인사말/예식정보/필름 갤러리/오시는길/계좌/RSVP/안내) — 아카이브/필름 톤 카피.
- [ ] **Step 3:** 시그니처 — 필름 인덱스 번호·날짜 스탬프, 종이 질감 배경, 흑백/세피아 이미지 처리(CSS filter).
- [ ] **Step 4:** 인터랙션 — 스크롤 리빌 + RSVP 폼 상태.
- [ ] **Step 5:** 모든 `<img>` AI-IMG 주석(필름 스냅 웨딩, 그레인·세피아, 4:3).
- [ ] **Step 6:** `pnpm build` 통과.
- [ ] **Step 7:** `git add pages/demos/archive-wedding.vue && git commit -m "feat(demo): archive-wedding 필름 아카이브 섹션·인터랙션 구축"`

## Task 8: vip-party (스타일리쉬)

**Files:** Modify `pages/demos/vip-party.vue` (158줄)

**Style commit:** 스타일리쉬 — 골드+딥블랙 럭셔리(시그니처). 브랜드 VIP 초청 톤.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 보강 — 행사 개요(일시·장소·드레스코드), 프로그램 타임라인, 참석 대상/혜택, 오시는 길(발렛), RSVP(참석/동반 인원), 문의.
- [ ] **Step 3:** 시그니처 — 골드 포인트 라인·세리프 대형 타이틀, 카운트다운 or 카운트업 지표(가상: 초청 인원/프로그램 수).
- [ ] **Step 4:** 인터랙션 — RSVP 폼 상태 + 프로그램 탭 또는 아코디언.
- [ ] **Step 5:** 모든 `<img>` AI-IMG 주석(럭셔리 VIP 파티/갈라, 골드·딥블랙, 16:9).
- [ ] **Step 6:** `pnpm build` 통과.
- [ ] **Step 7:** `git add pages/demos/vip-party.vue && git commit -m "feat(demo): vip-party 프로그램·RSVP·지표 보강"`

## Task 9: 배치 1 렌더 스팟체크 + 사용자 확인

- [ ] **Step 1:** dev 서버 실행: `pnpm dev` (백그라운드).
- [ ] **Step 2:** 스타일리쉬 1개(modern-wedding)와 대중형 1개(classic-wedding)를 브라우저로 로드, 콘솔 에러/레이아웃 깨짐 없는지 확인. 모바일 폭(375px)도 확인.
- [ ] **Step 3:** 사용자에게 배치 1 결과 보고 후 다음 배치 진행 승인 받기.

---

# 배치 2 — 의료군 (3)

의료 대중 골격: Hero → 진료 안내(과목/시술 상세) → 병원/의료진 소개 → 신뢰지표(수치) → 후기 → 오시는 길·진료시간 → FAQ → 예약/상담 CTA → 푸터(사업자정보).

## Task 10: dental-clinic (대중형)

**Files:** Modify `pages/demos/dental-clinic.vue` (21줄, 얇음)

**Style commit:** 대중형 — 따뜻한 세리프/베이지, 동네 치과의 신뢰·친근. 검증된 병원 홈 구조.

- [ ] **Step 1:** 현재 파일 읽기(treatments/reasons 배열 존재).
- [ ] **Step 2:** 섹션 보강 — 진료안내 상세(항목별 설명·소요·주의), 신뢰지표(개원 연차·누적 환자·재방문율 가상 수치), 환자 후기 3건(가상), FAQ 5문항, 진료시간표, 오시는길(교통·주차), 푸터 사업자정보 형식.
- [ ] **Step 3:** 인터랙션 — FAQ 아코디언 + 간편상담 폼 상태(기존 `sent` 활용) + 신뢰지표 카운트업.
- [ ] **Step 4:** 이미지 마커 — hero/의료진 `<img>` 위 AI-IMG 주석(밝은 치과 진료실, 청결·따뜻, 16:9 / 치과의사 포트레이트 3:4).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/dental-clinic.vue && git commit -m "feat(demo): dental-clinic 진료상세·후기·FAQ·지표 보강"`

## Task 11: medical-center (대중형)

**Files:** Modify `pages/demos/medical-center.vue` (22줄, 얇음)

**Style commit:** 대중형 — 지역 종합병원 표준. 정보 탐색성 최우선(진료과·의료진·예약·오시는길 빠르게).

- [ ] **Step 1:** 현재 파일 읽기.
- [ ] **Step 2:** 섹션 구축 — 진료과 목록(내과/정형외과/소아과 등 6~8개, 각 1줄 설명), 의료진 소개 카드 3~4명(가상: 성명·전문분야), 신뢰지표(병상 수·연간 진료·응급 24시간), 이용 안내(예약방법·준비물), FAQ, 진료시간/과별 시간표, 오시는길, 푸터 사업자정보.
- [ ] **Step 3:** 인터랙션 — 진료과 탭 전환(과 선택 시 안내 표시) + FAQ 아코디언 + 지표 카운트업.
- [ ] **Step 4:** 이미지 마커(종합병원 외관/로비, 밝고 신뢰감, 16:9 / 진료 장면).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/medical-center.vue && git commit -m "feat(demo): medical-center 진료과 탭·의료진·지표·FAQ 구축"`

## Task 12: hospital (스타일리쉬)

**Files:** Modify `pages/demos/hospital.vue` (22줄, 스타일 완성·콘텐츠 얇음 — NUE 피부/웰니스 클리닉)

**Style commit:** 스타일리쉬 — 기존 미니멀 웰니스 톤(세리프+모노, 세이지그린) 강화가 시그니처. 프리미엄 감성 유지.

- [ ] **Step 1:** 현재 파일 읽기(care 배열, journal/booking 섹션 존재).
- [ ] **Step 2:** 콘텐츠 보강(스타일 언어 유지) — care 항목별 상세(효과·과정·소요·회복), 프로그램/가격대 안내(가상, "상담 후 결정" 톤), 신뢰지표(누적 상담·재방문·전문의 수), 고객 후기 2~3건, FAQ(피부/시술 관련 5문항), 오시는길·운영시간, 푸터 사업자정보.
- [ ] **Step 3:** 인터랙션 — FAQ 아코디언 + 상담 폼 상태(기존 `requested`) + 지표 카운트업.
- [ ] **Step 4:** 이미지 마커 — hero/공간 `<img>` AI-IMG 주석(차분한 프라이빗 클리닉 인테리어, 세이지톤·자연광, 16:9/3:4).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/hospital.vue && git commit -m "feat(demo): hospital(NUE) 시술상세·후기·FAQ·지표 보강"`

## Task 13: 배치 2 렌더 스팟체크 + 사용자 확인

- [ ] **Step 1:** `pnpm dev`, dental-clinic(대중형)·hospital(스타일리쉬) 브라우저 확인(데스크톱+375px). 탭/아코디언/카운트업 동작 확인.
- [ ] **Step 2:** 사용자 보고 후 승인.

---

# 배치 3 — 기업·전문직 (4)

기업 대중 골격: Hero → 회사/서비스 소개 → 사업/업무 분야 → 실적·신뢰지표 → 사례/포트폴리오 → 고객사/후기 → FAQ 또는 인사이트 → 문의 CTA → 푸터(사업자정보).

## Task 14: corporate-company (대중형)

**Files:** Modify `pages/demos/corporate-company.vue` (28줄, 얇음)

**Style commit:** 대중형 — 표준 기업 홈페이지. 신뢰감 있는 그리드·명확한 정보 구조.

- [ ] **Step 1:** 현재 파일 읽기.
- [ ] **Step 2:** 섹션 구축 — 회사 소개(비전·연혁 타임라인), 주요 사업 3~4개 상세, 실적 지표(설립연도·프로젝트 수·고객사 수), 대표 사례 3건, 고객사 로고 영역(텍스트 플레이스홀더), FAQ, 문의 폼(상태 토글), 푸터 사업자정보.
- [ ] **Step 3:** 인터랙션 — 연혁/사업 탭 또는 스크롤 리빌 + 문의 폼 상태 + 지표 카운트업.
- [ ] **Step 4:** 이미지 마커(모던 오피스/팀 협업, 밝고 프로페셔널, 16:9).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/corporate-company.vue && git commit -m "feat(demo): corporate-company 사업·실적·사례·문의 보강"`

## Task 15: corporate-event (중간)

**Files:** Modify `pages/demos/corporate-event.vue` (159줄)

**Style commit:** 중간 — 네이비/그리드 컨퍼런스 초청. 프로페셔널하되 포인트 있는 세미나 랜딩.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 보강 — 행사 개요(일시·장소·주제), 프로그램 타임테이블(세션별 시각·연사), 연사 소개 카드(가상 3~4명), 참가 혜택, 등록/티켓 안내(등급별), 오시는 길, FAQ, 등록 폼 상태, 푸터.
- [ ] **Step 3:** 인터랙션 — 프로그램 탭(Day1/Day2 or 트랙) + FAQ 아코디언 + 등록 폼 상태.
- [ ] **Step 4:** 이미지 마커(컨퍼런스 무대/청중, 네이비 톤, 16:9 / 연사 포트레이트).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/corporate-event.vue && git commit -m "feat(demo): corporate-event 프로그램·연사·등록 보강"`

## Task 16: law-firm (대중형)

**Files:** Modify `pages/demos/law-firm.vue` (23줄, 스타일 완성·콘텐츠 얇음 — RATIO LAW)

**Style commit:** 대중형(무게감 있는 정통) — 기존 다크+세리프 톤 유지하되, 로펌 홈의 검증된 정보 구조를 충실히. (스펙표상 대중형이나 시각 톤은 이미 고급)

- [ ] **Step 1:** 현재 파일 읽기(numbers/practice 배열 존재).
- [ ] **Step 2:** 콘텐츠 보강 — 업무분야 상세(각 분야 설명·대표 업무 3줄), 구성원(파트너) 소개 카드 3~4명(가상: 성명·분야·약력 1줄), 대표 자문/사례(수치·업종), 인사이트/칼럼 목록 3건, FAQ 또는 상담 절차 안내, 상담 문의 폼 상태, 푸터 사업자정보.
- [ ] **Step 3:** 인터랙션 — 업무분야 아코디언(상세 펼침) + 상담 폼 상태 + 기존 numbers 카운트업.
- [ ] **Step 4:** 이미지 마커(로펌 회의실/도시 오피스, 무게감·다크, 16:9 / 변호사 포트레이트 3:4).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/law-firm.vue && git commit -m "feat(demo): law-firm 업무분야·구성원·인사이트·상담 보강"`

## Task 17: architecture (스타일리쉬)

**Files:** Modify `pages/demos/architecture.vue` (20줄, 스타일 완성·콘텐츠 얇음 — FORM/FIELD)

**Style commit:** 스타일리쉬 — 기존 이미지 중심·비대칭·레드 포인트 아방가르드 유지 강화가 시그니처.

- [ ] **Step 1:** 현재 파일 읽기(projects 배열 존재).
- [ ] **Step 2:** 콘텐츠 보강(스타일 유지) — 프로젝트 6개로 확장(각 유형·연도·설명·규모), 서비스 범위(설계·감리·인테리어), 스튜디오 소개·팀·수상/실적 지표, 프로세스 단계(1~4), 저널/노트 목록, 문의(폼 상태 or 메일), 푸터.
- [ ] **Step 3:** 인터랙션 — 프로젝트 갤러리 필터(유형별: 주거/문화/상업) 또는 스크롤 리빌 + 문의 폼 상태.
- [ ] **Step 4:** 이미지 마커 — 각 project image + hero AI-IMG 주석(현대 건축 외관/공간, 미니멀·자연광, 4:3/16:9).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/architecture.vue && git commit -m "feat(demo): architecture 프로젝트 확장·필터·프로세스·문의 보강"`

## Task 18: 배치 3 렌더 스팟체크 + 사용자 확인

- [ ] **Step 1:** `pnpm dev`, corporate-company(대중형)·architecture(스타일리쉬) 확인(데스크톱+375px). 필터/탭/폼 동작 확인.
- [ ] **Step 2:** 사용자 보고 후 승인.

---

# 배치 4 — 커머스·행사 (4)

## Task 19: b2b-landing (대중형)

**Files:** Modify `pages/demos/b2b-landing.vue` (443줄, 이미 풍부)

**Style commit:** 대중형 — 미니멀 흑백 리드젠 랜딩. 전환 최적화 검증 패턴.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악(리드젠 랜딩 필수 블록: 헤드라인/가치제안/기능/사회적증거/가격 or 데모신청/FAQ/CTA).
- [ ] **Step 2:** 누락 보강 — 고객 로고/후기(사회적 증거), 숫자 성과지표, 요금제 or 데모신청 섹션, FAQ, 최종 CTA 폼.
- [ ] **Step 3:** 인터랙션 — 데모신청/문의 폼 상태 + FAQ 아코디언 + 지표 카운트업.
- [ ] **Step 4:** 이미지 마커(SaaS 대시보드/추상 그래픽, 미니멀 흑백, 16:9).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/b2b-landing.vue && git commit -m "feat(demo): b2b-landing 사회적증거·요금·FAQ·CTA 보강"`

## Task 20: ecommerce (중간)

**Files:** Modify `pages/demos/ecommerce.vue` (233줄)

**Style commit:** 중간 — 라이프스타일 브랜드 쇼핑몰. 상품 탐색·구매 유도 검증 UX + 브랜드 무드.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 보강 — 상품 그리드(가격·태그, 6~8개), 카테고리 필터, 베스트/신상 섹션, 상품 후기·별점, 브랜드 스토리, 배송/교환 안내, FAQ, 뉴스레터/장바구니 유도. 가상 상품명·가격.
- [ ] **Step 3:** 인터랙션 — 카테고리 필터(전체/의류/리빙 등) + 장바구니 담기 카운트(담기 시 배지 수 증가) + FAQ 아코디언.
- [ ] **Step 4:** 이미지 마커(라이프스타일 제품 컷/룩북, 미니멀·따뜻, 1:1/4:5 상품, 16:9 배너).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/ecommerce.vue && git commit -m "feat(demo): ecommerce 상품필터·장바구니·후기·안내 보강"`

## Task 21: bio-link (스타일리쉬)

**Files:** Modify `pages/demos/bio-link.vue` (194줄)

**Style commit:** 스타일리쉬 — 글래스모피즘 멀티링크(시그니처). SNS 프로필 톤.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 보강 — 프로필(이름·소개·태그), 링크 버튼 6~8개(카테고리 구분: 예약/샵/SNS/문의), 대표 콘텐츠 미리보기 카드, 소셜 아이콘, 간단 소식/공지, 문의/뉴스레터. 링크 클릭 카운트(가상) 표기 가능.
- [ ] **Step 3:** 인터랙션 — 링크 탭/카테고리 전환 + 복사/공유 버튼 상태 토글(눌림 피드백).
- [ ] **Step 4:** 이미지 마커(프로필 아바타/배경, 글래스·그라디언트, 1:1 아바타 / 배경 9:16).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/bio-link.vue && git commit -m "feat(demo): bio-link 프로필·카테고리 링크·공유 보강"`

## Task 22: exhibition (스타일리쉬)

**Files:** Modify `pages/demos/exhibition.vue` (157줄)

**Style commit:** 스타일리쉬 — 비대칭·아방가르드 타이포(시그니처). 갤러리 전시 오프닝.

- [ ] **Step 1:** 현재 파일 읽고 갭 파악.
- [ ] **Step 2:** 보강 — 전시 개요(제목·기간·장소·큐레이터), 작가/작품 소개 카드, 전시 섹션/동선 안내, 관람 정보(시간·요금·예매), 프로그램/도슨트 일정, 오시는 길, 문의, 방명록/RSVP. 가상 전시명·작가명.
- [ ] **Step 3:** 인터랙션 — 작품 갤러리 필터 또는 스크롤 리빌 + 관람 예매 폼 상태.
- [ ] **Step 4:** 이미지 마커(갤러리 전시 전경/작품, 아방가르드·화이트큐브, 3:4/16:9).
- [ ] **Step 5:** `pnpm build` 통과.
- [ ] **Step 6:** `git add pages/demos/exhibition.vue && git commit -m "feat(demo): exhibition 작가·관람정보·프로그램·예매 보강"`

## Task 23: index.vue 카드 문구 동기화

**Files:** Modify `pages/index.vue`

- [ ] **Step 1:** 각 데모 재설계 결과에 맞춰 카드 `card-desc` 문구가 실제 내용과 어긋나는 곳만 수정(전면 재설계 아님).
- [ ] **Step 2:** 스타일 스펙트럼이 카드에서 드러나도록 태그 보강 검토(예: `대중형`/`스타일리쉬` 뉘앙스 태그) — 선택.
- [ ] **Step 3:** `pnpm build` 통과.
- [ ] **Step 4:** `git add pages/index.vue && git commit -m "chore(demo): index 카드 문구 데모 내용과 동기화"`

## Task 24: 배치 4 + 최종 렌더/빌드 검증 + 사용자 확인

- [ ] **Step 1:** `pnpm build` 전체 통과(에러 0).
- [ ] **Step 2:** `pnpm dev`, ecommerce(필터/장바구니)·exhibition(스타일리쉬) 확인(데스크톱+375px).
- [ ] **Step 3:** 19개 데모 라우트 전수 로드 스팟체크(콘솔 에러 없음).
- [ ] **Step 4:** 사용자 최종 보고, 브랜치 마무리 방식 결정(finishing-a-development-branch).

---

## Self-Review 결과

- **스펙 커버리지:** 스펙의 스코프(19개), 블루프린트(섹션/인터랙션/접근성), 이미지 마커, 스타일 스펙트럼 배정표 → 각각 태스크로 매핑됨. 배치 4단계·배치별 확인 게이트 반영. index 동기화(스펙 언급) → Task 23.
- **placeholder 스캔:** 각 태스크에 구체 섹션·데이터 필드·인터랙션·이미지 프롬프트 명시. "적당히" 류 없음. (콘텐츠 실값은 실행 시 데모 톤 맞춰 작성하도록 도메인 적응 절에 명시)
- **일관성:** 인터랙션 구현은 상단 레시피(아코디언 `openFaq`, 탭 `tab`, 폼 `sent`/`requested`, 리빌 `.reveal`, 카운트업)로 통일. 기존 데모의 `sent`/`requested` ref 이름 재사용.
- **스타일 배정 일치:** 스펙 배정표와 태스크 Style commit 일치(웨딩 대중=classic/botanical, 스타일리쉬=modern/editorial/archive/vip; 의료 대중=dental/medical-center, 스타일리쉬=hospital; 기업 대중=law-firm/corporate-company, 중간=corporate-event, 스타일리쉬=architecture; 커머스 대중=b2b, 중간=ecommerce, 스타일리쉬=bio-link/exhibition).
