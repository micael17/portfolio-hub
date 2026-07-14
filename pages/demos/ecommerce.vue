<template>
  <div class="ecommerce">
    <header class="navbar">
      <div class="nav-left">
        <a href="#products">Shop</a>
        <a href="#story">Collections</a>
      </div>
      <div class="logo">ESSENTIALS.</div>
      <div class="nav-right">
        <a href="#faq">Help</a>
        <a href="#products" class="cart-link">
          Cart <span class="cart-badge">{{ cart }}</span>
        </a>
      </div>
    </header>

    <section class="hero">
      <!-- AI-IMG: 미니멀 라이프스타일 브랜드 히어로, 자연광 아래 뉴트럴 톤 의류/오브제, 따뜻하고 차분한 무드 · 16:9 -->
      <img src="https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=1600&q=80" alt="따뜻한 자연광이 비치는 미니멀 라이프스타일 매장 전경">
      <div class="hero-text">
        <p class="hero-kicker">2026 Spring Collection</p>
        <h2>The New Standard.</h2>
        <p class="hero-sub">일상을 위한 견고한 기본. 오래 두고 쓰는 물건들.</p>
        <a href="#products" class="shop-btn">Shop Collection</a>
      </div>
    </section>

    <section class="products" id="products">
      <div class="section-title">
        <h3>All Products</h3>
        <a href="#story">View Story</a>
      </div>

      <div class="filters" role="tablist" aria-label="상품 카테고리 필터">
        <button
          v-for="c in categories"
          :key="c.value"
          class="filter-btn"
          :class="{ active: filter === c.value }"
          role="tab"
          :aria-selected="filter === c.value"
          @click="filter = c.value"
        >
          {{ c.label }}
        </button>
      </div>

      <div class="grid">
        <!-- AI-IMG: 라이프스타일 제품 컷, 미니멀·따뜻한 뉴트럴 톤, 스튜디오 자연광 · 1:1 (상품별 프롬프트는 products 배열 item.prompt 참조) -->
        <div class="p-card" v-for="p in filteredProducts" :key="p.id">
          <div class="img-box">
            <span v-if="p.tag" class="p-tag" :class="p.tag.toLowerCase()">{{ p.tag }}</span>
            <img :src="p.img" :alt="p.alt">
          </div>
          <div class="p-info">
            <div class="p-meta">
              <h4>{{ p.name }}</h4>
              <p class="p-cat">{{ categoryLabel(p.category) }}</p>
            </div>
            <span class="p-price">{{ p.price }}</span>
          </div>
          <button class="add-btn" @click="addCart(p)">Add to Cart</button>
        </div>
      </div>

      <p v-if="filteredProducts.length === 0" class="empty">
        해당 카테고리의 상품이 곧 입고됩니다.
      </p>
    </section>

    <section class="bestsellers">
      <div class="section-title">
        <h3>Best Sellers</h3>
        <span class="section-note">이번 주 가장 많이 담은 제품</span>
      </div>
      <div class="best-grid">
        <div class="best-card" v-for="p in bestSellers" :key="p.id">
          <div class="best-rank">{{ p.rank }}</div>
          <div class="best-img">
            <!-- AI-IMG: 베스트셀러 제품 클로즈업, 질감이 드러나는 뉴트럴 톤 · 4:3 (상품별 프롬프트는 bestSellers 배열 item.prompt 참조) -->
            <img :src="p.img" :alt="p.alt">
          </div>
          <div class="best-info">
            <h4>{{ p.name }}</h4>
            <span>{{ p.price }}</span>
          </div>
        </div>
      </div>
    </section>

    <section class="reviews" aria-label="고객 후기">
      <div class="section-title">
        <h3>Customer Reviews</h3>
        <span class="section-note">평점 4.8 / 5.0 · 리뷰 1,204건</span>
      </div>
      <div class="review-grid">
        <blockquote class="review-card" v-for="r in reviews" :key="r.id">
          <div class="stars" :aria-label="`별점 ${r.rating}점 만점 5점`">
            <span v-for="n in 5" :key="n" :class="{ filled: n <= r.rating }">★</span>
          </div>
          <p class="review-text">"{{ r.text }}"</p>
          <footer class="review-author">
            <strong>{{ r.author }}</strong>
            <span>{{ r.product }}</span>
          </footer>
        </blockquote>
      </div>
    </section>

    <section class="story" id="story">
      <div class="story-img">
        <!-- AI-IMG: 브랜드 스토리 이미지, 소재를 다듬는 장인의 손 또는 워크숍, 따뜻하고 절제된 톤 · 3:4 -->
        <img src="https://images.unsplash.com/photo-1523381210434-271e8be1f52b?w=800&q=80" alt="자연 소재를 손질하는 브랜드 워크숍 장면">
      </div>
      <div class="story-text">
        <p class="story-kicker">Our Story</p>
        <h3>덜 만들고, 오래 쓰이도록.</h3>
        <p>
          ESSENTIALS.는 2019년 서울의 작은 작업실에서 시작했습니다.
          유행을 좇는 대신, 매일 손이 가는 물건을 만듭니다.
          검증된 소재와 절제된 디자인으로, 계절이 바뀌어도 곁에 남는 기본을 지향합니다.
        </p>
        <p>
          모든 제품은 국내외 인증 공방과 협업하며, 남는 원단은 재사용해
          폐기물을 최소화합니다.
        </p>
      </div>
    </section>

    <section class="policy" aria-label="배송 및 교환 안내">
      <div class="policy-item">
        <h4>무료 배송</h4>
        <p>5만원 이상 주문 시 전국 무료 배송. 오후 2시 이전 결제 건은 당일 출고됩니다.</p>
      </div>
      <div class="policy-item">
        <h4>교환 &amp; 반품</h4>
        <p>수령 후 14일 이내 무료 교환·반품. 택 제거·착용 흔적이 없는 상태여야 합니다.</p>
      </div>
      <div class="policy-item">
        <h4>품질 보증</h4>
        <p>봉제·소재 하자는 구매 후 1년간 무상 수선해 드립니다.</p>
      </div>
    </section>

    <section class="faq" id="faq">
      <div class="section-title">
        <h3>FAQ</h3>
      </div>
      <div class="faq-list">
        <div class="faq-item" v-for="(f, i) in faqs" :key="i">
          <button
            class="faq-q"
            :aria-expanded="openFaq === i"
            :aria-controls="`faq-panel-${i}`"
            @click="toggleFaq(i)"
          >
            <span>{{ f.q }}</span>
            <span class="faq-icon" aria-hidden="true">{{ openFaq === i ? '−' : '+' }}</span>
          </button>
          <div
            class="faq-a"
            :id="`faq-panel-${i}`"
            v-show="openFaq === i"
            role="region"
          >
            <p>{{ f.a }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="newsletter">
      <h3>Join the list.</h3>
      <p>신제품 소식과 회원 전용 혜택을 가장 먼저 받아보세요.</p>
      <form class="news-form" @submit.prevent="subscribe">
        <label class="sr-only" for="news-email">이메일 주소</label>
        <input
          id="news-email"
          v-model="email"
          type="email"
          placeholder="you@example.com"
          required
        >
        <button type="submit">Subscribe</button>
      </form>
      <p v-if="subscribed" class="news-ok" role="status">
        구독이 완료됐습니다. 곧 첫 소식을 보내드릴게요.
      </p>
    </section>

    <footer>
      <p>ESSENTIALS. &copy; 2026</p>
    </footer>
  </div>
</template>

<script setup>
useHead({ title: 'Essentials | E-Commerce' })
definePageMeta({ layout: false })

const categories = [
  { value: 'all', label: '전체' },
  { value: 'apparel', label: '의류' },
  { value: 'living', label: '리빙' },
  { value: 'beauty', label: '뷰티' }
]

const products = [
  {
    id: 1,
    name: 'Cotton Basic Tee',
    category: 'apparel',
    price: '₩45,000',
    tag: 'BEST',
    img: 'https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=400&q=80',
    alt: '뉴트럴 톤 코튼 베이직 티셔츠 제품 컷',
    prompt: '오프화이트 코튼 반팔 티셔츠, 접힌 상태, 밝은 스튜디오 배경 · 1:1'
  },
  {
    id: 2,
    name: 'Utility Jacket',
    category: 'apparel',
    price: '₩120,000',
    tag: 'NEW',
    img: 'https://images.unsplash.com/photo-1591047139829-d91aecb6caea?w=400&q=80',
    alt: '카키 유틸리티 재킷 제품 컷',
    prompt: '카키 유틸리티 재킷, 옷걸이에 걸린 정면 컷, 뉴트럴 배경 · 1:1'
  },
  {
    id: 3,
    name: 'Canvas Sneakers',
    category: 'apparel',
    price: '₩85,000',
    tag: '',
    img: 'https://images.unsplash.com/photo-1588099768531-a72d4a198538?w=400&q=80',
    alt: '아이보리 캔버스 스니커즈 제품 컷',
    prompt: '아이보리 캔버스 스니커즈 한 켤레, 위에서 내려다본 컷 · 1:1'
  },
  {
    id: 4,
    name: 'Leather Tote',
    category: 'living',
    price: '₩210,000',
    tag: 'BEST',
    img: 'https://images.unsplash.com/photo-1543163521-1bf539c55dd2?w=400&q=80',
    alt: '탄 컬러 가죽 토트백 제품 컷',
    prompt: '탄 컬러 미니멀 가죽 토트백, 정면 스탠딩 컷 · 1:1'
  },
  {
    id: 5,
    name: 'Linen Throw Blanket',
    category: 'living',
    price: '₩68,000',
    tag: 'NEW',
    img: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e6?w=400&q=80',
    alt: '오트밀 색 리넨 담요가 소파에 놓인 컷',
    prompt: '오트밀 톤 리넨 담요, 나무 의자에 자연스럽게 걸친 컷 · 1:1'
  },
  {
    id: 6,
    name: 'Ceramic Mug Set',
    category: 'living',
    price: '₩39,000',
    tag: '',
    img: 'https://images.unsplash.com/photo-1514228742587-6b1558fcca3d?w=400&q=80',
    alt: '뉴트럴 톤 세라믹 머그 세트 제품 컷',
    prompt: '핸드메이드 세라믹 머그 2개, 뉴트럴 톤, 나무 테이블 위 · 1:1'
  },
  {
    id: 7,
    name: 'Hand Cream Duo',
    category: 'beauty',
    price: '₩29,000',
    tag: 'BEST',
    img: 'https://images.unsplash.com/photo-1556228578-8c89e6adf883?w=400&q=80',
    alt: '미니멀 패키지 핸드크림 듀오 제품 컷',
    prompt: '미니멀 튜브 핸드크림 2종, 뉴트럴 배경 플랫레이 · 1:1'
  },
  {
    id: 8,
    name: 'Botanical Candle',
    category: 'beauty',
    price: '₩34,000',
    tag: 'NEW',
    img: 'https://images.unsplash.com/photo-1602874801007-bd458bb1b8b6?w=400&q=80',
    alt: '유리 용기에 담긴 보태니컬 향초 제품 컷',
    prompt: '유리 용기 보태니컬 향초, 은은한 자연광, 뉴트럴 톤 · 1:1'
  }
]

const bestSellers = [
  {
    id: 1,
    rank: '01',
    name: 'Cotton Basic Tee',
    price: '₩45,000',
    img: 'https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=600&q=80',
    alt: '베스트셀러 1위 코튼 베이직 티셔츠',
    prompt: '오프화이트 코튼 티셔츠 클로즈업, 질감 강조 · 4:3'
  },
  {
    id: 4,
    rank: '02',
    name: 'Leather Tote',
    price: '₩210,000',
    img: 'https://images.unsplash.com/photo-1543163521-1bf539c55dd2?w=600&q=80',
    alt: '베스트셀러 2위 가죽 토트백',
    prompt: '탄 컬러 가죽 토트백 질감 클로즈업 · 4:3'
  },
  {
    id: 7,
    rank: '03',
    name: 'Hand Cream Duo',
    price: '₩29,000',
    img: 'https://images.unsplash.com/photo-1556228578-8c89e6adf883?w=600&q=80',
    alt: '베스트셀러 3위 핸드크림 듀오',
    prompt: '핸드크림 튜브 클로즈업, 미니멀 패키지 · 4:3'
  }
]

const reviews = [
  {
    id: 1,
    rating: 5,
    text: '기본 티셔츠라고 하기엔 원단이 너무 좋아요. 세탁 여러 번 해도 목이 늘어나지 않네요.',
    author: '김서연',
    product: 'Cotton Basic Tee'
  },
  {
    id: 2,
    rating: 4,
    text: '토트백 가죽 질감이 사진보다 훨씬 고급스러워요. 수납도 넉넉해서 매일 들고 다닙니다.',
    author: '이준호',
    product: 'Leather Tote'
  },
  {
    id: 3,
    rating: 5,
    text: '향초 향이 과하지 않고 은은해서 좋아요. 재구매 의사 100%입니다.',
    author: '박민지',
    product: 'Botanical Candle'
  }
]

const faqs = [
  {
    q: '배송은 얼마나 걸리나요?',
    a: '오후 2시 이전 결제 건은 당일 출고되며, 일반적으로 1~2일 내 수령하실 수 있습니다. 도서·산간 지역은 1일 정도 더 소요됩니다.'
  },
  {
    q: '교환이나 반품은 어떻게 하나요?',
    a: '상품 수령 후 14일 이내라면 마이페이지에서 신청하실 수 있습니다. 택 제거나 착용 흔적이 없는 경우 무료로 처리됩니다.'
  },
  {
    q: '재입고 알림을 받을 수 있나요?',
    a: '품절 상품 페이지의 재입고 알림 신청 버튼을 누르시면, 입고 시 이메일로 안내해 드립니다.'
  },
  {
    q: '오프라인 매장이 있나요?',
    a: '서울 성수동에 플래그십 쇼룸을 운영하고 있습니다. 온라인 판매 제품 대부분을 직접 보고 구매하실 수 있습니다.'
  },
  {
    q: '세탁·관리 방법은 어디서 확인하나요?',
    a: '각 상품 상세 페이지 하단과 동봉된 케어 카드에 소재별 관리법을 안내하고 있습니다.'
  }
]

const filter = ref('all')
const cart = ref(0)
const openFaq = ref(-1)
const email = ref('')
const subscribed = ref(false)

const filteredProducts = computed(() =>
  filter.value === 'all'
    ? products
    : products.filter(p => p.category === filter.value)
)

function categoryLabel(value) {
  const found = categories.find(c => c.value === value)
  return found ? found.label : value
}

function addCart() {
  cart.value += 1
}

function toggleFaq(i) {
  openFaq.value = openFaq.value === i ? -1 : i
}

function subscribe() {
  if (!email.value) return
  subscribed.value = true
  email.value = ''
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap');

.ecommerce {
  font-family: 'Inter', sans-serif;
  color: #000;
  background: #fff;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 3rem;
  border-bottom: 1px solid #000;
  position: sticky;
  top: 0;
  background: #fff;
  z-index: 100;
}

.logo {
  font-size: 1.5rem;
  font-weight: 800;
  letter-spacing: -1px;
}

.nav-left, .nav-right {
  display: flex;
  gap: 2rem;
  flex: 1;
}

.nav-right {
  justify-content: flex-end;
}

.navbar a {
  text-decoration: none;
  color: #000;
  font-weight: 600;
  font-size: 0.9rem;
  text-transform: uppercase;
}

.cart-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

.cart-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 1.4rem;
  height: 1.4rem;
  padding: 0 0.4rem;
  background: #000;
  color: #fff;
  border-radius: 999px;
  font-size: 0.75rem;
  font-weight: 800;
}

.hero {
  position: relative;
  height: 80vh;
  border-bottom: 1px solid #000;
}

.hero img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  background: #fff;
  padding: 3rem 4rem;
  border: 1px solid #000;
  max-width: 90%;
}

