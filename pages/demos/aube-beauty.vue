<template>
  <div class="aube">
    <CommerceAdminAdminDemoLink to="/demos/commerce-admin/aube" />
    <div class="announcement">COMPLIMENTARY SHIPPING ON ORDERS OVER ₩50,000</div>
    <header class="nav">
      <button class="menu" aria-label="메뉴 열기">MENU</button>
      <a href="#" class="wordmark">AUBE<span>°</span></a>
      <nav>
        <a href="#ritual">Ritual</a>
        <a href="#journal">Journal</a>
        <button class="bag" @click="cartOpen = true">Bag ({{ cartCount }})</button>
      </nav>
    </header>

    <main>
      <section class="hero">
        <img src="https://images.unsplash.com/photo-1556228720-195a672e8a03?auto=format&fit=crop&w=1800&q=90" alt="자연광 속 스킨케어 제품과 식물">
        <div class="hero-copy">
          <p>BOTANICAL SKINCARE · SEOUL</p>
          <h1>Skin, in its<br><em>quiet state.</em></h1>
          <a href="#ritual">Explore the ritual <span>↗</span></a>
        </div>
        <div class="hero-index">01 / 03</div>
      </section>

      <section class="intro">
        <p class="eyebrow">OUR PHILOSOPHY</p>
        <h2>피부가 스스로 균형을 찾도록.<br>우리는 필요한 것만 남깁니다.</h2>
        <p class="intro-body">제주의 식물과 피부 과학을 결합한 저자극 포뮬러. 매일 반복할 수 있는 단순하고 온전한 리추얼을 제안합니다.</p>
      </section>

      <section id="ritual" class="shop">
        <div class="section-head">
          <div><p class="eyebrow">THE DAILY RITUAL</p><h2>Essentials</h2></div>
          <div class="tabs" role="tablist">
            <button v-for="tab in tabs" :key="tab" :class="{ active: activeTab === tab }" @click="activeTab = tab">{{ tab }}</button>
          </div>
        </div>
        <div class="product-grid">
          <article v-for="product in visibleProducts" :key="product.name" class="product">
            <div class="product-image">
              <span v-if="product.badge">{{ product.badge }}</span>
              <img :src="product.image" :alt="product.name">
              <button @click="addToCart(product)">QUICK ADD +</button>
            </div>
            <div class="product-info">
              <div><h3>{{ product.name }}</h3><p>{{ product.desc }}</p></div>
              <strong>{{ product.price }}</strong>
            </div>
          </article>
        </div>
      </section>

      <section class="ingredient">
        <div class="ingredient-copy">
          <p class="eyebrow">INGREDIENT NO. 07</p>
          <h2>Camellia<br>Japonica</h2>
          <p>차가운 바닷바람을 견디며 자란 동백의 씨앗에는 피부 장벽을 위한 오메가 지방산이 풍부합니다. 저온 압착으로 천천히, 유효 성분을 온전히 담았습니다.</p>
          <a href="#journal">Discover our ingredients →</a>
        </div>
        <div class="ingredient-image">
          <img src="https://images.unsplash.com/photo-1497250681960-ef046c08a56e?auto=format&fit=crop&w=1100&q=85" alt="짙은 초록빛 동백 잎">
          <div class="note">HARVESTED<br>IN JEJU</div>
        </div>
      </section>

      <section id="journal" class="quote">
        <span>“</span>
        <blockquote>좋은 스킨케어는 더하는 일이 아니라,<br>피부가 편안해질 때까지 덜어내는 일.</blockquote>
        <p>— AUBE LAB, SEOUL 2026</p>
      </section>

      <section class="newsletter">
        <p class="eyebrow">A LETTER FROM AUBE</p>
        <h2>Slow notes for your skin.</h2>
        <form @submit.prevent="subscribed = true">
          <input v-model="email" type="email" required placeholder="Email address" aria-label="이메일 주소">
          <button>{{ subscribed ? 'THANK YOU' : 'SUBSCRIBE ↗' }}</button>
        </form>
      </section>
    </main>

    <footer><a class="wordmark" href="#">AUBE<span>°</span></a><p>SEOUL · JEJU<br>© 2026 AUBE LAB</p><div><a href="#">Instagram</a><a href="#">Customer care</a><NuxtLink to="/demos/commerce-admin/aube">Admin Preview ↗</NuxtLink></div></footer>

    <Transition name="drawer">
      <div v-if="cartOpen" class="cart-layer" @click.self="cartOpen = false">
        <aside>
          <div class="cart-head"><h2>Your bag</h2><button @click="cartOpen = false">CLOSE ×</button></div>
          <div v-if="cartItems.length" class="cart-items">
            <div v-for="item in cartItems" :key="item.name"><img :src="item.image" :alt="item.name"><p>{{ item.name }}<br><strong>{{ item.price }}</strong></p></div>
          </div>
          <p v-else class="empty">Your ritual is waiting.</p>
          <button v-if="cartItems.length" class="checkout">CHECKOUT · {{ total }}</button>
        </aside>
      </div>
    </Transition>
  </div>
</template>

