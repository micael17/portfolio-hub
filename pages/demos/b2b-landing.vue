<template>
  <div class="saas-landing">
    <!-- Navbar -->
    <nav class="navbar" :class="{ 'scrolled': isScrolled }">
      <div class="logo">Nexus<span>HQ</span></div>
      <div class="nav-links">
        <a href="#features">Features</a>
        <a href="#testimonials">Testimonials</a>
        <a href="#pricing">Pricing</a>
        <a href="#faq">FAQ</a>
      </div>
      <div class="nav-actions">
        <a href="#contact" class="login">Log In</a>
        <a href="#contact" class="btn-primary">Book a Demo</a>
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
            <a href="#contact" class="btn-primary large">Start 14-Day Free Trial</a>
            <a href="#contact" class="btn-secondary large"><i class="fa-solid fa-play"></i> Watch Product Tour</a>
          </div>
          <p class="no-cc">No credit card required. Cancel anytime.</p>
        </div>
        <div class="hero-image">
          <!-- AI-IMG: B2B SaaS 매출 대시보드 UI, 다크 테마 · 16:9 -->
          <!-- prompt: minimal dark-theme B2B SaaS revenue dashboard UI, clean charts and sales pipeline, subtle blue accent, 16:9 -->
          <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=1000&q=80" alt="NexusHQ 매출 파이프라인 대시보드 화면" class="dashboard-mockup">
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
          <div class="brand">Umbrella</div>
          <div class="brand">Hooli</div>
          <div class="brand">Vandelay</div>
        </div>
      </section>

      <!-- Metrics / Social Proof Numbers -->
      <section class="metrics" ref="metricsRef">
        <div class="metrics-inner">
          <div v-for="(m, i) in metrics" :key="i" class="metric">
            <div class="metric-value">{{ formatMetric(m) }}</div>
            <div class="metric-label">{{ m.label }}</div>
          </div>
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
          <!-- AI-IMG: 노코드 워크플로우 자동화 빌더 화면, 다크 테마 · 4:3 -->
          <!-- prompt: dark-theme no-code workflow automation builder, drag and drop nodes and branches, blue accent, clean -->
          <img src="https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800&q=80" alt="드래그 앤 드롭 워크플로우 자동화 빌더 화면">
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
          <!-- AI-IMG: 실시간 매출 분석 리포트 대시보드, 다크 테마 · 4:3 -->
          <!-- prompt: dark-theme revenue intelligence analytics dashboard, forecasting charts and drill-down reports, blue accent -->
          <img src="https://images.unsplash.com/photo-1504868584819-f8e8b4b6d7e3?w=800&q=80" alt="실시간 매출 예측 분석 리포트 화면">
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
            <button class="btn-secondary w-100" @click="choosePlan('Starter')">Start Free Trial</button>
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
            <button class="btn-primary w-100" @click="choosePlan('Professional')">Start Free Trial</button>
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
            <button class="btn-secondary w-100" @click="choosePlan('Enterprise')">Contact Sales</button>
          </div>
        </div>
      </section>

      <!-- FAQ -->
      <section class="faq" id="faq">
        <h2 class="section-title text-center">Frequently asked questions</h2>
        <p class="text-center subtitle">Everything you need to know before getting started.</p>
        <div class="faq-list">
          <div v-for="(item, i) in faqs" :key="i" class="faq-item" :class="{ open: openFaq === i }">
            <button
              class="faq-question"
              :aria-expanded="openFaq === i"
              :aria-controls="`faq-panel-${i}`"
              @click="toggleFaq(i)"
            >
              <span>{{ item.q }}</span>
              <i class="fa-solid" :class="openFaq === i ? 'fa-minus' : 'fa-plus'"></i>
            </button>
            <div v-show="openFaq === i" :id="`faq-panel-${i}`" class="faq-answer" role="region">
              <p>{{ item.a }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- CTA / Demo Request -->
      <section class="cta" id="contact">
        <div class="cta-content">
          <h2>Ready to accelerate your growth?</h2>
          <p>Book a personalized demo and see how NexusHQ fits your sales team. No credit card, no commitment.</p>

          <form v-if="!submitted" class="demo-form" @submit.prevent="submitForm" novalidate>
            <p v-if="form.plan" class="plan-pill">Selected plan: <strong>{{ form.plan }}</strong></p>
            <div class="form-row">
              <label class="field">
                <span>Full name</span>
                <input v-model.trim="form.name" type="text" placeholder="Jane Doe" autocomplete="name">
              </label>
              <label class="field">
                <span>Work email</span>
                <input v-model.trim="form.email" type="email" placeholder="jane@company.com" autocomplete="email">
              </label>
            </div>
            <div class="form-row">
              <label class="field">
                <span>Company</span>
                <input v-model.trim="form.company" type="text" placeholder="Acme Inc." autocomplete="organization">
              </label>
              <label class="field">
                <span>Team size</span>
                <select v-model="form.size">
                  <option value="">Select…</option>
                  <option value="1-10">1–10</option>
                  <option value="11-50">11–50</option>
                  <option value="51-200">51–200</option>
                  <option value="200+">200+</option>
                </select>
              </label>
            </div>
            <p v-if="formError" class="form-error">{{ formError }}</p>
            <button type="submit" class="btn-primary large w-100">Book my demo</button>
            <p class="form-note">By submitting, you agree to receive product updates. Unsubscribe anytime.</p>
          </form>

          <div v-else class="demo-success" role="status">
            <div class="success-icon"><i class="fa-solid fa-circle-check"></i></div>
            <h3>Thanks, {{ form.name }}! 🎉</h3>
            <p>Our team will reach out to <strong>{{ form.email }}</strong> within one business day to schedule your demo.</p>
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
          <a href="#features">Features</a>
          <a href="#features">Integrations</a>
          <a href="#pricing">Pricing</a>
          <a href="#contact">Book a Demo</a>
        </div>
        <div class="f-col">
          <h4>Resources</h4>
          <a href="#testimonials">Customer Stories</a>
          <a href="#faq">Help Center</a>
          <a href="#faq">FAQ</a>
          <a href="#features">Product Tour</a>
        </div>
        <div class="f-col">
          <h4>Company</h4>
          <a href="#testimonials">About Us</a>
          <a href="#pricing">Pricing</a>
          <a href="#contact">Contact Sales</a>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2026 NexusHQ Inc. All rights reserved. (Demo Portfolio)</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue'

useHead({
  title: 'NexusHQ | Full B2B SaaS Platform Demo',
  link: [{ rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css' }]
})
definePageMeta({ layout: false })

const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

/* Metrics count-up */
const metricsRef = ref(null)
const hasAnimated = ref(false)
const metrics = ref([
  { value: 0, target: 10000, suffix: '+', label: 'Companies onboarded' },
  { value: 0, target: 40, suffix: '%', label: 'Faster sales cycle' },
  { value: 0, target: 32, suffix: '%', label: 'Higher average win rate' },
  { value: 0, target: 99.9, suffix: '%', decimals: 1, label: 'Uptime SLA' }
])

const formatMetric = (m) => {
  const v = m.decimals
    ? m.value.toFixed(m.decimals)
    : Math.round(m.value).toLocaleString('en-US')
  return `${m.prefix || ''}${v}${m.suffix || ''}`
}

const animateMetrics = () => {
  const duration = 1800
  const start = performance.now()
  const step = (now) => {
    const progress = Math.min((now - start) / duration, 1)
    const eased = 1 - Math.pow(1 - progress, 3)
    metrics.value.forEach((m) => { m.value = m.target * eased })
    if (progress < 1) {
      requestAnimationFrame(step)
    } else {
      metrics.value.forEach((m) => { m.value = m.target })
    }
  }
  requestAnimationFrame(step)
}

/* FAQ accordion */
const openFaq = ref(-1)
const toggleFaq = (i) => { openFaq.value = openFaq.value === i ? -1 : i }
const faqs = [
  {
    q: 'How long does implementation take?',
    a: 'Most teams are fully onboarded within a day. Our guided setup imports your CRM data, maps your pipeline stages, and connects your email in minutes — no engineering required.'
  },
  {
    q: 'Which tools does NexusHQ integrate with?',
    a: 'We offer 500+ native integrations, including Salesforce, HubSpot, Slack, Gmail, Outlook, and Zapier. Anything not covered natively can be connected through our REST API and webhooks.'
  },
  {
    q: 'Is my data secure?',
    a: 'Yes. NexusHQ is SOC 2 Type II certified and GDPR compliant. All data is encrypted in transit and at rest, with SSO and role-based access controls available on Professional and Enterprise plans.'
  },
  {
    q: 'Can I change or cancel my plan later?',
    a: 'Absolutely. You can upgrade, downgrade, or cancel at any time from your billing settings. Changes take effect at the start of your next billing cycle, and unused time is prorated.'
  },
  {
    q: 'Do you offer onboarding support?',
    a: 'Every plan includes access to our help center and email support. Professional plans add priority support, and Enterprise customers get a dedicated success manager and custom onboarding.'
  }
]

/* Demo request form */
const form = reactive({ name: '', email: '', company: '', size: '', plan: '' })
const formError = ref('')
const submitted = ref(false)
const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

const choosePlan = (plan) => {
  form.plan = plan
  if (typeof document !== 'undefined') {
    document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })
  }
}

const submitForm = () => {
  if (!form.name.trim()) {
    formError.value = 'Please enter your full name.'
    return
  }
  if (!emailPattern.test(form.email)) {
    formError.value = 'Please enter a valid work email address.'
    return
  }
  formError.value = ''
  submitted.value = true
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  if (typeof window !== 'undefined' && 'IntersectionObserver' in window && metricsRef.value) {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting && !hasAnimated.value) {
          hasAnimated.value = true
          animateMetrics()
          observer.disconnect()
        }
      })
    }, { threshold: 0.3 })
    observer.observe(metricsRef.value)
  }
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
.text-center { text-align: center; }
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

