<script setup>
import { ref, onMounted } from 'vue'

const isScrolled = ref(false)
const heroCard = ref(null)
const parallaxBox = ref(null)

// 1. 3D Tilt-Effekt für das Hero-Bild
const handleMove = (e) => {
  if (!heroCard.value) return
  const { left, top, width, height } = heroCard.value.getBoundingClientRect()
  const x = (e.clientX - left) / width - 0.5
  const y = (e.clientY - top) / height - 0.5
  
  heroCard.value.style.transform = `perspective(1000px) rotateY(${x * 15}deg) rotateX(${-y * 15}deg) translateY(-10px)`
  heroCard.value.style.boxShadow = `${-x * 30}px ${-y * 30}px 50px rgba(0, 243, 255, 0.15)`
}

const resetMove = () => {
  if (!heroCard.value) return
  heroCard.value.style.transform = 'perspective(1000px) rotateY(0deg) rotateX(0deg) translateY(0px)'
  heroCard.value.style.boxShadow = '0 20px 40px rgba(0,0,0,0.4)'
}

// 2. Scroll-Reveals & Parallax
onMounted(() => {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50
    
    if (parallaxBox.value) {
      const scrollRate = window.scrollY * 0.15
      parallaxBox.value.style.transform = `translateY(${scrollRate}px)`
    }
  })

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible')
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0.15, rootMargin: '0px 0px -50px 0px' })

  document.querySelectorAll('.reveal').forEach((el, index) => {
    el.style.transitionDelay = `${(index % 3) * 0.15}s`
    observer.observe(el)
  })
})
</script>

