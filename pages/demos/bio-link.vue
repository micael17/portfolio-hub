<template>
  <div class="bio-link-bg">
    <div class="glass-card">
      <!-- AI-IMG: 커버 배경 이미지, 파스텔 그라디언트 위 추상 디자인 작업물 · 3:1 와이드 -->
      <!-- prompt: abstract colorful design studio moodboard banner, soft pastel gradient, blurred, wide 3:1 -->
      <div class="header-cover"></div>

      <div class="profile-section">
        <!-- AI-IMG: 프로필 아바타, 글래스·밝은 그라디언트 배경의 디자이너 인물 · 1:1 -->
        <!-- prompt: profile avatar portrait of a creative designer, soft gradient glassmorphism, bright, friendly, 1:1 -->
        <img
          src="https://images.unsplash.com/photo-1611162617474-5b21e879e113?w=400&q=80"
          alt="문채린 디자이너 프로필 사진"
          class="profile-img"
        >
        <h2>채린 스튜디오</h2>
        <p class="handle">@chaerin.studio</p>
        <p class="bio">브랜드 &amp; UI/UX 디자인 스튜디오<br>로고 · 앱 화면 · 디자인 시스템을 만듭니다.</p>
        <div class="tags">
          <span class="tag"><i class="fa-solid fa-pen-ruler"></i> 프로덕트 디자이너</span>
          <span class="tag"><i class="fa-solid fa-location-dot"></i> 서울, 성수</span>
          <span class="tag"><i class="fa-solid fa-circle-check"></i> 신규 의뢰 가능</span>
        </div>

        <div class="action-row">
          <button class="action-btn" :class="{ done: copied }" @click="copyLink">
            <i :class="copied ? 'fa-solid fa-check' : 'fa-solid fa-link'"></i>
            {{ copied ? '주소 복사됨' : '링크 복사' }}
          </button>
          <button class="action-btn" :class="{ done: shared }" @click="sharePage">
            <i :class="shared ? 'fa-solid fa-check' : 'fa-solid fa-share-nodes'"></i>
            {{ shared ? '공유 완료' : '공유하기' }}
          </button>
        </div>
      </div>

      <div class="content-section">
        <!-- 카테고리 탭 -->
        <div class="tabs" role="tablist">
          <button
            v-for="c in categories"
            :key="c.key"
            class="tab"
            :class="{ active: tab === c.key }"
            role="tab"
            :aria-selected="tab === c.key"
            @click="tab = c.key"
          >
            {{ c.label }}
          </button>
        </div>

        <!-- 카테고리별 링크 버튼 -->
        <div class="links">
          <a
            v-for="link in filteredLinks"
            :key="link.title"
            :href="link.url"
            target="_blank"
            rel="noopener"
            class="link-item"
            :class="{ highlight: link.highlight }"
          >
            <div class="link-icon"><i :class="link.icon"></i></div>
            <div class="link-text">
              <strong>{{ link.title }}</strong>
              <span>{{ link.desc }}</span>
            </div>
            <div class="link-meta">
              <span class="clicks"><i class="fa-solid fa-arrow-pointer"></i> {{ link.clicks }}</span>
              <i class="fa-solid fa-chevron-right arrow"></i>
            </div>
          </a>
          <p v-if="!filteredLinks.length" class="empty-links">이 카테고리에 등록된 링크가 아직 없어요.</p>
        </div>

        <!-- 대표 콘텐츠 미리보기 -->
        <h3>대표 콘텐츠</h3>
        <div class="video-container">
          <div class="video-mock">
            <!-- AI-IMG: 유튜브 대표 영상 썸네일, 피그마 작업 화면 캡처 느낌 · 16:9 -->
            <!-- prompt: youtube thumbnail of figma design workflow screen, clean UI, 16:9 -->
            <img
              src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=800&q=80"
              alt="피그마 디자인 워크플로우 영상 썸네일"
            >
            <div class="play-btn"><i class="fa-solid fa-play"></i></div>
            <div class="video-badge">조회수 4.2만</div>
            <div class="video-title">피그마로 앱 화면 하루 만에 완성하기</div>
          </div>
        </div>

        <div class="preview-cards">
          <!--
            AI-IMG(1): 인스타 최근 게시물, 모바일 앱 온보딩 UI 3화면 · 4:3
            prompt: instagram post of mobile app onboarding UI screens, bright, 4:3
            AI-IMG(2): 스토어 인기 상품, 피그마 UI 킷 목업 · 4:3
            prompt: product mockup of a figma UI kit, isometric, colorful, 4:3
          -->
          <a
            v-for="card in previewCards"
            :key="card.title"
            :href="card.url"
            target="_blank"
            rel="noopener"
            class="preview-card"
          >
            <img :src="card.img" :alt="card.alt">
            <div class="preview-body">
              <span class="preview-kind">{{ card.kind }}</span>
              <strong>{{ card.title }}</strong>
              <span class="preview-sub">{{ card.sub }}</span>
            </div>
          </a>
        </div>

        <!-- 소식 / 공지 -->
        <h3>소식</h3>
        <div class="news">
          <div v-for="n in notices" :key="n.title" class="news-item">
            <div class="news-dot" :class="n.type"></div>
            <div class="news-body">
              <strong>{{ n.title }}</strong>
              <span>{{ n.date }} · {{ n.desc }}</span>
            </div>
          </div>
        </div>

        <!-- 뉴스레터 구독 -->
        <div class="newsletter" :class="{ done: subscribed }">
          <template v-if="!subscribed">
            <h4>월간 디자인 레터</h4>
            <p>새 작업물과 무료 리소스를 매달 첫째 주에 보내드려요.</p>
            <form class="news-form" @submit.prevent="subscribe">
              <input
                v-model="email"
                type="email"
                inputmode="email"
                placeholder="이메일 주소"
                aria-label="이메일 주소"
                required
              >
              <button type="submit"><i class="fa-solid fa-paper-plane"></i></button>
            </form>
          </template>
          <div v-else class="news-thanks">
            <i class="fa-solid fa-circle-check"></i>
            <div>
              <strong>구독 완료!</strong>
              <span>{{ email }} 로 확인 메일을 보냈어요.</span>
            </div>
          </div>
        </div>

        <!-- 소셜 아이콘 -->
        <div class="socials">
          <a href="https://instagram.com/chaerin.studio" target="_blank" rel="noopener" aria-label="인스타그램"><i class="fa-brands fa-instagram"></i></a>
          <a href="https://youtube.com/@chaerin.studio" target="_blank" rel="noopener" aria-label="유튜브"><i class="fa-brands fa-youtube"></i></a>
          <a href="https://www.behance.net/chaerinstudio" target="_blank" rel="noopener" aria-label="비핸스"><i class="fa-brands fa-behance"></i></a>
          <a href="https://dribbble.com/chaerin-studio" target="_blank" rel="noopener" aria-label="드리블"><i class="fa-brands fa-dribbble"></i></a>
          <a href="mailto:hello@chaerin.studio" aria-label="이메일 문의"><i class="fa-solid fa-envelope"></i></a>
        </div>
      </div>

      <div class="footer">
        <p>Powered by <strong>LinkHub</strong></p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

