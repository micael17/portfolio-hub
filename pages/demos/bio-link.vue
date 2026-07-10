<template>
  <div class="bio-link-bg">
    <div class="glass-card">
      <div class="header-cover"></div>
      
      <div class="profile-section">
        <img src="https://images.unsplash.com/photo-1611162617474-5b21e879e113?w=400&q=80" alt="Profile" class="profile-img">
        <h2>@creative_studio</h2>
        <p>Digital Art & UI/UX Design<br>Based in Seoul, KR 🇰🇷</p>
      </div>
      
      <div class="socials">
        <a href="#"><i class="fa-brands fa-instagram"></i></a>
        <a href="#"><i class="fa-brands fa-twitter"></i></a>
        <a href="#"><i class="fa-brands fa-dribbble"></i></a>
        <a href="#"><i class="fa-brands fa-youtube"></i></a>
      </div>

      <div class="content-section">
        <h3>Featured Links</h3>
        <div class="links">
          <a href="#" class="link-item highlight">
            <div class="link-icon"><i class="fa-solid fa-briefcase"></i></div>
            <div class="link-text">
              <strong>View My Portfolio</strong>
              <span>Latest UI/UX Case Studies</span>
            </div>
            <i class="fa-solid fa-chevron-right arrow"></i>
          </a>
          
          <a href="#" class="link-item">
            <div class="link-icon"><i class="fa-solid fa-pen-nib"></i></div>
            <div class="link-text">
              <strong>Design Assets Shop</strong>
              <span>Figma templates & UI kits</span>
            </div>
            <i class="fa-solid fa-chevron-right arrow"></i>
          </a>
          
          <a href="#" class="link-item">
            <div class="link-icon"><i class="fa-solid fa-envelope"></i></div>
            <div class="link-text">
              <strong>Business Inquiries</strong>
              <span>Available for freelance work</span>
            </div>
            <i class="fa-solid fa-chevron-right arrow"></i>
          </a>
        </div>

        <h3>Latest Video</h3>
        <div class="video-container">
          <div class="video-mock">
            <img src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=800&q=80" alt="Thumbnail">
            <div class="play-btn"><i class="fa-solid fa-play"></i></div>
            <div class="video-title">My 2026 Design Workflow in Figma</div>
          </div>
        </div>

        <h3>Latest Work</h3>
        <div class="work-grid">
          <img src="https://images.unsplash.com/photo-1558655146-d09347e92766?w=400&q=80" alt="Work 1">
          <img src="https://images.unsplash.com/photo-1561070791-2526d30994b5?w=400&q=80" alt="Work 2">
          <img src="https://images.unsplash.com/photo-1550745165-9bc0b252726f?w=400&q=80" alt="Work 3">
          <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=400&q=80" alt="Work 4">
        </div>
      </div>
      
      <div class="footer">
        <p>Powered by <strong>LinkHub</strong></p>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ 
  title: 'Bio Link | Creative Studio Full Demo',
  link: [{ rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css' }]
})
definePageMeta({ layout: false })
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

h2 { font-size: 1.8rem; margin-bottom: 0.5rem; color: #fff; font-weight: 800; text-shadow: 0 2px 10px rgba(0,0,0,0.2); }
.profile-section p { color: rgba(255, 255, 255, 0.9); font-size: 1.05rem; font-weight: 500; line-height: 1.5; }

.socials {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin: 2rem 0;
}
.socials a {
  width: 45px; height: 45px; background: rgba(255,255,255,0.2); border-radius: 50%; display: flex; justify-content: center; align-items: center; color: #fff; font-size: 1.2rem; transition: all 0.3s ease; border: 1px solid rgba(255,255,255,0.1);
}
.socials a:hover { transform: translateY(-5px); background: rgba(255,255,255,0.4); box-shadow: 0 10px 20px rgba(0,0,0,0.1); }

.content-section { padding: 0 2rem 2rem; }
h3 { color: #fff; font-size: 1.2rem; font-weight: 800; margin-bottom: 1rem; margin-top: 2rem; }

.links { display: flex; flex-direction: column; gap: 1rem; }
.link-item {
  display: flex; align-items: center; padding: 1rem; background: rgba(255, 255, 255, 0.15); color: #fff; text-decoration: none; border-radius: 20px; transition: all 0.3s ease; border: 1px solid rgba(255, 255, 255, 0.2);
}
.link-item:hover { transform: translateY(-3px); background: rgba(255, 255, 255, 0.25); box-shadow: 0 15px 30px rgba(0,0,0,0.1); }
.link-item.highlight { background: rgba(255, 255, 255, 0.95); color: #111; }
.link-item.highlight:hover { background: #fff; box-shadow: 0 15px 30px rgba(245, 87, 108, 0.3); }

.link-icon { width: 50px; height: 50px; background: rgba(0,0,0,0.05); border-radius: 15px; display: flex; justify-content: center; align-items: center; font-size: 1.3rem; margin-right: 1rem; }
.highlight .link-icon { background: rgba(245, 87, 108, 0.1); color: #f5576c; }

.link-text { flex: 1; display: flex; flex-direction: column; }
.link-text strong { font-size: 1.1rem; font-weight: 800; margin-bottom: 0.2rem; }
.link-text span { font-size: 0.85rem; opacity: 0.8; font-weight: 500; }
.arrow { opacity: 0.5; }

.video-container { width: 100%; border-radius: 20px; overflow: hidden; position: relative; }
.video-mock { width: 100%; height: 200px; position: relative; display: flex; justify-content: center; align-items: center; cursor: pointer; }
.video-mock img { position: absolute; width: 100%; height: 100%; object-fit: cover; transition: transform 0.3s; }
.video-mock::after { content: ''; position: absolute; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.3); transition: background 0.3s; }
.video-mock:hover img { transform: scale(1.05); }
.video-mock:hover::after { background: rgba(0,0,0,0.2); }
.play-btn { width: 60px; height: 60px; background: rgba(255,255,255,0.9); color: #f5576c; border-radius: 50%; display: flex; justify-content: center; align-items: center; font-size: 1.5rem; position: relative; z-index: 2; padding-left: 5px; box-shadow: 0 10px 20px rgba(0,0,0,0.2); }
.video-title { position: absolute; bottom: 15px; left: 15px; color: #fff; font-weight: 700; z-index: 2; text-shadow: 0 2px 4px rgba(0,0,0,0.5); }

.work-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.work-grid img { width: 100%; height: 150px; object-fit: cover; border-radius: 16px; transition: transform 0.3s; cursor: pointer; }
.work-grid img:hover { transform: scale(1.03); }

.footer { padding: 2rem; text-align: center; color: rgba(255,255,255,0.7); font-size: 0.9rem; border-top: 1px solid rgba(255,255,255,0.1); margin-top: 2rem; }
.footer strong { color: #fff; font-weight: 800; }
</style>
