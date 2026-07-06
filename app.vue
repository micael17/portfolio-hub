<template>
  <div>
    <!-- Header -->
    <header class="header">
      <a href="#" class="logo">Port<span>folio</span></a>
      <div>
        <a href="mailto:your@email.com" class="contact-btn" style="padding: 0.6rem 1.5rem; font-size: 0.9rem;">의뢰하기</a>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <h1>매출을 높이는<br>프리미엄 웹사이트</h1>
      <p>단순한 디자인을 넘어, 고객의 비즈니스 목적에 완벽하게 부합하는 맞춤형 웹/모바일 솔루션을 제공합니다. 완성도 높은 데모를 직접 확인해 보세요.</p>
      <a href="#portfolio" class="contact-btn">포트폴리오 보기 <i class="fa-solid fa-arrow-down" style="margin-left: 8px;"></i></a>
    </section>

    <!-- Portfolio Showcase -->
    <section id="portfolio" class="portfolio">
      <h2 class="section-title">주요 프로젝트</h2>
      
      <div class="portfolio-grid">
        <!-- Project 1: Bio Link -->
        <div class="portfolio-card">
          <img src="https://images.unsplash.com/photo-1611162617474-5b21e879e113?w=600&q=80" alt="Bio Link" class="card-image">
          <div class="card-content">
            <div class="tags"><span class="tag">Mobile</span><span class="tag">SNS</span></div>
            <h3 class="card-title">인스타 프로필 링크 템플릿</h3>
            <p class="card-desc">글래스모피즘(Glassmorphism) 디자인이 적용된 트렌디한 멀티 링크 페이지입니다. 개인 브랜딩과 인플루언서에게 적합합니다.</p>
            <a href="#" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
          </div>
        </div>

        <!-- Project 2: Landing Page -->
        <div class="portfolio-card">
          <img src="https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=600&q=80" alt="Landing Page" class="card-image">
          <div class="card-content">
            <div class="tags"><span class="tag">B2B</span><span class="tag">Lead Gen</span></div>
            <h3 class="card-title">DB 수집용 원페이지 랜딩</h3>
            <p class="card-desc">기업의 신뢰도를 높이는 깔끔한 레이아웃과, 외부 API(Formspree) 연동을 통한 서버리스 이메일 문의 폼을 포함합니다.</p>
            <a href="#" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
          </div>
        </div>

        <!-- Project 3: QR Menu -->
        <div class="portfolio-card">
          <img src="https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=600&q=80" alt="QR Menu" class="card-image">
          <div class="card-content">
            <div class="tags"><span class="tag">F&B</span><span class="tag">App UI</span></div>
            <h3 class="card-title">스마트 QR 모바일 메뉴판</h3>
            <p class="card-desc">카페 및 식당을 위한 모바일 앱 스타일의 메뉴판입니다. 카테고리 탭과 실시간 장바구니 기능을 지원합니다.</p>
            <a href="#" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
          </div>
        </div>

        <!-- Project 4: Wedding Invitation -->
        <div class="portfolio-card">
          <img src="https://images.unsplash.com/photo-1519741497674-611481863552?w=600&q=80" alt="Wedding Invitation" class="card-image">
          <div class="card-content">
            <div class="tags"><span class="tag">Wedding</span><span class="tag">Premium</span></div>
            <h3 class="card-title">고급형 모바일 청첩장</h3>
            <p class="card-desc">부드러운 애니메이션, 가로 스와이프 갤러리, 계좌번호 복사 및 지도 연동을 포함한 프리미엄 청첩장입니다.</p>
            <a href="#" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer>
      <p>&copy; 2026 Web Portfolio. Built with Nuxt 3.</p>
    </footer>
  </div>
</template>

<script setup>
// Hub page logic
</script>