useHead({
  title: 'Bio Link | 채린 스튜디오',
  link: [{ rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css' }]
})
definePageMeta({ layout: false })

// 카테고리 탭 전환
const tab = ref('all')
const categories = [
  { key: 'all', label: '전체' },
  { key: 'work', label: '포트폴리오' },
  { key: 'shop', label: '샵' },
  { key: 'contact', label: '문의' }
]

const links = [
  { cat: 'work', icon: 'fa-solid fa-briefcase', title: '포트폴리오 보기', desc: '2026 브랜드 · UI 케이스 스터디', clicks: '12.4k', highlight: true, url: 'https://chaerin.studio/portfolio' },
  { cat: 'work', icon: 'fa-brands fa-behance', title: 'Behance 프로젝트', desc: '전체 작업물 아카이브', clicks: '3.8k', url: 'https://www.behance.net/chaerinstudio' },
  { cat: 'shop', icon: 'fa-solid fa-store', title: '디자인 에셋 샵', desc: 'Figma 템플릿 · UI 킷', clicks: '9.1k', url: 'https://smartstore.naver.com/chaerin-studio' },
  { cat: 'shop', icon: 'fa-solid fa-book-open', title: '무료 아이콘 팩', desc: '120종 라인 아이콘 다운로드', clicks: '15.7k', url: 'https://gumroad.com/chaerin/line-icons' },
  { cat: 'contact', icon: 'fa-solid fa-calendar-check', title: '30분 상담 예약', desc: '프로젝트 문의 · 캘린더 예약', clicks: '2.1k', url: 'https://calendly.com/chaerin-studio/30min' },
  { cat: 'contact', icon: 'fa-solid fa-envelope', title: '제휴 · 외주 문의', desc: '프리랜스 작업 가능', clicks: '1.6k', url: 'mailto:hello@chaerin.studio' },
  { cat: 'work', icon: 'fa-brands fa-youtube', title: '디자인 튜토리얼', desc: '유튜브 채널 구독 4.5만', clicks: '22.3k', url: 'https://youtube.com/@chaerin.studio' }
]
const filteredLinks = computed(() =>
  tab.value === 'all' ? links : links.filter(l => l.cat === tab.value)
)

// 대표 콘텐츠 미리보기 카드
const previewCards = [
  {
    kind: '최근 게시물',
    title: '앱 온보딩 리디자인',
    sub: '좋아요 1,240',
    img: 'https://images.unsplash.com/photo-1558655146-d09347e92766?w=400&q=80',
    alt: '앱 온보딩 UI 리디자인 게시물 미리보기',
    prompt: 'instagram post of mobile app onboarding UI screens, bright, 4:3',
    url: 'https://instagram.com/p/chaerin-onboarding'
  },
  {
    kind: '인기 상품',
    title: 'Minimal UI Kit',
    sub: '₩29,000',
    img: 'https://images.unsplash.com/photo-1561070791-2526d30994b5?w=400&q=80',
    alt: '미니멀 UI 킷 상품 미리보기',
    prompt: 'product mockup of a figma UI kit, isometric, colorful, 4:3',
    url: 'https://smartstore.naver.com/chaerin-studio/products/minimal-ui-kit'
  }
]

// 소식 / 공지
const notices = [
  { type: 'new', title: '신규 UI 킷 출시', date: '7월 2주', desc: 'Minimal UI Kit v2 업데이트' },
  { type: 'info', title: '8월 의뢰 마감 임박', date: '상시', desc: '이번 달 잔여 2건' }
]

// 링크 복사 / 공유 상태 토글
const pageUrl = 'https://linkhub.app/chaerin.studio'
const copied = ref(false)
const shared = ref(false)

function copyLink() {
  if (import.meta.client && typeof navigator !== 'undefined' && navigator.clipboard) {
    navigator.clipboard.writeText(pageUrl).catch(() => {})
  }
  copied.value = true
  setTimeout(() => { copied.value = false }, 1500)
}

function sharePage() {
  if (import.meta.client && typeof navigator !== 'undefined' && navigator.share) {
    navigator.share({ title: '채린 스튜디오', url: pageUrl }).catch(() => {})
  } else if (import.meta.client && typeof navigator !== 'undefined' && navigator.clipboard) {
    navigator.clipboard.writeText(pageUrl).catch(() => {})
  }
  shared.value = true
  setTimeout(() => { shared.value = false }, 1500)
}

// 뉴스레터 구독 폼
const email = ref('')
const subscribed = ref(false)
function subscribe() {
  if (!email.value) return
  subscribed.value = true
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;800&display=swap');

.bio-link-bg {
  min-height: 100vh;
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  display: flex;
  justify-content: center;
  align-items: flex-start;
  font-family: 'Outfit', sans-serif;
  padding: 3rem 1rem;
  position: relative;
  overflow-x: hidden;
}

.bio-link-bg::before {
  content: ''; position: absolute; width: 500px; height: 500px; background: rgba(255, 255, 255, 0.3); border-radius: 50%; top: -150px; left: -150px; filter: blur(100px);
}
.bio-link-bg::after {
  content: ''; position: absolute; width: 400px; height: 400px; background: rgba(255, 200, 0, 0.2); border-radius: 50%; bottom: -100px; right: -100px; filter: blur(80px);
}

.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(30px);
  -webkit-backdrop-filter: blur(30px);
  border: 1px solid rgba(255, 255, 255, 0.4);
  width: 100%;
  max-width: 480px;
  border-radius: 40px;
  box-shadow: 0 40px 80px rgba(0,0,0,0.15);
  z-index: 1;
  overflow: hidden;
  position: relative;
}

.header-cover {
  height: 150px;
  background: url('https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=800&q=80') center/cover;
  position: relative;
}
.header-cover::after {
  content: ''; position: absolute; top:0; left:0; width:100%; height:100%; background: linear-gradient(to bottom, transparent, rgba(0,0,0,0.5));
}

.profile-section {
  text-align: center;
  margin-top: -60px;
  position: relative;
  z-index: 2;
  padding: 0 2rem;
}

.profile-img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 1rem;
  border: 4px solid #fff;
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

h2 { font-size: 1.8rem; margin-bottom: 0.25rem; color: #fff; font-weight: 800; text-shadow: 0 2px 10px rgba(0,0,0,0.2); }
.handle { color: rgba(255,255,255,0.85); font-size: 0.95rem; font-weight: 600; margin-bottom: 0.75rem; }
.bio { color: rgba(255, 255, 255, 0.95); font-size: 1.02rem; font-weight: 500; line-height: 1.5; }

.tags {
  display: flex; flex-wrap: wrap; justify-content: center; gap: 0.5rem; margin-top: 1rem;
}
.tag {
  display: inline-flex; align-items: center; gap: 0.35rem;
  background: rgba(255,255,255,0.2); border: 1px solid rgba(255,255,255,0.3);
  color: #fff; font-size: 0.8rem; font-weight: 600; padding: 0.35rem 0.75rem; border-radius: 999px;
}

.action-row { display: flex; gap: 0.75rem; margin-top: 1.25rem; }
.action-btn {
  flex: 1; display: inline-flex; align-items: center; justify-content: center; gap: 0.5rem;
  background: rgba(255,255,255,0.2); border: 1px solid rgba(255,255,255,0.35);
  color: #fff; font-family: inherit; font-size: 0.9rem; font-weight: 700;
  padding: 0.7rem 0.5rem; border-radius: 14px; cursor: pointer; transition: all 0.25s ease;
}
.action-btn:hover { background: rgba(255,255,255,0.35); transform: translateY(-2px); }
.action-btn.done { background: #fff; color: #f5576c; border-color: #fff; }

.content-section { padding: 1.5rem 2rem 2rem; }

.tabs {
  display: flex; gap: 0.4rem; background: rgba(255,255,255,0.12);
  border: 1px solid rgba(255,255,255,0.2); border-radius: 16px; padding: 0.35rem; margin-bottom: 1.5rem;
}
.tab {
  flex: 1; background: transparent; border: none; color: rgba(255,255,255,0.85);
  font-family: inherit; font-size: 0.85rem; font-weight: 700; padding: 0.55rem 0.25rem;
  border-radius: 12px; cursor: pointer; transition: all 0.25s ease;
}
.tab:hover { color: #fff; }
.tab.active { background: #fff; color: #f5576c; box-shadow: 0 6px 16px rgba(0,0,0,0.12); }

h3 { color: #fff; font-size: 1.2rem; font-weight: 800; margin-bottom: 1rem; margin-top: 2rem; }

.links { display: flex; flex-direction: column; gap: 1rem; }
.link-item {
  display: flex; align-items: center; padding: 1rem; background: rgba(255, 255, 255, 0.15); color: #fff; text-decoration: none; border-radius: 20px; transition: all 0.3s ease; border: 1px solid rgba(255, 255, 255, 0.2);
}
.link-item:hover { transform: translateY(-3px); background: rgba(255, 255, 255, 0.25); box-shadow: 0 15px 30px rgba(0,0,0,0.1); }
.link-item.highlight { background: rgba(255, 255, 255, 0.95); color: #111; }
.link-item.highlight:hover { background: #fff; box-shadow: 0 15px 30px rgba(245, 87, 108, 0.3); }

.link-icon { width: 50px; height: 50px; background: rgba(0,0,0,0.05); border-radius: 15px; display: flex; justify-content: center; align-items: center; font-size: 1.3rem; margin-right: 1rem; flex-shrink: 0; }
.highlight .link-icon { background: rgba(245, 87, 108, 0.1); color: #f5576c; }
.link-item:not(.highlight) .link-icon { background: rgba(255,255,255,0.15); }

.link-text { flex: 1; display: flex; flex-direction: column; min-width: 0; }
.link-text strong { font-size: 1.1rem; font-weight: 800; margin-bottom: 0.2rem; }
.link-text span { font-size: 0.85rem; opacity: 0.8; font-weight: 500; }

.link-meta { display: flex; flex-direction: column; align-items: flex-end; gap: 0.35rem; margin-left: 0.5rem; flex-shrink: 0; }
.clicks { font-size: 0.72rem; font-weight: 700; opacity: 0.7; display: inline-flex; align-items: center; gap: 0.25rem; white-space: nowrap; }
.arrow { opacity: 0.5; font-size: 0.9rem; }

.empty-links { color: rgba(255,255,255,0.8); font-size: 0.9rem; text-align: center; padding: 1rem 0; }

.video-container { width: 100%; border-radius: 20px; overflow: hidden; position: relative; }
.video-mock { width: 100%; height: 200px; position: relative; display: flex; justify-content: center; align-items: center; cursor: pointer; }
.video-mock img { position: absolute; width: 100%; height: 100%; object-fit: cover; transition: transform 0.3s; }
.video-mock::after { content: ''; position: absolute; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.3); transition: background 0.3s; }
.video-mock:hover img { transform: scale(1.05); }
.video-mock:hover::after { background: rgba(0,0,0,0.2); }
.play-btn { width: 60px; height: 60px; background: rgba(255,255,255,0.9); color: #f5576c; border-radius: 50%; display: flex; justify-content: center; align-items: center; font-size: 1.5rem; position: relative; z-index: 2; padding-left: 5px; box-shadow: 0 10px 20px rgba(0,0,0,0.2); }
.video-badge { position: absolute; top: 12px; right: 12px; z-index: 2; background: rgba(0,0,0,0.55); color: #fff; font-size: 0.72rem; font-weight: 700; padding: 0.25rem 0.6rem; border-radius: 999px; }
.video-title { position: absolute; bottom: 15px; left: 15px; right: 15px; color: #fff; font-weight: 700; z-index: 2; text-shadow: 0 2px 4px rgba(0,0,0,0.6); }

.preview-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 1rem; }
.preview-card {
  background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.2);
  border-radius: 18px; overflow: hidden; text-decoration: none; color: #fff; transition: all 0.3s ease;
}
.preview-card:hover { transform: translateY(-3px); background: rgba(255,255,255,0.25); box-shadow: 0 15px 30px rgba(0,0,0,0.12); }
.preview-card img { width: 100%; height: 110px; object-fit: cover; display: block; }
.preview-body { padding: 0.75rem; display: flex; flex-direction: column; gap: 0.2rem; }
.preview-kind { font-size: 0.68rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.04em; opacity: 0.75; }
.preview-body strong { font-size: 0.95rem; font-weight: 800; }
.preview-sub { font-size: 0.8rem; opacity: 0.85; font-weight: 600; }

.news { display: flex; flex-direction: column; gap: 0.75rem; }
.news-item {
  display: flex; align-items: flex-start; gap: 0.75rem; padding: 0.9rem 1rem;
  background: rgba(255,255,255,0.12); border: 1px solid rgba(255,255,255,0.18); border-radius: 16px;
}
.news-dot { width: 10px; height: 10px; border-radius: 50%; margin-top: 0.35rem; flex-shrink: 0; }
.news-dot.new { background: #ffd166; box-shadow: 0 0 0 4px rgba(255,209,102,0.25); }
.news-dot.info { background: #a0e7e5; box-shadow: 0 0 0 4px rgba(160,231,229,0.25); }
.news-body { display: flex; flex-direction: column; gap: 0.15rem; }
.news-body strong { color: #fff; font-size: 0.95rem; font-weight: 800; }
.news-body span { color: rgba(255,255,255,0.82); font-size: 0.8rem; font-weight: 500; }

.newsletter {
  margin-top: 1.5rem; padding: 1.25rem; border-radius: 20px;
  background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.25); text-align: center;
}
.newsletter h4 { color: #fff; font-size: 1.05rem; font-weight: 800; margin-bottom: 0.35rem; }
.newsletter p { color: rgba(255,255,255,0.85); font-size: 0.85rem; font-weight: 500; margin-bottom: 0.9rem; }
.news-form { display: flex; gap: 0.5rem; }
.news-form input {
  flex: 1; min-width: 0; border: 1px solid rgba(255,255,255,0.35); background: rgba(255,255,255,0.9);
  border-radius: 12px; padding: 0.7rem 0.9rem; font-family: inherit; font-size: 0.9rem; color: #111;
}
.news-form input::placeholder { color: #999; }
.news-form input:focus { outline: 2px solid #fff; }
.news-form button {
  width: 46px; flex-shrink: 0; background: #fff; color: #f5576c; border: none; border-radius: 12px;
  font-size: 1rem; cursor: pointer; transition: all 0.25s ease;
}
.news-form button:hover { background: #f5576c; color: #fff; }
.newsletter.done { background: rgba(255,255,255,0.9); }
.news-thanks { display: flex; align-items: center; gap: 0.75rem; text-align: left; color: #f5576c; }
.news-thanks i { font-size: 1.6rem; }
.news-thanks strong { display: block; color: #111; font-size: 0.95rem; }
.news-thanks span { color: #555; font-size: 0.82rem; }

.socials {
  display: flex;
  justify-content: center;
  gap: 1.25rem;
  margin: 2rem 0 0.5rem;
}
.socials a {
  width: 45px; height: 45px; background: rgba(255,255,255,0.2); border-radius: 50%; display: flex; justify-content: center; align-items: center; color: #fff; font-size: 1.2rem; transition: all 0.3s ease; border: 1px solid rgba(255,255,255,0.1);
}
.socials a:hover { transform: translateY(-5px); background: rgba(255,255,255,0.4); box-shadow: 0 10px 20px rgba(0,0,0,0.1); }

.footer { padding: 2rem; text-align: center; color: rgba(255,255,255,0.7); font-size: 0.9rem; border-top: 1px solid rgba(255,255,255,0.1); margin-top: 1.5rem; }
.footer strong { color: #fff; font-weight: 800; }

@media (max-width: 420px) {
  .content-section { padding: 1.25rem 1.25rem 1.5rem; }
  .profile-section { padding: 0 1.25rem; }
  .preview-cards { grid-template-columns: 1fr; }
}
</style>
