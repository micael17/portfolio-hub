<template>
  <div class="saas-landing">
    <!-- Navbar -->
    <nav class="navbar" :class="{ 'scrolled': isScrolled }">
      <div class="logo">Nexus<span>HQ</span></div>
      <div class="nav-links">
        <a href="#features">Features</a>
        <a href="#testimonials">Testimonials</a>
        <a href="#pricing">Pricing</a>
      </div>
      <div class="nav-actions">
        <a href="#" class="login">Log In</a>
        <a href="#contact" class="btn-primary">Get Started</a>
      </div>
    </nav>
    
    <main>
      <!-- Hero Section -->
      <section class="hero">
        <div class="hero-content">
          <div class="badge">🚀 v2.0 is now live with AI Insights</div>
          <h1>The Operating System for B2B Sales Teams</h1>
          <p>NexusHQ helps modern teams unify their data, automate complex workflows, and close deals 40% faster. Join 10,000+ top performing companies.</p>
          <div class="hero-actions">
            <a href="#" class="btn-primary large">Start 14-Day Free Trial</a>
            <a href="#" class="btn-secondary large"><i class="fa-solid fa-play"></i> Watch Product Tour</a>
          </div>
          <p class="no-cc">No credit card required. Cancel anytime.</p>
        </div>
        <div class="hero-image">
          <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=1000&q=80" alt="Dashboard Dashboard" class="dashboard-mockup">
        </div>
      </section>

      <!-- Trusted By Section -->
      <section class="trusted-by">
        <p>TRUSTED BY INNOVATIVE TEAMS WORLDWIDE</p>
        <div class="logo-grid">
          <div class="brand">ACME Corp</div>
          <div class="brand">Globex</div>
          <div class="brand">Soylent</div>
          <div class="brand">Initech</div>
          <div class="brand">Stark Ind.</div>
        </div>
      </section>

      <!-- Detail Feature 1 -->
      <section class="feature-detail" id="features">
        <div class="feature-text">
          <h2 class="section-title">Automate everything without writing code</h2>
          <p>Stop wasting time on manual data entry. Our intuitive drag-and-drop workflow builder lets you automate email sequences, task assignments, and CRM updates in minutes.</p>
          <ul>
            <li><i class="fa-solid fa-check"></i> 500+ Native Integrations</li>
            <li><i class="fa-solid fa-check"></i> Advanced branching logic</li>
            <li><i class="fa-solid fa-check"></i> AI-powered email drafting</li>
          </ul>
        </div>
        <div class="feature-img">
          <img src="https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800&q=80" alt="Workflow">
        </div>
      </section>

      <!-- Detail Feature 2 -->
      <section class="feature-detail reverse">
        <div class="feature-text">
          <h2 class="section-title">Real-time revenue intelligence</h2>
          <p>Get complete visibility into your sales pipeline. Our advanced analytics engine spots risks before they become lost deals and predicts revenue with 95% accuracy.</p>
          <ul>
            <li><i class="fa-solid fa-check"></i> Custom dashboard builder</li>
            <li><i class="fa-solid fa-check"></i> Interactive drill-down reports</li>
            <li><i class="fa-solid fa-check"></i> Automated weekly summaries</li>
          </ul>
        </div>
        <div class="feature-img">
          <img src="https://images.unsplash.com/photo-1504868584819-f8e8b4b6d7e3?w=800&q=80" alt="Analytics">
        </div>
      </section>

      <!-- Testimonials -->
      <section class="testimonials" id="testimonials">
        <h2 class="section-title text-center">Don't just take our word for it</h2>
        <div class="testimonial-grid">
          <div class="t-card">
            <div class="stars">★★★★★</div>
            <p>"NexusHQ completely transformed how our sales team operates. We've increased our win rate by 32% in just one quarter."</p>
            <div class="author">
              <strong>Sarah Jenkins</strong>
              <span>VP of Sales, TechCorp</span>
            </div>
          </div>
          <div class="t-card">
            <div class="stars">★★★★★</div>
            <p>"The AI forecasting feature is incredibly accurate. It saves our management team hours of manual spreadsheet work every week."</p>
            <div class="author">
              <strong>Michael Chang</strong>
              <span>CRO, Globex</span>
            </div>
          </div>
          <div class="t-card">
            <div class="stars">★★★★★</div>
            <p>"Setup took less than a day, and the ROI was immediate. Best software investment we've made this year."</p>
            <div class="author">
              <strong>Elena Rodriguez</strong>
              <span>Director of RevOps, Initech</span>
            </div>
          </div>
        </div>
      </section>

      <!-- Pricing -->
      <section class="pricing" id="pricing">
        <h2 class="section-title text-center">Simple, transparent pricing</h2>
        <p class="text-center subtitle">Start free, upgrade when you need to.</p>
        <div class="pricing-grid">
          <div class="p-card">
            <h3>Starter</h3>
            <div class="price"><span>$</span>49<span>/mo</span></div>
            <p>Perfect for small teams getting started.</p>
            <ul>
              <li>Up to 5 Users</li>
              <li>Basic CRM integration</li>
              <li>1,000 Automations/mo</li>
            </ul>
            <button class="btn-secondary w-100">Start Free Trial</button>
          </div>
          <div class="p-card featured">
            <div class="popular-badge">Most Popular</div>
            <h3>Professional</h3>
            <div class="price"><span>$</span>99<span>/mo</span></div>
            <p>Advanced features for growing sales teams.</p>
            <ul>
              <li>Up to 20 Users</li>
              <li>AI Forecasting</li>
              <li>Unlimited Automations</li>
              <li>Priority Support</li>
            </ul>
            <button class="btn-primary w-100">Start Free Trial</button>
          </div>
          <div class="p-card">
            <h3>Enterprise</h3>
            <div class="price">Custom</div>
            <p>For large organizations with complex needs.</p>
            <ul>
              <li>Unlimited Users</li>
              <li>Dedicated Success Manager</li>
              <li>Custom API Limits</li>
              <li>SSO & SOC2</li>
            </ul>
            <button class="btn-secondary w-100">Contact Sales</button>
          </div>
        </div>
      </section>

      <!-- CTA -->
      <section class="cta" id="contact">
        <div class="cta-content">
          <h2>Ready to accelerate your growth?</h2>
          <p>Join thousands of companies using NexusHQ to close more deals.</p>
          <div class="cta-form">
            <input type="email" placeholder="Enter your work email">
            <button class="btn-primary">Get Started</button>
          </div>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer>
      <div class="footer-grid">
        <div class="f-col">
          <div class="logo">Nexus<span>HQ</span></div>
          <p>The ultimate revenue operating system for B2B teams.</p>
        </div>
        <div class="f-col">
          <h4>Product</h4>
          <a href="#">Features</a>
          <a href="#">Integrations</a>
          <a href="#">Pricing</a>
          <a href="#">Changelog</a>
        </div>
        <div class="f-col">
          <h4>Resources</h4>
          <a href="#">Blog</a>
          <a href="#">Help Center</a>
          <a href="#">Sales Guides</a>
          <a href="#">API Docs</a>
        </div>
        <div class="f-col">
          <h4>Company</h4>
          <a href="#">About Us</a>
          <a href="#">Careers</a>
          <a href="#">Contact</a>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2026 NexusHQ Inc. All rights reserved. (Demo Portfolio)</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