<script setup>
useHead({ title: 'AUBE — Botanical Skincare' })
definePageMeta({ layout: false })

const tabs = ['ALL', 'CLEANSE', 'TREAT', 'MOISTURE']
const activeTab = ref('ALL')
const cartOpen = ref(false)
const cartItems = ref([])
const email = ref('')
const subscribed = ref(false)

const products = [
  { name: 'Dew Cleanser', desc: 'Rice water · 150 ml', price: '₩32,000', category: 'CLEANSE', badge: 'BESTSELLER', image: 'https://images.unsplash.com/photo-1556228578-8c89e6adf883?auto=format&fit=crop&w=800&q=85' },
  { name: 'Quiet Serum', desc: 'Camellia · 30 ml', price: '₩48,000', category: 'TREAT', badge: 'NEW', image: 'https://images.unsplash.com/photo-1608248597279-f99d160bfcbc?auto=format&fit=crop&w=800&q=85' },
  { name: 'Barrier Cream', desc: 'Ceramide · 50 ml', price: '₩42,000', category: 'MOISTURE', image: 'https://images.unsplash.com/photo-1611930022073-b7a4ba5fcccd?auto=format&fit=crop&w=800&q=85' },
  { name: 'Night Oil', desc: 'Jeju camellia · 30 ml', price: '₩56,000', category: 'TREAT', image: 'https://images.unsplash.com/photo-1608571423902-eed4a5ad8108?auto=format&fit=crop&w=800&q=85' }
]
const visibleProducts = computed(() => activeTab.value === 'ALL' ? products : products.filter(p => p.category === activeTab.value))
const cartCount = computed(() => cartItems.value.length)
const total = computed(() => `₩${cartItems.value.reduce((sum, p) => sum + Number(p.price.replace(/\D/g, '')), 0).toLocaleString()}`)
function addToCart(product) { cartItems.value.push(product); cartOpen.value = true }
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=Italiana&display=swap');
:global(*){box-sizing:border-box}.aube{width:100vw;margin-left:calc(50% - 50vw);font-family:'DM Sans','Pretendard',sans-serif;background:#eee9df;color:#173b2b;min-height:100vh}.announcement{height:30px;background:#173b2b;color:#eee9df;text-align:center;font-size:10px;letter-spacing:2px;padding:8px}.nav{height:82px;display:grid;grid-template-columns:1fr auto 1fr;align-items:center;padding:0 3.5vw;border-bottom:1px solid rgba(23,59,43,.35);position:absolute;top:30px;z-index:4;width:100%;color:white}.nav a,.nav button{color:inherit}.menu{display:none}.wordmark{font:48px/1 'Italiana',serif;letter-spacing:-2px;text-decoration:none}.wordmark span{font:18px 'DM Sans';vertical-align:top}.nav nav{display:flex;justify-content:flex-end;gap:30px;align-items:center}.nav nav a,.nav button{background:0;border:0;text-decoration:none;text-transform:uppercase;font:10px 'DM Sans';letter-spacing:1.5px;cursor:pointer}.hero{height:calc(100vh - 30px);min-height:650px;position:relative;color:white;overflow:hidden}.hero>img{width:100%;height:100%;object-fit:cover;filter:brightness(.7)}.hero-copy{position:absolute;left:7vw;bottom:10vh}.hero-copy p,.eyebrow{font-size:10px;letter-spacing:2.3px;font-weight:600}.hero h1{font:clamp(60px,8.5vw,130px)/.84 'Italiana',serif;letter-spacing:-4px;margin:24px 0 36px}.hero h1 em{font-weight:400}.hero-copy a{color:white;text-decoration:none;border-bottom:1px solid;padding-bottom:8px;font-size:12px;letter-spacing:1px}.hero-copy a span{margin-left:60px}.hero-index{position:absolute;right:3.5vw;bottom:4vh;font-size:10px;letter-spacing:2px}.intro{padding:140px 8vw 160px;display:grid;grid-template-columns:1fr 3fr;gap:30px}.intro h2{font:clamp(36px,4.5vw,70px)/1.22 'Italiana',serif;letter-spacing:-1px;max-width:1000px}.intro-body{grid-column:2;max-width:520px;margin:45px 0 0 40%;font-size:14px;line-height:1.9;color:#496255}.shop{padding:0 3.5vw 140px}.section-head{display:flex;justify-content:space-between;align-items:end;border-bottom:1px solid #173b2b;padding-bottom:25px}.section-head h2{font:64px 'Italiana';margin-top:8px}.tabs{display:flex;gap:22px}.tabs button{border:0;background:none;color:#6c7e73;font-size:10px;letter-spacing:1px;padding:7px 0;cursor:pointer}.tabs button.active{color:#173b2b;border-bottom:1px solid}.product-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-top:24px}.product-image{height:480px;position:relative;overflow:hidden;background:#ddd5c7}.product-image img{width:100%;height:100%;object-fit:cover;transition:.6s}.product:hover img{transform:scale(1.03)}.product-image>span{position:absolute;z-index:1;top:15px;left:15px;background:#eee9df;padding:7px 9px;font-size:8px;letter-spacing:1px}.product-image button{position:absolute;bottom:12px;left:12px;right:12px;padding:14px;border:0;background:#eee9df;color:#173b2b;font-size:9px;letter-spacing:1.5px;opacity:0;transform:translateY(5px);transition:.25s;cursor:pointer}.product:hover .product-image button{opacity:1;transform:none}.product-info{display:flex;justify-content:space-between;padding:16px 2px}.product-info h3{font:22px 'Italiana';margin-bottom:5px}.product-info p,.product-info strong{font-size:10px;font-weight:500;color:#65786d}.ingredient{display:grid;grid-template-columns:42% 58%;background:#173b2b;color:#eee9df;min-height:730px}.ingredient-copy{padding:9vw 8vw}.ingredient-copy h2{font:clamp(60px,7vw,105px)/.9 'Italiana';margin:40px 0}.ingredient-copy>p:not(.eyebrow){font-size:13px;line-height:2;max-width:390px;color:#c2cec6}.ingredient-copy a{display:inline-block;margin-top:50px;color:inherit;text-decoration:none;border-bottom:1px solid;padding-bottom:8px;font-size:11px}.ingredient-image{position:relative}.ingredient-image img{width:100%;height:100%;object-fit:cover;filter:saturate(.7)}.note{position:absolute;right:30px;bottom:30px;background:#eee9df;color:#173b2b;width:105px;height:105px;border-radius:50%;display:grid;place-items:center;text-align:center;font-size:9px;letter-spacing:1px}.quote{text-align:center;padding:170px 5vw}.quote>span{font:90px 'Italiana';line-height:.6}.quote blockquote{font:clamp(32px,4vw,58px)/1.4 'Italiana';margin:30px auto;max-width:1000px}.quote p{font-size:9px;letter-spacing:2px}.newsletter{background:#d8c6a7;padding:100px 7vw;display:grid;grid-template-columns:1fr 1.5fr;align-items:end}.newsletter h2{font:clamp(45px,6vw,85px)/1 'Italiana';grid-row:2}.newsletter form{grid-column:2;grid-row:2;display:flex;border-bottom:1px solid;padding-bottom:12px}.newsletter input{flex:1;border:0;background:none;font:22px 'Italiana';outline:0;color:#173b2b}.newsletter button{border:0;background:none;font-size:10px;letter-spacing:1px;color:#173b2b}footer{background:#d8c6a7;border-top:1px solid rgba(23,59,43,.3);padding:50px 3.5vw;display:flex;align-items:end;justify-content:space-between}footer p,footer a{font-size:9px;line-height:2;letter-spacing:1px;color:#173b2b;text-decoration:none}footer>div{display:flex;gap:25px}.cart-layer{position:fixed;z-index:20;inset:0;background:rgba(0,0,0,.35);display:flex;justify-content:flex-end}.cart-layer aside{width:min(460px,100%);height:100%;background:#eee9df;padding:30px;display:flex;flex-direction:column}.cart-head{display:flex;justify-content:space-between;border-bottom:1px solid;padding-bottom:20px}.cart-head h2{font:36px 'Italiana'}.cart-head button{border:0;background:none;font-size:9px}.cart-items{overflow:auto}.cart-items>div{display:flex;gap:16px;padding:18px 0;border-bottom:1px solid #b9b4aa}.cart-items img{width:80px;height:100px;object-fit:cover}.cart-items p{font:18px/1.8 'Italiana'}.empty{margin:auto;text-align:center;font:30px 'Italiana'}.checkout{margin-top:auto;background:#173b2b;color:#eee9df;border:0;padding:18px;letter-spacing:1px}.drawer-enter-active,.drawer-leave-active{transition:.3s}.drawer-enter-from,.drawer-leave-to{opacity:0}.drawer-enter-from aside,.drawer-leave-to aside{transform:translateX(100%)}
@media(max-width:800px){.nav{height:65px;padding:0 20px}.menu{display:block!important}.nav nav a{display:none}.nav nav{gap:0}.wordmark{font-size:34px}.hero{min-height:620px}.hero-copy{left:24px;bottom:80px}.hero h1{font-size:60px;letter-spacing:-2px}.intro{padding:90px 24px;display:block}.intro h2{font-size:38px;margin:25px 0}.intro-body{margin:0}.shop{padding:0 16px 90px}.section-head{display:block}.section-head h2{font-size:48px}.tabs{overflow:auto;margin-top:25px}.product-grid{grid-template-columns:repeat(2,1fr);gap:8px}.product-image{height:270px}.product-image button{opacity:1}.product-info{display:block}.product-info h3{font-size:18px}.product-info strong{display:block;margin-top:8px}.ingredient{grid-template-columns:1fr}.ingredient-copy{padding:80px 25px}.ingredient-copy h2{font-size:64px}.ingredient-image{height:520px}.quote{padding:100px 24px}.quote blockquote{font-size:33px}.newsletter{padding:75px 24px;display:block}.newsletter h2{font-size:50px;margin:20px 0 45px}.newsletter form{display:flex}footer{align-items:flex-start;gap:30px;flex-wrap:wrap}footer>.wordmark{width:100%}}
</style>