<template>
  <div class="app-shell">
    <div class="fx-grid"></div>
    <div class="fx-noise"></div>
    <div class="fx-glow fx-glow-a"></div>
    <div class="fx-glow fx-glow-b"></div>

    <header class="topbar" :class="{ compact: isScrolled }">
      <div class="brand">
        <div class="brand-mark" aria-hidden="true"><span></span></div>
        <div>
          <p class="brand-overline">Premium Detailing</p>
          <h1 class="brand-title">Veloura Wash</h1>
        </div>
      </div>

      <nav class="nav">
        <a href="#services">Services</a>
        <a href="#experience">Experience</a>
        <a href="#process">Process</a>
        <a href="#pricing">Pricing</a>
        <a href="#reviews">Reviews</a>
      </nav>

      <a href="#contact" class="btn btn-primary nav-cta">Jetzt buchen</a>
    </header>

    <main>
      <section class="hero section">
        <div class="hero-copy reveal">
          <span class="eyebrow">3D Motion Automotive Experience</span>
          <h2>
            Drive <span class="text-cyan">clean</span>.<br />
            Launch like a
            <em class="text-glow">luxury brand</em>.
          </h2>
          <p>
            Eine kreative Premium-Car-Wash Website mit cineastischer Bildsprache,
            3D-Tilt-Hero, Neon-Licht, Parallax-Gefühl, animierten Preisblöcken,
            Trust-Elementen und klarer Booking-Conversion.
          </p>

          <div class="hero-actions">
            <a href="#pricing" class="btn btn-primary">Pakete entdecken</a>
            <a href="#experience" class="btn btn-ghost">Experience ansehen</a>
          </div>

          <div class="hero-stats">
            <article>
              <strong>12k+</strong>
              <span>Detailings pro Jahr</span>
            </article>
            <article>
              <strong>4.9/5</strong>
              <span>Premium Reviews</span>
            </article>
            <article>
              <strong>90 Min</strong>
              <span>Signature Finish</span>
            </article>
          </div>
        </div>

        <div
          class="hero-visual reveal"
          ref="heroCard"
          @mousemove="handleMove"
          @mouseleave="resetMove"
        >
          <div class="scan-line"></div>
          <div class="hero-panel top-panel">
            <span>Finish Quality</span>
            <strong>Mirror Gloss+</strong>
          </div>

          <div class="floating-orb orb-a"></div>
          <div class="floating-orb orb-b"></div>

          <div class="car-stage">
            <img
              src="https://pplx-res.cloudinary.com/image/upload/pplx_search_images/ef5b6e5fa944e5ce91947b3b8cc624227228c8e5.jpg"
              alt="Luxury sports car side view"
              width="1000"
              height="554"
              class="car-img"
            />
          </div>

          <div class="hero-panel bottom-panel">
            <span>Wash Stack</span>
            <strong>Foam · Polish · Shield</strong>
          </div>
        </div>
      </section>

      <section id="services" class="section">
        <div class="section-head reveal">
          <div>
            <p class="section-kicker">Signature Services</p>
            <h3>Luxus-Detailing mit Showroom-Effekt</h3>
          </div>
          <p class="section-text">
            Nicht einfach waschen, sondern inszenieren: starke Oberfläche,
            tiefes Finish, saubere Preisstruktur und ein Auftritt wie eine starke
            Automotive-Marke statt wie eine Standard-Dienstleisterseite.
          </p>
        </div>

        <div class="service-grid">
          <article class="glass-card reveal">
            <div class="icon-badge">✦</div>
            <h4>Hyper Foam Wash</h4>
            <p>Snow-Foam-Vorwäsche, Lackpflege und ein reflektionsstarkes Ergebnis.</p>
          </article>

          <article class="glass-card reveal">
            <div class="icon-badge">◈</div>
            <h4>Interior Reset</h4>
            <p>Tiefenreinigung für Sitze, Cockpit und Oberflächen mit Executive-Finish.</p>
          </article>

          <article class="glass-card reveal">
            <div class="icon-badge">⬡</div>
            <h4>Ceramic Shield</h4>
            <p>Hydrophober Schutz, langanhaltender Glanz und High-End-Exterior-Look.</p>
          </article>
        </div>
      </section>

      <section id="experience" class="section showcase">
        <div class="showcase-media glass-frame reveal parallax-box" ref="parallaxBox">
          <img
            src="https://pplx-res.cloudinary.com/image/upload/pplx_search_images/de788c4f90a0a2d49cb63b7b7170e964c02a1d8a.jpg"
            alt="Neon lit sports car showcase"
            width="1600"
            height="990"
            class="full-img"
          />
        </div>

        <div class="showcase-copy glass-frame reveal">
          <span class="chip">Visual Experience</span>
          <h3>Mehr als eine Seite — eine digitale Brand-Inszenierung</h3>
          <p>
            Lichtführung, Motion und Tiefenwirkung erzeugen genau den Eindruck,
            den eine Premium-Car-Wash-Marke braucht: modern, hochwertig,
            selbstbewusst und vertrauenswürdig.
          </p>
          <ul class="feature-list">
            <li>3D-Tilt-Hero mit räumlicher Tiefe.</li>
            <li>Luxury Dark Mode mit Cyan-Glow und starken Highlights.</li>
            <li>Klare CTAs für Buchung, Preise und Markenwirkung.</li>
          </ul>
        </div>
      </section>

      <section id="process" class="section">
        <div class="section-head reveal">
          <div>
            <p class="section-kicker">Process</p>
            <h3>Ein Ablauf, der schnell wirkt und premium aussieht</h3>
          </div>
          <p class="section-text">
            Dein Kunde soll sofort verstehen, wie einfach der Weg vom Klick bis zum
            perfekten Finish ist.
          </p>
        </div>

        <div class="timeline">
          <article class="timeline-step glass-card reveal">
            <span class="step-num">01</span>
            <h4>Booking</h4>
            <p>Termin online wählen, Paket festlegen und direkt starten.</p>
          </article>
          <article class="timeline-step glass-card reveal">
            <span class="step-num">02</span>
            <h4>Detailing</h4>
            <p>Außenreinigung, Innenraum-Finish und abgestimmter Pflegeprozess.</p>
          </article>
          <article class="timeline-step glass-card reveal">
            <span class="step-num">03</span>
            <h4>Reveal</h4>
            <p>Übergabe mit spiegelndem Glanz und starkem Premium-Eindruck.</p>
          </article>
        </div>
      </section>

      <section id="pricing" class="section">
        <div class="section-head reveal">
          <div>
            <p class="section-kicker">Pricing</p>
            <h3>Pakete mit echter Premium-Positionierung</h3>
          </div>
          <p class="section-text">
            Klare Angebotslogik, damit Kunden Standard, Signature und Elite sofort
            verstehen und dein Angebot hochwertiger wahrnehmen.
          </p>
        </div>

        <div class="pricing-grid">
          <article class="price-card reveal">
            <span class="chip">Start</span>
            <h4>Express Clean</h4>
            <div class="price">29€</div>
            <p>Schneller Außen-Refresh mit elegantem Finish.</p>
            <ul class="feature-list">
              <li>Foam Wash</li>
              <li>Felgenreinigung</li>
              <li>Dry Gloss Finish</li>
            </ul>
          </article>

          <article class="price-card featured reveal">
            <span class="chip">Most Wanted</span>
            <h4>Signature Detail</h4>
            <div class="price text-cyan">79€</div>
            <p>Das starke Kernpaket für maximalen Shine und Interior-Effekt.</p>
            <ul class="feature-list">
              <li>Exterior + Interior</li>
              <li>Dashboard & vacuum</li>
              <li>Glass perfection</li>
            </ul>
          </article>

          <article class="price-card reveal">
            <span class="chip">Elite</span>
            <h4>Ceramic Luxe</h4>
            <div class="price">149€</div>
            <p>Showroom-Optik mit Schutzschicht und High-End-Finish.</p>
            <ul class="feature-list">
              <li>Ceramic shield</li>
              <li>Deep polish</li>
              <li>Luxury finish pass</li>
            </ul>
          </article>
        </div>
      </section>

      <section id="reviews" class="section">
        <div class="section-head reveal">
          <div>
            <p class="section-kicker">Client Love</p>
            <h3>Social Proof mit Premium-Vibe</h3>
          </div>
          <p class="section-text">
            Bewertungen sind nicht nur Vertrauen, sondern Teil deiner Positionierung.
          </p>
        </div>

        <div class="review-grid">
          <article class="review-card reveal">
            <strong>„Sieht aus wie eine Luxusmarke, nicht wie ein kleiner Waschservice.“</strong>
            <p>Die Seite wirkt sofort hochwertig und macht direkt Lust zu buchen.</p>
            <span class="author">— Automotive Client</span>
          </article>
          <article class="review-card reveal">
            <strong>„Extrem modern, starkes Design, perfekter erster Eindruck.“</strong>
            <p>Vor allem das Hero und die Preisstruktur wirken sehr professionell.</p>
            <span class="author">— Premium Customer</span>
          </article>
          <article class="review-card reveal">
            <strong>„Genau so soll eine Car-Wash Brand im Jahr 2026 aussehen.“</strong>
            <p>Technisch clean, visuell stark und deutlich über dem Standard.</p>
            <span class="author">— Local Business Owner</span>
          </article>
        </div>
      </section>

      <section id="contact" class="section">
        <div class="contact-band glass-card reveal">
          <div class="contact-text">
            <p class="section-kicker">Ready to launch</p>
            <h3>Deine neue Car-Wash Website soll brutal gut aussehen.</h3>
            <p>
              Diese Version kombiniert starke Premium-Visuals, moderne Motion,
              3D-Feeling, Review-Trust und klare Verkaufsstruktur für einen deutlich
              stärkeren Online-Auftritt.
            </p>
          </div>
          <div class="hero-actions">
            <a href="mailto:booking@velourawash.de" class="btn btn-primary">Projekt starten</a>
            <a href="#pricing" class="btn btn-ghost">Preise ansehen</a>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<style>
