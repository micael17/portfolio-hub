<template>
  <div class="vice">
    <CommerceAdminAdminDemoLink to="/demos/commerce-admin/vice" />
    <header>
      <a class="logo" href="#">VICE/VERSE</a>
      <nav><a href="#drop">NEW DROP</a><a href="#lookbook">LOOKBOOK</a><a href="#about">ABOUT</a></nav>
      <button @click="bagOpen = !bagOpen">BAG [{{ bag.length }}]</button>
    </header>
    <main>
      <section class="hero">
        <div class="ticker"><div>DROP 07 — OUT NOW &nbsp; DROP 07 — OUT NOW &nbsp; DROP 07 — OUT NOW &nbsp;</div></div>
        <img src="https://images.unsplash.com/photo-1529139574466-a303027c1d8b?auto=format&fit=crop&w=1800&q=90" alt="도시 거리의 스트리트 패션 모델">
        <div class="hero-copy"><p>SEOUL / 2026 / CAPSULE 07</p><h1>NO<br>PERMISSION</h1><a href="#drop">SHOP THE DROP ↓</a></div>
        <div class="stamp">LIMITED<br>EDITION<br>07/100</div>
      </section>

      <section id="drop" class="drop">
        <div class="drop-head"><h2>DROP_07</h2><p>UNIFORM FOR<br>THE UNDECIDED.</p><span>04 PIECES</span></div>
        <div class="products">
          <article v-for="(p,i) in products" :key="p.name" class="product">
            <div class="pic"><img :src="p.image" :alt="p.name"><span>0{{ i+1 }}</span><button @click="add(p)">ADD TO BAG</button></div>
            <div class="info"><h3>{{ p.name }}</h3><p>{{ p.price }}</p><small>{{ p.colors }}</small></div>
          </article>
        </div>
      </section>

      <section id="lookbook" class="manifesto">
        <p>[ V/V MANIFESTO 001 ]</p>
        <h2>WE MAKE CLOTHES<br>FOR <span>NO ONE</span> IN<br>PARTICULAR.</h2>
        <div class="manifesto-foot"><p>Designed in Seoul.<br>Made in small runs.<br>Worn everywhere.</p><p>거리를 규정하는 대신,<br>거리가 우리를 바꾸게 둡니다.</p></div>
      </section>

      <section class="lookbook">
        <div class="look one"><img src="https://images.unsplash.com/photo-1539109136881-3be0616acf4b?auto=format&fit=crop&w=1100&q=85" alt="블랙 재킷 스트리트 룩"><b>LOOK 01</b></div>
        <div class="look two"><img src="https://images.unsplash.com/photo-1523398002811-999ca8dec234?auto=format&fit=crop&w=1100&q=85" alt="그래픽 티셔츠 스트리트 룩"><b>LOOK 02</b></div>
        <div class="look-copy"><p>CAPTURED IN<br>EULJIRO, SEOUL</p><h2>AFTER<br>DARK.</h2><span>35.126° N<br>126.831° E</span></div>
      </section>

      <section id="about" class="signup"><div><span>GET ACCESS</span><h2>FIRST TO KNOW.<br>LAST TO FOLLOW.</h2></div><form @submit.prevent="joined=true"><input v-model="email" required type="email" placeholder="ENTER YOUR EMAIL"><button>{{ joined ? 'YOU’RE IN' : 'JOIN →' }}</button></form></section>
    </main>
    <footer><a class="logo" href="#">VICE/VERSE</a><div><a href="#">INSTAGRAM</a><a href="#">SHIPPING</a><a href="#">CONTACT</a><NuxtLink to="/demos/commerce-admin/vice">ADMIN ↗</NuxtLink></div><p>©2026<br>SEOUL, KR</p></footer>
    <Transition name="bag"><aside v-if="bagOpen" class="bag"><div class="bag-title"><h2>BAG</h2><button @click="bagOpen=false">[CLOSE]</button></div><p v-if="!bag.length" class="bag-empty">NOTHING HERE.<br>YET.</p><div v-for="item in bag" :key="item.name" class="bag-item"><img :src="item.image" :alt="item.name"><div>{{ item.name }}<br>{{ item.price }}</div></div><button v-if="bag.length" class="checkout">CHECKOUT →</button></aside></Transition>
  </div>