.hero-kicker {
  text-transform: uppercase;
  letter-spacing: 2px;
  font-size: 0.75rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.hero-text h2 {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 1rem;
  letter-spacing: -2px;
}

.hero-sub {
  font-size: 0.95rem;
  color: #444;
  margin-bottom: 2rem;
}

.shop-btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 1rem 3rem;
  font-weight: 600;
  text-transform: uppercase;
  cursor: pointer;
  transition: opacity 0.3s;
  text-decoration: none;
  font-size: 0.9rem;
}

.shop-btn:hover {
  opacity: 0.8;
}

.products {
  padding: 5rem 3rem;
}

.section-title {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 2rem;
  border-bottom: 1px solid #000;
  padding-bottom: 1rem;
  gap: 1rem;
  flex-wrap: wrap;
}

.section-title h3 {
  font-size: 2rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: -1px;
}

.section-title a {
  color: #000;
  font-weight: 600;
  text-decoration: underline;
}

.section-note {
  font-size: 0.85rem;
  color: #444;
  font-weight: 600;
}

.filters {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.filter-btn {
  background: #fff;
  color: #000;
  border: 1px solid #000;
  padding: 0.55rem 1.5rem;
  font-family: inherit;
  font-weight: 600;
  font-size: 0.85rem;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}

.filter-btn.active,
.filter-btn:hover {
  background: #000;
  color: #fff;
}

.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
}