/* Globale Resets */
* { box-sizing: border-box; margin: 0; padding: 0; }
body { background-color: #090a0f; font-family: 'Inter', sans-serif; color: #fff; }
a { text-decoration: none; color: inherit; }
li { list-style: none; margin-bottom: 0.5rem; }
</style>

<style scoped>
/* Basis-Variablen */
:root {
  --neon-cyan: #00e5ff;
  --dark-bg: #090a0f;
  --glass-bg: rgba(255, 255, 255, 0.03);
  --glass-border: rgba(255, 255, 255, 0.08);
}

.text-cyan { color: var(--neon-cyan); }
.text-glow { color: #fff; text-shadow: 0 0 10px var(--neon-cyan); font-style: normal; }

/* HINTERGRUND & SHELL */
.app-shell {
  background-color: var(--dark-bg);
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

.fx-grid {
  position: fixed;
  inset: 0;
  background-image: 
    linear-gradient(to right, rgba(255,255,255,0.03) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
  mask-image: radial-gradient(circle at 50% 50%, black, transparent 80%);
  z-index: 0;
  pointer-events: none;
  animation: gridMove 20s linear infinite;
}

@keyframes gridMove {
  0% { transform: translateY(0); }
  100% { transform: translateY(40px); }
}

.fx-glow {
  position: fixed;
  border-radius: 50%;
  filter: blur(120px);
  z-index: 0;
  opacity: 0.4;
  pointer-events: none;
}
.fx-glow-a { top: -10%; left: -10%; width: 50vw; height: 50vw; background: radial-gradient(circle, var(--neon-cyan), transparent 70%); animation: pulseGlow 8s ease-in-out infinite alternate; }
.fx-glow-b { bottom: 20%; right: -10%; width: 40vw; height: 40vw; background: radial-gradient(circle, #5b21b6, transparent 70%); }

@keyframes pulseGlow {
  0% { opacity: 0.2; transform: scale(0.8); }
  100% { opacity: 0.5; transform: scale(1.1); }
}

/* NAVIGATION */
.topbar {
  position: fixed;
  top: 0; width: 100%;
  display: flex; justify-content: space-between; align-items: center;
  padding: 1.5rem 5%;
  z-index: 100;
  transition: all 0.3s ease;
}
.topbar.compact {
  padding: 1rem 5%;
  background: rgba(9, 10, 15, 0.8);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--glass-border);
}
.brand { display: flex; align-items: center; gap: 1rem; }
.brand-overline { font-size: 0.7rem; text-transform: uppercase; letter-spacing: 2px; color: var(--neon-cyan); margin: 0; }
.brand-title { font-size: 1.2rem; margin: 0; font-weight: 700; }
.nav { display: flex; gap: 2rem; }
.nav a { font-size: 0.9rem; transition: color 0.3s; }
.nav a:hover { color: var(--neon-cyan); }

/* LAYOUT & TYPOGRAFIE */
main { position: relative; z-index: 10; padding: 0 5%; }
.section { padding: 6rem 0; }
.section-head { text-align: center; max-width: 600px; margin: 0 auto 4rem auto; }
.section-kicker, .eyebrow { color: var(--neon-cyan); text-transform: uppercase; letter-spacing: 2px; font-size: 0.8rem; font-weight: bold; display: block; margin-bottom: 0.5rem; }
h2 { font-size: 3.5rem; line-height: 1.1; margin-bottom: 1.5rem; }
h3 { font-size: 2.2rem; margin-bottom: 1rem; }
p { color: #a0a0a0; line-height: 1.6; }

/* HERO SECTION */
.hero { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; align-items: center; min-height: 100vh; padding-top: 8rem; }
.hero-actions { display: flex; gap: 1rem; margin: 2rem 0; }
.hero-stats { display: flex; gap: 2rem; margin-top: 3rem; padding-top: 2rem; border-top: 1px solid var(--glass-border); }
.hero-stats strong { display: block; font-size: 1.5rem; color: #fff; }
.hero-stats span { font-size: 0.8rem; color: #888; }

.hero-visual { position: relative; transform-style: preserve-3d; transition: transform 0.1s ease-out, box-shadow 0.1s ease-out; border-radius: 20px; z-index: 2; padding: 2rem; }
.car-stage { position: relative; z-index: 2; text-align: center; }
.car-img { max-width: 100%; height: auto; filter: drop-shadow(0 20px 30px rgba(0,0,0,0.5)); }

.hero-panel { position: absolute; background: var(--glass-bg); backdrop-filter: blur(10px); border: 1px solid var(--glass-border); padding: 1rem; border-radius: 12px; z-index: 3; }
.top-panel { top: 10%; right: 0; transform: translateZ(30px); }
.bottom-panel { bottom: 10%; left: 0; transform: translateZ(40px); }
.hero-panel span { display: block; font-size: 0.7rem; color: #888; }
.hero-panel strong { color: var(--neon-cyan); }

.scan-line { position: absolute; top: 0; left: 0; right: 0; height: 2px; background: var(--neon-cyan); box-shadow: 0 0 15px 2px var(--neon-cyan); opacity: 0.5; animation: scan 4s linear infinite; z-index: 10; pointer-events: none; }
@keyframes scan { 0% { top: 0%; opacity: 0; } 10% { opacity: 0.8; } 90% { opacity: 0.8; } 100% { top: 100%; opacity: 0; } }

.floating-orb { position: absolute; width: 150px; height: 150px; border-radius: 50%; background: var(--neon-cyan); filter: blur(60px); z-index: 1; animation: float 6s ease-in-out infinite; }
.orb-a { top: 10%; left: -5%; animation-delay: 0s; }
.orb-b { bottom: 10%; right: -5%; animation-delay: -3s; }
@keyframes float { 0%, 100% { transform: translateY(0px) scale(1); } 50% { transform: translateY(-30px) scale(1.2); } }

/* BUTTONS */
.btn { padding: 1rem 2rem; border-radius: 50px; font-weight: bold; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; transition: all 0.3s; display: inline-block; }
.btn-primary { background: linear-gradient(45deg, #00b4cc, var(--neon-cyan)); color: #000; box-shadow: 0 0 15px rgba(0, 229, 255, 0.3); }
.btn-primary:hover { box-shadow: 0 0 30px rgba(0, 229, 255, 0.6); transform: scale(1.05); }
.btn-ghost { border: 1px solid var(--neon-cyan); color: var(--neon-cyan); }
.btn-ghost:hover { background: rgba(0, 229, 255, 0.1); transform: scale(1.05); }

/* GRIDS & CARDS */
.service-grid, .pricing-grid, .review-grid, .timeline { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem; }

.glass-card, .price-card, .review-card {
  background: var(--glass-bg); backdrop-filter: blur(12px); border: 1px solid var(--glass-border); border-radius: 16px; padding: 2.5rem; transition: all 0.4s; position: relative; overflow: hidden;
}
.glass-card:hover, .price-card:hover { transform: translateY(-10px) scale(1.02); border-color: rgba(0, 229, 255, 0.3); box-shadow: 0 15px 30px rgba(0,0,0,0.5), 0 0 20px rgba(0, 229, 255, 0.1) inset; }

.icon-badge { font-size: 2rem; color: var(--neon-cyan); margin-bottom: 1rem; }
.price { font-size: 3rem; font-weight: bold; margin: 1rem 0; color: #fff; }
.chip { display: inline-block; padding: 0.3rem 0.8rem; background: rgba(0, 229, 255, 0.1); color: var(--neon-cyan); border-radius: 20px; font-size: 0.8rem; margin-bottom: 1rem; border: 1px solid rgba(0, 229, 255, 0.2); }
.feature-list li::before { content: "✓ "; color: var(--neon-cyan); }

.price-card.featured { border-color: var(--neon-cyan); box-shadow: 0 0 30px rgba(0, 229, 255, 0.1); }

/* SHOWCASE SECTION */
.showcase { display: grid; grid-template-columns: 1.5fr 1fr; gap: 4rem; align-items: center; }
.glass-frame { border-radius: 20px; overflow: hidden; border: 1px solid var(--glass-border); }
.full-img { width: 100%; height: 100%; object-fit: cover; }
.showcase-copy { padding: 3rem; background: var(--glass-bg); backdrop-filter: blur(10px); }

/* CONTACT BAND */
.contact-band { display: flex; justify-content: space-between; align-items: center; gap: 2rem; }

/* ANIMATIONEN */
.reveal { opacity: 0; transform: translateY(40px); transition: opacity 0.8s cubic-bezier(0.2, 0.8, 0.2, 1), transform 0.8s cubic-bezier(0.2, 0.8, 0.2, 1); }
.reveal.is-visible { opacity: 1; transform: translateY(0); }

@media (max-width: 900px) {
  .hero, .showcase, .contact-band { grid-template-columns: 1fr; text-align: center; flex-direction: column; }
  .nav { display: none; }
  h2 { font-size: 2.5rem; }
  .hero-actions { justify-content: center; }
}
</style>