</template>
<script setup>
useHead({ title: 'VICE/VERSE — Drop 07' })
definePageMeta({ layout:false })
const bag=ref([]), bagOpen=ref(false), email=ref(''), joined=ref(false)
const products=[
 {name:'VOID SHELL JACKET',price:'₩189,000',colors:'BLACK / STEEL',image:'https://images.unsplash.com/photo-1551028719-00167b16eac5?auto=format&fit=crop&w=900&q=85'},
 {name:'SYSTEM CARGO 2.0',price:'₩142,000',colors:'STONE / BLACK',image:'https://images.unsplash.com/photo-1517445312882-bc9910d016b7?auto=format&fit=crop&w=900&q=85'},
 {name:'SIGNAL MESH TOP',price:'₩79,000',colors:'OPTIC / ACID',image:'https://images.unsplash.com/photo-1503342394128-c104d54dba01?auto=format&fit=crop&w=900&q=85'},
 {name:'V/V UNIT BAG',price:'₩96,000',colors:'BLACK ONLY',image:'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?auto=format&fit=crop&w=900&q=85'}]
function add(p){bag.value.push(p);bagOpen.value=true}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Archivo+Black&family=IBM+Plex+Mono:wght@400;500&display=swap');
:global(*){box-sizing:border-box}.vice{width:100vw;margin-left:calc(50% - 50vw);font-family:'IBM Plex Mono',monospace;background:#e8e7e2;color:#111;min-height:100vh}.vice header{height:70px;background:#d8ff00;display:grid;grid-template-columns:1fr 1fr 1fr;align-items:center;padding:0 25px;border-bottom:2px solid #111;position:relative;z-index:3}.logo{font:22px 'Archivo Black';color:#111;text-decoration:none;letter-spacing:-1px}.vice header nav{display:flex;justify-content:center;gap:25px}.vice header nav a,.vice header button{font:11px 'IBM Plex Mono';color:#111;text-decoration:none;background:0;border:0;cursor:pointer}.vice header>button{text-align:right}.hero{height:calc(100vh - 70px);min-height:620px;position:relative;overflow:hidden;background:#111}.hero>img{width:100%;height:100%;object-fit:cover;object-position:center 35%;filter:grayscale(1) contrast(1.15) brightness(.72)}.ticker{position:absolute;z-index:2;top:0;width:100%;overflow:hidden;background:#111;color:#d8ff00;border-bottom:1px solid #d8ff00;padding:8px 0;font-size:10px;white-space:nowrap}.ticker div{width:max-content;animation:scroll 15s linear infinite}@keyframes scroll{to{transform:translateX(-33.333%)}}.hero-copy{position:absolute;left:4vw;bottom:6vh;color:white}.hero-copy p{font-size:11px;letter-spacing:1px}.hero h1{font:clamp(70px,12vw,180px)/.77 'Archivo Black';letter-spacing:-8px;margin:28px 0 35px}.hero-copy a{display:inline-block;background:#d8ff00;color:#111;padding:16px 22px;text-decoration:none;font-size:11px;font-weight:bold}.stamp{position:absolute;right:4vw;bottom:6vh;width:120px;height:120px;border-radius:50%;border:2px solid #d8ff00;color:#d8ff00;display:grid;place-items:center;text-align:center;transform:rotate(12deg);font-size:11px}.drop{padding:110px 25px;background:#e8e7e2}.drop-head{display:grid;grid-template-columns:2fr 1fr 1fr;align-items:end;border-bottom:3px solid;padding-bottom:20px;margin-bottom:20px}.drop-head h2{font:clamp(55px,8vw,120px)/.8 'Archivo Black';letter-spacing:-5px}.drop-head p,.drop-head span{font-size:11px}.drop-head span{text-align:right}.products{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}.pic{height:480px;position:relative;background:#ccc;overflow:hidden}.pic img{width:100%;height:100%;object-fit:cover;filter:grayscale(1);transition:.25s}.product:hover img{filter:grayscale(0)}.pic>span{position:absolute;top:10px;left:10px;background:#111;color:white;padding:5px 8px;font-size:10px}.pic button{position:absolute;left:8px;right:8px;bottom:8px;background:#d8ff00;border:2px solid;padding:13px;font:11px 'IBM Plex Mono';font-weight:bold;cursor:pointer;transform:translateY(70px);transition:.2s}.product:hover button{transform:none}.info{display:grid;grid-template-columns:1fr auto;gap:5px;padding:13px 0;border-top:2px solid;margin-top:7px}.info h3,.info p{font-size:11px}.info small{font-size:9px;color:#555}.manifesto{background:#111;color:white;padding:130px 5vw}.manifesto>p{font-size:10px;color:#d8ff00}.manifesto h2{font:clamp(55px,9vw,135px)/.88 'Archivo Black';letter-spacing:-7px;margin:60px 0}.manifesto h2 span{color:#d8ff00;text-decoration:line-through;text-decoration-thickness:6px}.manifesto-foot{border-top:1px solid #777;padding-top:20px;display:flex;justify-content:space-between;font-size:11px;line-height:1.7}.lookbook{display:grid;grid-template-columns:1fr 1fr;height:1100px;position:relative;background:#d8ff00;padding:45px;gap:25px}.look{position:relative}.look img{width:100%;height:100%;object-fit:cover;filter:grayscale(1)}.look b{position:absolute;top:10px;left:10px;background:#d8ff00;padding:5px;font-size:10px}.look.one{height:700px}.look.two{height:700px;margin-top:300px}.look-copy{position:absolute;left:6%;top:780px;z-index:2}.look-copy p{font-size:10px}.look-copy h2{font:90px/.8 'Archivo Black';letter-spacing:-6px;margin:15px 0}.look-copy span{font-size:9px}.signup{background:#ec4b25;color:#111;padding:95px 4vw;display:grid;grid-template-columns:1.4fr 1fr;align-items:end;border-top:3px solid}.signup span{font-size:10px}.signup h2{font:clamp(42px,5vw,72px)/.9 'Archivo Black';letter-spacing:-3px;margin-top:20px}.signup form{display:flex;border-bottom:3px solid;padding:12px 0}.signup input{flex:1;background:none;border:0;outline:0;font:13px 'IBM Plex Mono';color:#111}.signup input::placeholder{color:#111}.signup button{background:none;border:0;font:bold 12px 'IBM Plex Mono'}.vice footer{background:#111;color:white;padding:60px 25px;display:grid;grid-template-columns:1fr 1fr 1fr;align-items:end}.vice footer .logo{color:white}.vice footer div{display:flex;gap:25px}.vice footer a,.vice footer p{color:white;text-decoration:none;font-size:10px}.vice footer p{text-align:right}.bag{position:fixed;z-index:10;right:0;top:0;width:min(450px,100%);height:100%;background:#d8ff00;border-left:3px solid;padding:25px;display:flex;flex-direction:column;overflow:auto}.bag-title{display:flex;justify-content:space-between;border-bottom:3px solid;padding-bottom:15px}.bag-title h2{font:60px 'Archivo Black'}.bag-title button{border:0;background:0}.bag-empty{margin:auto;font:35px/1 'Archivo Black';text-align:center}.bag-item{display:flex;gap:15px;border-bottom:2px solid;padding:15px 0;font-size:11px}.bag-item img{width:80px;height:100px;object-fit:cover;filter:grayscale(1)}.checkout{margin-top:auto;background:#111;color:#d8ff00;border:0;padding:18px;font:12px 'IBM Plex Mono'}.bag-enter-active,.bag-leave-active{transition:.3s}.bag-enter-from,.bag-leave-to{transform:translateX(100%)}
@media(max-width:800px){.vice header{grid-template-columns:1fr auto;padding:0 15px}.vice header nav{display:none}.hero h1{font-size:67px;letter-spacing:-4px}.hero-copy{left:20px}.stamp{width:90px;height:90px;font-size:9px}.drop{padding:75px 12px}.drop-head{grid-template-columns:1fr auto}.drop-head h2{font-size:53px}.drop-head p{display:none}.products{grid-template-columns:repeat(2,1fr)}.pic{height:300px}.pic button{transform:none;padding:10px}.manifesto{padding:90px 20px}.manifesto h2{font-size:48px;letter-spacing:-3px}.manifesto-foot{gap:20px}.lookbook{height:850px;padding:12px;gap:8px}.look.one,.look.two{height:550px}.look.two{margin-top:180px}.look-copy{top:600px}.look-copy h2{font-size:58px}.signup{display:block;padding:70px 20px}.signup h2{font-size:42px;margin-bottom:60px}.vice footer{grid-template-columns:1fr auto}.vice footer div{display:none}}
</style>
