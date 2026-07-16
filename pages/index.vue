<template>
  <div class="home">
    <!-- Header -->
    <header class="header">
      <NuxtLink to="/" class="logo">Port<span>folio</span></NuxtLink>
      <div>
        <a href="mailto:micael17@naver.com" class="contact-btn">Contact</a>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <h1>Minimal. Impactful.</h1>
      <p>본질에 집중한 디자인과 최적화된 기술로<br>당신의 비즈니스에 완벽한 웹 경험을 제공합니다.</p>
      <a href="#portfolio" class="contact-btn">View Projects <i class="fa-solid fa-arrow-down" style="margin-left: 8px;"></i></a>
    </section>

    <!-- Portfolio Categories -->
    <div id="portfolio" class="portfolio-container">
      <!-- New Wedding Demos -->
      <section class="portfolio-category">
        <h2 class="section-title">New Wedding Demos <span class="sub">신규 청첩장 데모</span></h2>
        <div class="portfolio-grid">
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1519741497674-611481863552?auto=format&fit=crop&w=900&q=80" alt="Editorial Wedding" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Wedding</span><span class="tag">New</span><span class="tag">Editorial</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">에디토리얼 웨딩 청첩장</h3>
              <p class="card-desc">화보형 사진 구성과 큰 여백 중심으로 만든 최신 무드 청첩장 데모입니다.</p>
              <a href="/demos/editorial-wedding" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1519225421980-715cb0215aed?auto=format&fit=crop&w=900&q=80" alt="Signature Wedding" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Wedding</span><span class="tag">New</span><span class="tag">Hotel</span><span class="tag">중간</span></div>
              <h3 class="card-title">시그니처 호텔 웨딩 청첩장</h3>
              <p class="card-desc">저녁 예식과 호텔 브로슈어 톤을 섞어, 실제 호텔 웨딩 페이지처럼 순서와 안내까지 꼼꼼히 채운 정돈된 청첩장 데모입니다.</p>
              <a href="/demos/signature-wedding" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1520854221256-17451cc331bf?auto=format&fit=crop&w=900&q=80" alt="Archive Wedding" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Wedding</span><span class="tag">New</span><span class="tag">Film</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">아카이브 필름 웨딩 청첩장</h3>
              <p class="card-desc">필름 스냅과 종이 질감 무드를 앞세워, 실제 청첩장처럼 안내 정보까지 빠짐없이 채운 감도 높은 데모입니다.</p>
              <a href="/demos/archive-wedding" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>
        </div>
      </section>
      
      <!-- Category 1: Invitations & Events -->
      <section class="portfolio-category">
        <h2 class="section-title">Invitations & Events <span class="sub">초대장 및 행사</span></h2>
        <div class="portfolio-grid">
          <!-- 1. Classic Wedding -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1511285560929-80b456fea0bc?w=600&q=80" alt="Classic Wedding" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Wedding</span><span class="tag">Classic</span><span class="tag">대중형</span></div>
              <h3 class="card-title">클래식 웨딩 청첩장</h3>
              <p class="card-desc">우아한 세리프 폰트와 크림색 여백의 미를 살린 가장 정통적이고 고급스러운 웨딩 초대장입니다.</p>
              <a href="/demos/classic-wedding" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- 2. Modern Minimal Wedding -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1606800052052-a08af7148866?w=600&q=80" alt="Modern Wedding" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Wedding</span><span class="tag">Modern</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">모던 미니멀 청첩장</h3>
              <p class="card-desc">흑백의 강렬한 대비와 과감한 타이포그래피를 활용한 도시적인 느낌의 웨딩 초대장입니다.</p>
              <a href="/demos/modern-wedding" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- 3. Botanical Wedding -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1520854221256-17451cc331bf?w=600&q=80" alt="Botanical Wedding" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Wedding</span><span class="tag">Nature</span><span class="tag">대중형</span></div>
              <h3 class="card-title">가든 보태니컬 청첩장</h3>
              <p class="card-desc">그린 톤의 식물 패턴과 따뜻한 색감을 사용하여 싱그러운 야외 웨딩에 완벽하게 어울립니다.</p>
              <a href="/demos/botanical-wedding" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- 5. VIP Luxury Party -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1566737236500-c8ac43014a67?w=600&q=80" alt="VIP Party" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Party</span><span class="tag">Luxury</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">하이엔드 VIP 초청장</h3>
              <p class="card-desc">골드 포인트와 딥 블랙 테마를 사용하여 럭셔리 브랜드 행사에 걸맞은 VIP 전용 모바일 초청장입니다.</p>
              <a href="/demos/vip-party" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- 6. Kids Birthday -->
          <div class="portfolio-card">
            <img src="/images/kids-birthday-ai/leo-hero.webp" alt="Kids Birthday" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Birthday</span><span class="tag">Kids</span><span class="tag">중간</span></div>
              <h3 class="card-title">키즈 생일파티 초대장</h3>
              <p class="card-desc">비비드한 파스텔 컬러 블록과 직선적인 팝아트 요소를 결합한 감각적인 돌잔치/생일 초대장입니다.</p>
              <a href="/demos/kids-birthday" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- 7. Corporate Seminar -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1540575467063-178a50c2df87?w=600&q=80" alt="Corporate Seminar" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Corporate</span><span class="tag">B2B</span><span class="tag">중간</span></div>
              <h3 class="card-title">기업 컨퍼런스 초청장</h3>
              <p class="card-desc">신뢰감을 주는 네이비 블루와 그리드 시스템을 기반으로 한 프로페셔널한 비즈니스 세미나 초청장입니다.</p>
              <a href="/demos/corporate-event" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- 8. Art Exhibition -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1536924940846-227afb31e2a5?w=600&q=80" alt="Art Exhibition" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Art</span><span class="tag">Exhibition</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">갤러리 전시회 오프닝</h3>
              <p class="card-desc">아방가르드한 비대칭 레이아웃과 감각적인 타이포그래피가 돋보이는 예술 전시회 오프닝 초대장입니다.</p>
              <a href="/demos/exhibition" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>
        </div>
      </section>

      <!-- Category 2: Corporate & Professionals -->
      <section class="portfolio-category">
        <h2 class="section-title">Corporate & Professionals <span class="sub">기업 및 전문직 소개</span></h2>
        <div class="portfolio-grid">
          <!-- Placeholder 1: Law Firm -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1589829085413-56de8ae18c73?w=600&q=80" alt="Law Firm" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Corporate</span><span class="tag">Law</span><span class="tag">대중형</span></div>
              <h3 class="card-title">대형 법률사무소 웹사이트</h3>
              <p class="card-desc">무게감 있는 타이포그래피와 신뢰를 주는 레이아웃으로, 실제 대형 로펌 홈페이지처럼 조직·성공사례까지 갖춘 기업 소개 페이지입니다.</p>
              <a href="/demos/law-firm" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- Placeholder 2: Premium Hospital -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1519494026892-80bbd2d6fd0d?w=600&q=80" alt="Hospital" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Medical</span><span class="tag">Premium</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">프리미엄 성형외과/피부과</h3>
              <p class="card-desc">의료진의 전문성과 시설의 고급스러움을 강조하는 뷰티 클리닉 맞춤형 하이엔드 웹사이트입니다.</p>
              <a href="/demos/hospital" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- Placeholder 3: Architecture Firm -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=600&q=80" alt="Architecture" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Agency</span><span class="tag">Architecture</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">건축/인테리어 스튜디오</h3>
              <p class="card-desc">이미지 중심의 포트폴리오 쇼케이스와 함께, 실제 스튜디오 홈페이지처럼 프로젝트·연혁 정보까지 갖춘 소개 페이지입니다.</p>
              <a href="/demos/architecture" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1497366811353-6870744d04b2?w=600&q=80" alt="Corporate Company" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Corporate</span><span class="tag">Standard</span><span class="tag">대중형</span></div>
              <h3 class="card-title">일반 기업 홈페이지</h3>
              <p class="card-desc">회사 소개, 주요 사업, 실적과 문의 전환까지 실제 기업 홈페이지처럼 균형 있게 갖춘 표준형 웹사이트입니다.</p>
              <a href="/demos/corporate-company" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1576091160399-112ba8d25d1d?w=600&q=80" alt="Medical Center" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Medical</span><span class="tag">Hospital</span><span class="tag">대중형</span></div>
              <h3 class="card-title">지역 종합병원 홈페이지</h3>
              <p class="card-desc">진료과, 의료진, 예약과 오시는 길까지 실제 병원 홈페이지처럼 빠짐없이 갖춘 표준형 홈페이지입니다.</p>
              <a href="/demos/medical-center" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1629909613654-28e377c37b09?w=600&q=80" alt="Dental Clinic" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Medical</span><span class="tag">Dental</span><span class="tag">대중형</span></div>
              <h3 class="card-title">동네 치과 홈페이지</h3>
              <p class="card-desc">진료 안내와 의료진 신뢰, 간편 상담 예약까지 실제 치과 홈페이지처럼 갖춘 데모입니다.</p>
              <a href="/demos/dental-clinic" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>
        </div>
      </section>

      <!-- Category 3: Commerce & IT Services -->
      <section class="portfolio-category">
        <h2 class="section-title">Commerce & IT Services <span class="sub">커머스 및 IT 서비스</span></h2>
        <div class="portfolio-grid">
          <!-- B2B Landing -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=600&q=80" alt="Landing Page" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">B2B</span><span class="tag">SaaS</span><span class="tag">대중형</span></div>
              <h3 class="card-title">B2B 리드 제너레이션 랜딩</h3>
              <p class="card-desc">복잡한 요소를 배제하고 사용자 행동을 유도하는 흑백 톤의 랜딩 페이지입니다. 기업의 신뢰도를 극대화합니다.</p>
              <a href="/demos/b2b-landing" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <!-- Bio Link -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1611162617474-5b21e879e113?w=600&q=80" alt="Bio Link" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Mobile</span><span class="tag">SNS</span><span class="tag">스타일리쉬</span></div>
              <h3 class="card-title">인스타 프로필 멀티 링크</h3>
              <p class="card-desc">글래스모피즘 디자인이 적용된 깔끔한 멀티 링크 페이지입니다. 브랜드의 본질을 직관적으로 전달합니다.</p>
              <a href="/demos/bio-link" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>
          
          <!-- E-commerce Placeholder -->
          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=600&q=80" alt="Ecommerce" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Commerce</span><span class="tag">Shop</span><span class="tag">중간</span></div>
              <h3 class="card-title">라이프스타일 브랜드 쇼핑몰</h3>
              <p class="card-desc">구매 전환율을 최적화한 미니멀 디자인 기반의 프론트엔드 쇼핑몰 템플릿입니다.</p>
              <a href="/demos/ecommerce" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1556228720-195a672e8a03?auto=format&fit=crop&w=900&q=80" alt="AUBE Botanical Beauty" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Commerce</span><span class="tag">Beauty</span><span class="tag">Premium</span></div>
              <h3 class="card-title">보태니컬 뷰티 브랜드 숍</h3>
              <p class="card-desc">절제된 에디토리얼 레이아웃과 차분한 컬러로 브랜드 철학과 제품 리추얼을 함께 보여주는 프리미엄 뷰티 커머스입니다.</p>
              <a href="/demos/aube-beauty" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1529139574466-a303027c1d8b?auto=format&fit=crop&w=900&q=80" alt="VICE VERSE Streetwear" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Commerce</span><span class="tag">Fashion</span><span class="tag">Bold</span></div>
              <h3 class="card-title">스트리트웨어 드롭 스토어</h3>
              <p class="card-desc">형광 포인트와 거친 타이포그래피, 룩북 중심의 구성으로 한정판 드롭의 긴장감을 살린 패션 커머스입니다.</p>
              <a href="/demos/vice-street" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>

          <div class="portfolio-card">
            <img src="https://images.unsplash.com/photo-1542838132-92c53300491e?auto=format&fit=crop&w=900&q=80" alt="Morrow Grocery Market" class="card-image">
            <div class="card-content">
              <div class="tags"><span class="tag">Commerce</span><span class="tag">Grocery</span><span class="tag">Editorial</span></div>
              <h3 class="card-title">프리미엄 그로서리 마켓</h3>
              <p class="card-desc">생산자와 제철 이야기를 따뜻한 편집 디자인에 담아 상품 판매와 브랜드 콘텐츠를 자연스럽게 연결한 식품 커머스입니다.</p>
              <a href="/demos/morrow-market" target="_blank" class="demo-link">Live Demo <i class="fa-solid fa-external-link-alt"></i></a>
            </div>
          </div>
        </div>
      </section>

    </div>

    <!-- Policy & Workflow -->
    <section id="policy" class="info-section">
      <h2 class="section-title">Workflow & Policy <span class="sub">작업 방식 및 원칙</span></h2>
      <div class="info-grid">
        <!-- 1. Responsive -->
        <div class="info-card">
          <div class="info-header">01</div>
          <h3>프리미엄 반응형 설계</h3>
          <p>기본 작업은 데스크톱 또는 모바일 중 하나의 주요 타겟 플랫폼에 맞춰 진행됩니다. 모든 디바이스를 지원하는 <strong>풀 반응형(Full-Responsive) 최적화는 프리미엄 고급 의뢰</strong>로만 진행됩니다.</p>
        </div>

        <!-- 2. Process -->
        <div class="info-card">
          <div class="info-header">02</div>
          <h3>유연한 맞춤형 제작 프로세스</h3>
          <p>정해진 고정 기간은 없으며, 원하시는 서비스의 복잡도에 따라 유동적으로 방식을 결정합니다.<br><br>
          <strong>[사례 1] 점진적 고도화 방식</strong><br>
          기획(3일)&rarr;개발(1주)&rarr;재기획(3일)&rarr;재개발(1주)&rarr;배포.<br>조금씩 진행 상황을 확인하며 디테일을 맞춰가는 방식입니다.<br><br>
          <strong>[사례 2] 스탠다드 확정 방식</strong><br>
          기획(1주)&rarr;개발(1주)&rarr;배포.<br>템플릿 및 기획 확정 후, 변동 없이 빠르게 구축하는 방식입니다.</p>
        </div>

        <!-- 3. Support & Comm -->
        <div class="info-card">
          <div class="info-header">03</div>
          <h3>사후 관리 및 커뮤니케이션</h3>
          <p>모든 개발 및 배포가 완료된 이후에도 <strong>2주간 무상 수정 기간</strong>을 보장합니다. 원활하고 명확한 기록을 위해 기본 소통은 <strong>채팅/메시지</strong>로 진행하며, 화상 미팅이 필요하신 경우 <strong>오후 10시부터 밤 12시 사이 줌(Zoom) 회의</strong>가 가능합니다.</p>
        </div>
      </div>
    </section>

    <!-- Guide: Hosting -->
    <section class="guide-section">
      <div class="guide-content">
        <h2 class="section-title">Essential Guide <span class="sub">사이트 운영을 위한 필수 지식 : 호스팅</span></h2>
        
        <div class="analogy-box">
          <div class="analogy-text">
            <h3>웹사이트를 만들면 끝일까요? 아닙니다.</h3>
            <p>카페 창업을 위해 <strong>인테리어 디자인과 멋진 가구를 모두 준비</strong>했더라도, 손님을 받고 카페를 운영하려면 반드시 건물의 <strong>'부동산(상가 점포)'</strong>을 계약해야 합니다.</p>
            <p>웹사이트도 이와 완전히 똑같습니다. 사이트 개발은 '인테리어'를 마친 것과 같습니다. 개발 완료 후 이 사이트를 전 세계 사람들이 접속할 수 있도록 <strong>'서버'라는 가상의 부동산</strong> 공간에 올려두어야만 비로소 정상적인 서비스 운영이 가능해집니다. 이 가상의 부동산 공간을 임대하는 것을 <strong>호스팅(Hosting)</strong>이라고 부릅니다.</p>
            <div class="alert-box">
              <p>📌 부동산 월세를 내듯, 호스팅(서버) 운영 기간에 따라 정기적인 유지 비용이 발생합니다. 단, 서비스의 규모나 트래픽에 따라 완전 무료 옵션부터 프리미엄 유료 서버까지 다양하므로, 상세한 상담을 통해 가장 합리적인 비용의 서버를 세팅해 드립니다.</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Philosophy Banner -->
    <section class="philosophy-banner">
      <div class="ph-content">
        <h2>"고객님은 아이디어에만 집중하세요.<br>어려운 기술은 제가 해결합니다."</h2>
        <div class="ph-line"></div>
        <p>원하시는 서비스가 구체적일수록 완벽한 결과물이 나옵니다. 하지만 IT 지식이 부족해 막막하거나 모호한 부분이 있다면 전혀 걱정하지 마세요. 심도 있는 상담을 통해 머릿속의 아이디어를 현실로 구체화해 드립니다.</p>
        <p>어려운 IT 전문 용어는 몰라도 괜찮습니다. 복잡한 기술적 문제를 해결하고, 이를 가장 쉬운 언어로 풀어내어 고객님을 이해시켜 드리는 것이 바로 제 역할입니다. <strong>고객님은 오직 비즈니스의 본질과 서비스에만 집중해 주세요.</strong></p>
      </div>
    </section>

    <!-- Footer -->
    <footer>
      <p>&copy; 2026 Minif Web Portfolio.</p>
    </footer>
  </div>
</template>

<script setup>
useHead({
  title: 'Minif Portfolio Showcase'
})
</script>