useHead({ 
  title: 'NexusHQ | Full B2B SaaS Platform Demo',
  link: [{ rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css' }]
})
definePageMeta({ layout: false })

const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap');

.saas-landing {
  font-family: 'Inter', sans-serif;
  background: #09090b;
  color: #fff;
  min-height: 100vh;
  overflow-x: hidden;
}

/* Typography & Utilities */
h1, h2, h3, h4 { font-weight: 700; }
.section-title { font-size: 2.5rem; margin-bottom: 1.5rem; letter-spacing: -1px; }
.text-center { text-center; }
.subtitle { font-size: 1.2rem; color: #a1a1aa; margin-bottom: 3rem; }
.w-100 { width: 100%; }

/* Buttons */
.btn-primary {
  background: #3b82f6;
  color: #fff !important;
  padding: 0.8rem 1.5rem;
  border-radius: 8px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s;
  border: none;
  cursor: pointer;
  display: inline-block;
  text-align: center;
}
.btn-primary:hover { background: #2563eb; transform: translateY(-2px); }
.btn-primary.large { padding: 1.2rem 2.5rem; font-size: 1.1rem; }

.btn-secondary {
  background: rgba(255,255,255,0.05);
  color: #fff;
  border: 1px solid rgba(255,255,255,0.1);
  padding: 0.8rem 1.5rem;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s;
  cursor: pointer;
  display: inline-block;
  text-align: center;
}
.btn-secondary:hover { background: rgba(255,255,255,0.1); }
.btn-secondary.large { padding: 1.2rem 2.5rem; font-size: 1.1rem; }

/* Navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 5%;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 100;
  transition: all 0.3s;
}
.navbar.scrolled {
  background: rgba(9, 9, 11, 0.9);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255,255,255,0.05);
  padding: 1rem 5%;
}
.logo { font-size: 1.5rem; font-weight: 900; letter-spacing: -1px; }
.logo span { color: #3b82f6; }
.nav-links { display: flex; gap: 2rem; }
.nav-links a { color: #a1a1aa; text-decoration: none; font-weight: 500; transition: color 0.2s; }
.nav-links a:hover { color: #fff; }
.nav-actions { display: flex; align-items: center; gap: 1.5rem; }
.login { color: #fff; text-decoration: none; font-weight: 500; }

/* Hero */
.hero {
  padding: 12rem 5% 6rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
}
.badge {
  display: inline-block;
  padding: 0.5rem 1rem;
  background: rgba(59, 130, 246, 0.1);
  color: #60a5fa;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 600;
  margin-bottom: 1.5rem;
  border: 1px solid rgba(59, 130, 246, 0.2);
}
.hero h1 {
  font-size: 4.5rem;
  line-height: 1.1;
  margin-bottom: 1.5rem;
  letter-spacing: -2px;
}
.hero p {
  font-size: 1.25rem;
  color: #a1a1aa;
  margin-bottom: 2.5rem;
  line-height: 1.6;
}
.hero-actions { display: flex; gap: 1rem; margin-bottom: 1rem; }
.no-cc { font-size: 0.9rem !important; color: #71717a !important; }
.dashboard-mockup {
  width: 100%;
  border-radius: 12px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(255,255,255,0.1);
}

/* Trusted By */
.trusted-by {
  padding: 4rem 5%;
  border-top: 1px solid rgba(255,255,255,0.05);
  border-bottom: 1px solid rgba(255,255,255,0.05);
  text-align: center;
  background: rgba(255,255,255,0.01);
}
.trusted-by p { color: #71717a; font-size: 0.9rem; font-weight: 600; letter-spacing: 2px; margin-bottom: 2rem; }
.logo-grid {
  display: flex;
  justify-content: center;
  gap: 4rem;
  flex-wrap: wrap;
  opacity: 0.5;
}
.brand { font-size: 1.5rem; font-weight: 800; font-family: serif; color: #fff; }

/* Feature Detail */
.feature-detail {
  padding: 8rem 5%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
}
.feature-detail.reverse .feature-text { order: 2; }
.feature-detail.reverse .feature-img { order: 1; }
.feature-text p { font-size: 1.2rem; color: #a1a1aa; line-height: 1.7; margin-bottom: 2rem; }
.feature-text ul { list-style: none; padding: 0; }
.feature-text li { font-size: 1.1rem; margin-bottom: 1rem; display: flex; align-items: center; gap: 1rem; }
.feature-text li i { color: #3b82f6; }
.feature-img img { width: 100%; border-radius: 16px; border: 1px solid rgba(255,255,255,0.1); }

/* Testimonials */
.testimonials {
  padding: 8rem 5%;
  background: rgba(255,255,255,0.02);
}
.testimonial-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  max-width: 1400px;
  margin: 0 auto;
}
.t-card {
  background: rgba(255,255,255,0.03);
  padding: 2.5rem;
  border-radius: 16px;
  border: 1px solid rgba(255,255,255,0.05);
}
.stars { color: #fbbf24; margin-bottom: 1.5rem; font-size: 1.2rem; }
.t-card p { font-size: 1.1rem; color: #e4e4e7; line-height: 1.6; margin-bottom: 2rem; font-style: italic; }
.author strong { display: block; font-size: 1.1rem; }
.author span { color: #a1a1aa; font-size: 0.9rem; }

/* Pricing */
.pricing { padding: 8rem 5%; max-width: 1400px; margin: 0 auto; text-align: center; }
.pricing-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem; margin-top: 4rem; text-align: left; }
.p-card { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.05); border-radius: 16px; padding: 3rem 2.5rem; position: relative; }
.p-card.featured { border-color: #3b82f6; background: rgba(59, 130, 246, 0.05); transform: scale(1.05); z-index: 1; }
.popular-badge { position: absolute; top: -15px; left: 50%; transform: translateX(-50%); background: #3b82f6; padding: 0.4rem 1rem; border-radius: 20px; font-size: 0.8rem; font-weight: bold; }
.p-card h3 { font-size: 1.5rem; margin-bottom: 1rem; }
.price { font-size: 3.5rem; font-weight: 800; margin-bottom: 1rem; display: flex; align-items: baseline; }
.price span { font-size: 1.5rem; color: #a1a1aa; font-weight: 500; }
.p-card > p { color: #a1a1aa; margin-bottom: 2rem; }
.p-card ul { list-style: none; padding: 0; margin-bottom: 3rem; }
.p-card li { margin-bottom: 1rem; color: #e4e4e7; }
.p-card li::before { content: '✓'; color: #3b82f6; margin-right: 10px; font-weight: bold; }

/* CTA */
.cta { padding: 8rem 5%; }
.cta-content { background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%); padding: 5rem 2rem; border-radius: 24px; text-align: center; max-width: 1000px; margin: 0 auto; }
.cta-content h2 { font-size: 3rem; margin-bottom: 1rem; }
.cta-content p { font-size: 1.2rem; color: rgba(255,255,255,0.8); margin-bottom: 3rem; }
.cta-form { display: flex; gap: 1rem; max-width: 500px; margin: 0 auto; }
.cta-form input { flex: 1; padding: 1rem 1.5rem; border-radius: 8px; border: none; font-size: 1rem; outline: none; }

/* Footer */
footer { border-top: 1px solid rgba(255,255,255,0.05); padding: 5rem 5% 2rem; background: #000; }
.footer-grid { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 4rem; max-width: 1400px; margin: 0 auto 4rem; }
.footer-grid p { color: #a1a1aa; margin-top: 1.5rem; line-height: 1.6; }
.f-col h4 { font-size: 1.1rem; margin-bottom: 1.5rem; }
.f-col a { display: block; color: #a1a1aa; text-decoration: none; margin-bottom: 1rem; transition: color 0.2s; }
.f-col a:hover { color: #fff; }
.footer-bottom { text-align: center; padding-top: 2rem; border-top: 1px solid rgba(255,255,255,0.05); color: #71717a; font-size: 0.9rem; }

@media (max-width: 1024px) {
  .hero, .feature-detail { grid-template-columns: 1fr; text-align: center; }
  .feature-detail.reverse .feature-text { order: 1; }
  .feature-detail.reverse .feature-img { order: 2; }
  .testimonial-grid, .pricing-grid { grid-template-columns: 1fr; }
  .p-card.featured { transform: scale(1); }
  .footer-grid { grid-template-columns: 1fr 1fr; }
}
</style>