.p-card {
  display: flex;
  flex-direction: column;
}

.img-box {
  position: relative;
  border: 1px solid #000;
  height: 360px;
  margin-bottom: 1rem;
  overflow: hidden;
}

.img-box img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s;
}

.p-card:hover .img-box img {
  transform: scale(1.05);
}

.p-tag {
  position: absolute;
  top: 0.75rem;
  left: 0.75rem;
  z-index: 2;
  padding: 0.3rem 0.7rem;
  font-size: 0.7rem;
  font-weight: 800;
  letter-spacing: 1px;
  background: #000;
  color: #fff;
}

.p-tag.new {
  background: #fff;
  color: #000;
  border: 1px solid #000;
}

.p-info {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 0.75rem;
}

.p-info h4 {
  font-size: 1rem;
  font-weight: 600;
}

.p-cat {
  font-size: 0.75rem;
  color: #777;
  margin-top: 0.2rem;
}

.p-price {
  font-weight: 800;
  white-space: nowrap;
}

.add-btn {
  margin-top: auto;
  background: #fff;
  color: #000;
  border: 1px solid #000;
  padding: 0.75rem;
  font-family: inherit;
  font-weight: 600;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}

.add-btn:hover {
  background: #000;
  color: #fff;
}

.empty {
  text-align: center;
  padding: 3rem;
  color: #555;
}