/* Metrics */
.metrics { padding: 6rem 5%; border-bottom: 1px solid rgba(255,255,255,0.05); }
.metrics-inner { display: grid; grid-template-columns: repeat(4, 1fr); gap: 2rem; max-width: 1400px; margin: 0 auto; text-align: center; }
.metric-value { font-size: 3.5rem; font-weight: 900; letter-spacing: -2px; background: linear-gradient(135deg, #fff 0%, #60a5fa 100%); -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent; }
.metric-label { color: #a1a1aa; font-size: 1rem; margin-top: 0.75rem; }

/* FAQ */
.faq { padding: 8rem 5%; max-width: 800px; margin: 0 auto; }
.faq-list { display: flex; flex-direction: column; gap: 1rem; margin-top: 2rem; }
.faq-item { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.06); border-radius: 12px; overflow: hidden; transition: border-color 0.2s; }
.faq-item.open { border-color: rgba(59, 130, 246, 0.4); }
.faq-question { width: 100%; display: flex; justify-content: space-between; align-items: center; gap: 1rem; padding: 1.5rem; background: none; border: none; color: #fff; font-family: inherit; font-size: 1.15rem; font-weight: 600; text-align: left; cursor: pointer; }
.faq-question i { color: #60a5fa; font-size: 0.9rem; flex-shrink: 0; }
.faq-answer { padding: 0 1.5rem 1.5rem; }
.faq-answer p { color: #a1a1aa; line-height: 1.7; font-size: 1.05rem; }

/* CTA / Demo Request */
.cta { padding: 8rem 5%; }
.cta-content { background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%); padding: 4rem 2rem; border-radius: 24px; text-align: center; max-width: 720px; margin: 0 auto; }
.cta-content h2 { font-size: 3rem; margin-bottom: 1rem; }
.cta-content p { font-size: 1.2rem; color: rgba(255,255,255,0.85); margin-bottom: 2.5rem; }
.demo-form { max-width: 560px; margin: 0 auto; text-align: left; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 1rem; }
.field { display: flex; flex-direction: column; gap: 0.4rem; }
.field span { font-size: 0.85rem; font-weight: 600; color: rgba(255,255,255,0.9); }
.field input, .field select { padding: 0.9rem 1rem; border-radius: 8px; border: none; font-size: 1rem; font-family: inherit; outline: none; background: #fff; color: #09090b; }
.field select { appearance: none; -webkit-appearance: none; cursor: pointer; }
.form-error { color: #fecaca; background: rgba(153, 27, 27, 0.35); padding: 0.6rem 0.9rem; border-radius: 8px; font-size: 0.9rem; margin: 0.5rem 0 1rem; }
.cta-content .demo-form .btn-primary { background: #09090b; margin-top: 0.5rem; }
.cta-content .demo-form .btn-primary:hover { background: #000; }
.form-note { font-size: 0.8rem !important; color: rgba(255,255,255,0.7) !important; margin: 1rem 0 0 !important; text-align: center; }
.plan-pill { display: inline-block; background: rgba(255,255,255,0.15); color: #fff; padding: 0.4rem 1rem; border-radius: 20px; font-size: 0.85rem; margin-bottom: 1.25rem; }
.plan-pill strong { font-weight: 700; }
.demo-success { padding: 1rem; }
.success-icon { font-size: 3.5rem; color: #fff; margin-bottom: 1rem; }
.demo-success h3 { font-size: 1.75rem; margin-bottom: 0.75rem; }
.demo-success p { font-size: 1.1rem; color: rgba(255,255,255,0.9); margin-bottom: 0; }

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
  .metrics-inner { grid-template-columns: repeat(2, 1fr); gap: 3rem 2rem; }
  .footer-grid { grid-template-columns: 1fr 1fr; }
}

@media (max-width: 640px) {
  .hero h1 { font-size: 3rem; }
  .section-title { font-size: 2rem; }
  .cta-content h2 { font-size: 2.2rem; }
  .form-row { grid-template-columns: 1fr; }
  .nav-links { display: none; }
  .metric-value { font-size: 2.75rem; }
}
</style>