.bestsellers {
  padding: 5rem 3rem;
  background: #f6f6f4;
  border-top: 1px solid #000;
}

.best-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.best-card {
  position: relative;
  background: #fff;
  border: 1px solid #000;
}

.best-rank {
  position: absolute;
  top: 0.75rem;
  left: 0.75rem;
  z-index: 2;
  font-size: 1.2rem;
  font-weight: 800;
  background: #000;
  color: #fff;
  padding: 0.2rem 0.6rem;
}

.best-img {
  height: 280px;
  overflow: hidden;
  border-bottom: 1px solid #000;
}

.best-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.best-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 1.25rem;
}

.best-info h4 {
  font-size: 1rem;
  font-weight: 600;
}

.best-info span {
  font-weight: 800;
}

.reviews {
  padding: 5rem 3rem;
}

.review-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.review-card {
  border: 1px solid #000;
  padding: 2rem;
  margin: 0;
}

.stars {
  font-size: 1.1rem;
  letter-spacing: 2px;
  margin-bottom: 1rem;
  color: #ccc;
}

.stars .filled {
  color: #000;
}

.review-text {
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.review-author {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
}

.review-author strong {
  font-weight: 800;
}

.review-author span {
  font-size: 0.8rem;
  color: #777;
}

.story {
  display: grid;
  grid-template-columns: 1fr 1fr;
  border-top: 1px solid #000;
}

.story-img {
  height: 100%;
  min-height: 420px;
  border-right: 1px solid #000;
  overflow: hidden;
}

.story-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.story-text {
  padding: 4rem 3rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.story-kicker {
  text-transform: uppercase;
  letter-spacing: 2px;
  font-size: 0.75rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.story-text h3 {
  font-size: 2rem;
  font-weight: 800;
  letter-spacing: -1px;
  margin-bottom: 1.5rem;
}

.story-text p {
  font-size: 0.95rem;
  line-height: 1.7;
  color: #333;
  margin-bottom: 1rem;
}

.policy {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  border-top: 1px solid #000;
}

.policy-item {
  padding: 3rem;
  border-right: 1px solid #000;
}

.policy-item:last-child {
  border-right: none;
}

.policy-item h4 {
  font-size: 1.1rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 1rem;
}

.policy-item p {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #333;
}

.faq {
  padding: 5rem 3rem;
  border-top: 1px solid #000;
}

.faq-list {
  border-top: 1px solid #000;
}

.faq-item {
  border-bottom: 1px solid #000;
}

.faq-q {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem 0;
  background: none;
  border: none;
  font-family: inherit;
  font-size: 1.05rem;
  font-weight: 600;
  text-align: left;
  cursor: pointer;
  color: #000;
}

.faq-icon {
  font-size: 1.5rem;
  font-weight: 400;
  line-height: 1;
}

.faq-a {
  padding: 0 0 1.5rem;
}

.faq-a p {
  font-size: 0.95rem;
  line-height: 1.7;
  color: #333;
  max-width: 70ch;
}

.newsletter {
  padding: 5rem 3rem;
  text-align: center;
  background: #000;
  color: #fff;
}

.newsletter h3 {
  font-size: 2rem;
  font-weight: 800;
  letter-spacing: -1px;
  margin-bottom: 0.75rem;
}

.newsletter > p {
  font-size: 0.95rem;
  color: #ccc;
  margin-bottom: 2rem;
}

.news-form {
  display: flex;
  gap: 0;
  max-width: 480px;
  margin: 0 auto;
}

.news-form input {
  flex: 1;
  padding: 1rem 1.25rem;
  border: 1px solid #fff;
  background: #000;
  color: #fff;
  font-family: inherit;
  font-size: 0.95rem;
}

.news-form input::placeholder {
  color: #999;
}

.news-form button {
  padding: 1rem 2rem;
  background: #fff;
  color: #000;
  border: 1px solid #fff;
  font-family: inherit;
  font-weight: 600;
  text-transform: uppercase;
  cursor: pointer;
  transition: opacity 0.3s;
}

.news-form button:hover {
  opacity: 0.85;
}

.news-ok {
  margin-top: 1.5rem;
  font-size: 0.9rem;
  color: #fff;
}

footer {
  text-align: center;
  padding: 3rem;
  border-top: 1px solid #000;
  font-weight: 800;
  font-size: 1.2rem;
}

@media (max-width: 1024px) {
  .grid { grid-template-columns: repeat(3, 1fr); }
}

@media (max-width: 768px) {
  .navbar { padding: 1.25rem 1.5rem; }
  .nav-left { display: none; }
  .products, .bestsellers, .reviews, .faq, .newsletter { padding: 3rem 1.5rem; }
  .grid { grid-template-columns: repeat(2, 1fr); }
  .best-grid, .review-grid { grid-template-columns: 1fr; }
  .hero-text { padding: 2rem; }
  .hero-text h2 { font-size: 2rem; }
  .story { grid-template-columns: 1fr; }
  .story-img { border-right: none; border-bottom: 1px solid #000; min-height: 320px; }
  .story-text { padding: 3rem 1.5rem; }
  .policy { grid-template-columns: 1fr; }
  .policy-item { border-right: none; border-bottom: 1px solid #000; padding: 2rem 1.5rem; }
  .policy-item:last-child { border-bottom: none; }
}

@media (max-width: 480px) {
  .grid { grid-template-columns: 1fr; }
  .img-box { height: 320px; }
}
</style>
