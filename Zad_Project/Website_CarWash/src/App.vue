<script setup>
import { ref, onMounted } from 'vue'

const isScrolled = ref(false)
const parallaxBox = ref(null)
const showCookieBanner = ref(true)

// --- VIDEO SETUP ---
// Pfad zum lokalen Video im public-Ordner
const videoUrl = '/carwash'

// Referenz für den HTML Video-Player
const videoPlayer = ref(null)
// ------------------

// Cookie Logik
const acceptCookies = () => {
  showCookieBanner.value = false
}

// --- TACHOMETER LOGIK START ---
const statsSection = ref(null)

const stats = ref([
  { label: 'Gepflegte Fahrzeuge', target: 3500, current: 0, suffix: '+' },
  { label: 'Jahre Erfahrung', target: 12, current: 0, suffix: '' },
  { label: 'Stammkunden', target: 99, current: 0, suffix: '%' }
])

const animateCounters = () => {
  const duration = 2000; // 2 Sekunden Dauer
  const frameDuration = 1000 / 60; // 60 FPS
  const totalFrames = Math.round(duration / frameDuration);

  stats.value.forEach(stat => {
    let frame = 0;
    const counter = setInterval(() => {
      frame++;
      const progress = frame / totalFrames;
      const easeOut = 1 - Math.pow(1 - progress, 3);
      
      stat.current = Math.round(stat.target * easeOut);

      if (frame === totalFrames) {
        clearInterval(counter);
        stat.current = stat.target;
      }
    }, frameDuration);
  });
}
// --- TACHOMETER LOGIK ENDE ---

// Scroll-Reveals & Header-Logik
onMounted(() => {
  
  // --- VIDEO AUTOPLAY FIX ---
  if (videoPlayer.value) {
    videoPlayer.value.play().catch(error => {
      console.log("Autoplay blockiert. Versuche es stummgeschaltet:", error)
      videoPlayer.value.muted = true
      videoPlayer.value.play()
    })
  }
  // --------------------------

  // Header Scroll-Effekt
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50
    
    // Parallax Effekt für das Bild
    if (parallaxBox.value) {
      const scrollRate = window.scrollY * 0.1
      parallaxBox.value.style.transform = `translateY(${scrollRate}px)`
    }
  })

  // Sanfte Einblend-Animationen für alle Elemente
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible')
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' })

  document.querySelectorAll('.reveal').forEach((el, index) => {
    el.style.transitionDelay = `${(index % 4) * 0.1}s`
    observer.observe(el)
  })

  // Observer für die Tachometer (Startet nur 1x wenn sichtbar)
  const statsObserver = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      animateCounters()
      statsObserver.disconnect()
    }
  }, { threshold: 0.5 })

  if (statsSection.value) {
    statsObserver.observe(statsSection.value)
  }
})
</script>

<template>
  <div class="app-shell">
    <!-- Header -->
    <header class="topbar" :class="{ compact: isScrolled }">
      <div class="brand">
        <div>
          <p class="brand-overline">Halle (Saale)</p>
          <h1 class="brand-title">Zad Carwash</h1>
        </div>
      </div>

      <nav class="nav">
        <a href="#services">Services</a>
        <a href="#experience">Handwerk</a>
        <a href="#pricing">Preise</a>
        <a href="#reviews">Reviews</a>
      </nav>

      <a href="#contact" class="btn btn-primary nav-cta">Termin buchen</a>
    </header>

    <!-- FULLSCREEN VIDEO HERO -->
    <section class="hero-fullscreen">
      <div class="video-background">
        <div class="video-overlay"></div>
        <video 
          ref="videoPlayer"
          :src="videoUrl"
          autoplay 
          loop 
          muted 
          playsinline
          class="bg-video">
        </video>
      </div>

      <!-- Pointer-events: none sorgt dafür, dass man durch den Text hindurch das Video klicken kann, falls nötig -->
      <div class="hero-content reveal" style="pointer-events: none;">
        <span class="eyebrow">Premium Car Detailing</span>
        <h2>
          Perfektion in jedem <span class="text-accent">Detail.</span>
        </h2>
        <p class="hero-subtitle">
          Echtes Handwerk, exklusive Pflege und spiegelnder Glanz. 
          Die Nummer 1 Adresse für Fahrzeugaufbereitung in Halle (Saale).
        </p>
        
        <!-- Buttons wieder anklickbar machen -->
        <div class="hero-actions" style="pointer-events: auto;">
          <a href="#pricing" class="btn btn-primary">Preise & Pakete</a>
          <a href="#experience" class="btn btn-ghost">Unsere Arbeit</a>
        </div>
      </div>
    </section>

    <main>
      <!-- Services -->
      <section id="services" class="section">
        <div class="section-head reveal">
          <p class="section-kicker">Signature Services</p>
          <h3>Detailing auf höchstem Niveau</h3>
          <p class="section-text">
            Keine kratzenden Bürsten, keine Kompromisse. Wir bieten schonende Handwäsche, 
            Tiefenreinigung und keramische Versiegelungen für Fahrzeuge, die mehr verdienen.
          </p>
        </div>

        <div class="service-grid">
          <article class="clean-card reveal">
            <div class="icon-badge">01</div>
            <h4>Hyper Foam Wash</h4>
            <p>Schonende Snow-Foam-Vorwäsche und lackschonende 2-Eimer-Handwäsche. Kratzerfrei und tiefenrein.</p>
          </article>

          <article class="clean-card reveal">
            <div class="icon-badge">02</div>
            <h4>Interior Reset</h4>
            <p>Tiefenreinigung für Polster, Leder und Cockpit. Entfernt Bakterien und bringt den Neuwagen-Duft zurück.</p>
          </article>

          <article class="clean-card reveal">
            <div class="icon-badge">03</div>
            <h4>Ceramic Shield</h4>
            <p>Mehrstufige Maschinenpolitur und Keramikbeschichtung für monatelangen, hydrophoben Abperleffekt.</p>
          </article>
        </div>
      </section>

      <!-- Experience / Handwerk -->
      <section id="experience" class="section showcase">
        <div class="showcase-text reveal">
          <span class="section-kicker">Echtes Handwerk</span>
          <h3>Keine Maschinen,<br>nur Präzision.</h3>
          <p>
            Wo Waschanlagen versagen, fangen wir an. In unserem modernen Detailing-Studio 
            in Halle nutzen wir Premium-Chemie, weiche Mikrofasern und viel Zeit, um den Lack 
            deines Fahrzeugs in einen spiegelnden Showroom-Zustand zu versetzen.
          </p>
          <ul class="feature-list">
            <li>Defektkorrektur & Kratzerentfernung</li>
            <li>Lackschonende pH-neutrale Reiniger</li>
            <li>Sicheres Trocknen per Luftgebläse</li>
          </ul>
        </div>

        <div class="showcase-image reveal" ref="parallaxBox">
          <img
            src="https://images.unsplash.com/photo-1601362840469-51e4d8d58785?q=80&w=1200&auto=format&fit=crop"
            alt="Professionelle Auto Politur"
            class="img-fluid"
          />
        </div>
      </section>

      <!-- Pricing -->
      <section id="pricing" class="section bg-light-mix">
        <div class="section-head reveal">
          <p class="section-kicker">Pakete</p>
          <h3>Klare Preise, maximaler Glanz</h3>
        </div>

        <div class="pricing-grid">
          <article class="price-card reveal">
            <h4>Express Hand Wash</h4>
            <div class="price">49€</div>
            <p>Die sichere Handwäsche für zwischendurch.</p>
            <ul class="feature-list-small">
              <li>Snow Foam Vorwäsche</li>
              <li>Handwäsche & Felgen</li>
              <li>Trocknung mit Luft</li>
            </ul>
          </article>

          <article class="price-card featured reveal">
            <div class="chip">Bestseller</div>
            <h4 class="text-accent">Signature Detail</h4>
            <div class="price text-accent">129€</div>
            <p>Unser Kernpaket für Außen- und Innenraum.</p>
            <ul class="feature-list-small">
              <li>Außenwäsche + Interior</li>
              <li>Kunststoff- & Lederpflege</li>
              <li>Sprühversiegelung (3 Monate)</li>
            </ul>
            <a href="#contact" class="btn btn-primary full-width">Paket wählen</a>
          </article>

          <article class="price-card reveal">
            <h4>Paint Correction</h4>
            <div class="price">ab 349€</div>
            <p>Lackaufbereitung für Enthusiasten.</p>
            <ul class="feature-list-small">
              <li>Maschinenpolitur</li>
              <li>Hologrammentfernung</li>
              <li>Keramikbeschichtung</li>
            </ul>
          </article>
        </div>
      </section>

      <!-- Stats / Tachometer -->
      <section id="stats" class="section" ref="statsSection">
        <div class="stats-grid">
          <div class="stat-card reveal" v-for="(stat, index) in stats" :key="index">
            <div class="stat-circle">
              <div class="stat-inner">
                <span class="stat-value">{{ stat.current }}</span>
                <span class="stat-suffix">{{ stat.suffix }}</span>
              </div>
            </div>
            <p class="stat-label">{{ stat.label }}</p>
          </div>
        </div>
      </section>

      <!-- Contact -->
      <section id="contact" class="section">
        <div class="contact-banner reveal">
          <div class="contact-content">
            <h3>Bereit für das perfekte Finish?</h3>
            <p>Sichere dir jetzt deinen Termin in unserem Studio in Halle.</p>
          </div>
          <div class="contact-btns">
            <a href="mailto:kontakt@zadcarwash.de" class="btn btn-primary">Termin anfragen</a>
          </div>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-brand">
          <h2 class="brand-title">Zad Carwash</h2>
          <p>Premium Detailing Halle</p>
        </div>
        <div class="footer-links">
          <strong>Rechtliches</strong>
          <a href="#impressum">Impressum</a>
          <a href="#datenschutz">Datenschutz</a>
          <a href="#agb">AGB</a>
        </div>
        <div class="footer-contact">
          <strong>Kontakt</strong>
          <p>Leipziger Str. 123<br>06108 Halle (Saale)</p>
          <p>kontakt@zadcarwash.de</p>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2026 Zad Carwash Halle. Alle Rechte vorbehalten.</p>
      </div>
    </footer>

    <!-- MODERN COOKIE BANNER -->
    <Transition name="fade">
      <div v-if="showCookieBanner" class="cookie-banner">
        <div class="cookie-content">
          <h4>Wir respektieren deine Privatsphäre</h4>
          <p>Diese Website verwendet Cookies, um dir das beste Erlebnis zu bieten. Einige sind essenziell, andere helfen uns, die Seite zu optimieren.</p>
        </div>
        <div class="cookie-actions">
          <button @click="showCookieBanner = false" class="btn-ghost-small">Nur essenzielle</button>
          <button @click="acceptCookies" class="btn btn-primary btn-small">Alle akzeptieren</button>
        </div>
      </div>
    </Transition>
  </div>
</template>

<style>
/* Globale Resets */
* { box-sizing: border-box; margin: 0; padding: 0; }
body { background-color: #0f172a; font-family: 'Inter', -apple-system, sans-serif; color: #f8fafc; line-height: 1.6; }
html { scroll-behavior: smooth; }
a { text-decoration: none; color: inherit; }
li { list-style: none; }
</style>

<style scoped>
:root {
  --neon-accent: #0ea5e9;
  --bg-dark: #0f172a; 
  --bg-card: rgba(255, 255, 255, 0.05);
  --bg-card-hover: rgba(255, 255, 255, 0.09);
  --glass-border: rgba(255, 255, 255, 0.12); 
  --text-main: #f8fafc;
  --text-muted: #cbd5e1;
}

.text-accent { color: var(--neon-accent); }
.app-shell { position: relative; overflow-x: hidden; }

/* HEADER */
.topbar {
  position: fixed; top: 0; width: 100%; display: flex; justify-content: space-between; align-items: center;
  padding: 1.5rem 5%; z-index: 100; transition: all 0.4s ease; border-bottom: 1px solid transparent;
}
.topbar.compact { padding: 1rem 5%; background: rgba(15, 23, 42, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid var(--glass-border); }
.brand-overline { font-size: 0.7rem; text-transform: uppercase; letter-spacing: 2px; color: var(--neon-accent); font-weight: 700; margin: 0; }
.brand-title { font-size: 1.5rem; font-weight: 800; margin: 0; letter-spacing: -0.5px; color: var(--text-main); }
.nav { display: flex; gap: 2rem; }
.nav a { font-size: 0.9rem; font-weight: 600; text-transform: uppercase; letter-spacing: 1px; color: var(--text-main); transition: color 0.3s; }
.nav a:hover { color: var(--neon-accent); }

/* FULLSCREEN HERO VIDEO */
.hero-fullscreen {
  position: relative; height: 100vh; display: flex; align-items: center; justify-content: center; text-align: center; padding: 0 5%;
}
.video-background { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; overflow: hidden; }
.bg-video { width: 100%; height: 100%; object-fit: cover; }

/* NEU: pointer-events: none sorgt dafür, dass das dunkle Overlay keine Klicks auf den Video-Player blockiert */
.video-overlay { 
  position: absolute; 
  inset: 0; 
  background: linear-gradient(to bottom, rgba(15, 23, 42, 0.5), var(--bg-dark)); 
  z-index: 1; 
  pointer-events: none; 
}

.hero-content { position: relative; z-index: 2; max-width: 800px; }
.eyebrow { color: var(--neon-accent); text-transform: uppercase; letter-spacing: 4px; font-size: 0.9rem; font-weight: 800; display: block; margin-bottom: 1rem; }
h2 { font-size: 4.5rem; line-height: 1.1; margin-bottom: 1.5rem; font-weight: 900; letter-spacing: -1px; color: #fff; }
.hero-subtitle { font-size: 1.3rem; color: #e2e8f0; margin-bottom: 2.5rem; text-shadow: 0 2px 4px rgba(0,0,0,0.5); }
.hero-actions { display: flex; gap: 1.5rem; justify-content: center; }

/* LAYOUT & TYPOGRAFIE */
.section { padding: 8rem 5%; max-width: 1400px; margin: 0 auto; }
.bg-light-mix { background-color: #1e293b; max-width: 100%; padding-left: 5%; padding-right: 5%; border-top: 1px solid var(--glass-border); border-bottom: 1px solid var(--glass-border); }
.section-head { text-align: center; max-width: 700px; margin: 0 auto 5rem auto; }
.section-kicker { color: var(--neon-accent); text-transform: uppercase; letter-spacing: 3px; font-size: 0.8rem; font-weight: 800; display: block; margin-bottom: 1rem; }
h3 { font-size: 3rem; margin-bottom: 1.5rem; font-weight: 800; line-height: 1.1; letter-spacing: -1px; color: var(--text-main); }
h4 { font-size: 1.5rem; margin-bottom: 1rem; font-weight: 700; color: var(--text-main); }
p { color: var(--text-muted); font-size: 1.1rem; }

/* BUTTONS */
.btn { padding: 1rem 2rem; border-radius: 8px; font-weight: 700; font-size: 1rem; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; transition: all 0.3s ease; display: inline-block; bor[...]
.btn-primary { background: var(--neon-accent); color: #fff; box-shadow: 0 4px 15px rgba(14, 165, 233, 0.4); }
.btn-primary:hover { background: #0284c7; transform: translateY(-2px); box-shadow: 0 6px 20px rgba(14, 165, 233, 0.6); }
.btn-ghost { border: 2px solid #fff; color: #fff; background: rgba(255,255,255,0.05); backdrop-filter: blur(5px); }
.btn-ghost:hover { background: #fff; color: var(--bg-dark); transform: translateY(-2px); }
.btn-small { padding: 0.8rem 1.5rem; font-size: 0.9rem; }
.btn-ghost-small { background: none; border: none; color: var(--text-muted); cursor: pointer; text-decoration: underline; font-size: 0.9rem; }
.full-width { width: 100%; text-align: center; margin-top: 1.5rem; }

/* GRIDS & CARDS */
.service-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 3rem; }
.clean-card { padding: 2.5rem; background: var(--bg-card); border-radius: 16px; border: 1px solid var(--glass-border); transition: all 0.3s; }
.clean-card:hover { background: var(--bg-card-hover); transform: translateY(-5px); border-color: rgba(255,255,255,0.2); }
.icon-badge { font-size: 1.5rem; color: var(--neon-accent); font-weight: 900; margin-bottom: 1rem; background: rgba(14, 165, 233, 0.1); display: inline-block; padding: 0.5rem 1rem; border-radius: 8px;[...]

/* SHOWCASE SECTION */
.showcase { display: grid; grid-template-columns: 1fr 1fr; gap: 6rem; align-items: center; }
.showcase-image { border-radius: 16px; overflow: hidden; box-shadow: 0 20px 40px rgba(0,0,0,0.4); }
.img-fluid { width: 100%; height: auto; display: block; object-fit: cover; }
.feature-list { margin-top: 2rem; }
.feature-list li { margin-bottom: 1rem; display: flex; align-items: center; gap: 0.8rem; font-size: 1.1rem; color: var(--text-main); }
.feature-list li::before { content: "✓"; color: var(--neon-accent); font-weight: bold; font-size: 1.2rem; }

/* PRICING */
.pricing-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem; max-width: 1200px; margin: 0 auto; }
.price-card { background: var(--bg-card); border: 1px solid var(--glass-border); border-radius: 16px; padding: 3rem 2rem; transition: transform 0.3s; position: relative; box-shadow: 0 10px 30px rgba(0[...]
.price-card:hover { transform: translateY(-10px); border-color: rgba(255,255,255,0.3); background: var(--bg-card-hover); }
.price-card.featured { border-color: var(--neon-accent); background: rgba(14, 165, 233, 0.05); }
.price { font-size: 3.5rem; font-weight: 900; color: var(--text-main); margin: 1rem 0; letter-spacing: -2px; }
.chip { position: absolute; top: -12px; left: 50%; transform: translateX(-50%); background: var(--neon-accent); color: #fff; padding: 0.3rem 1rem; font-size: 0.8rem; font-weight: bold; text-transform:[...]
.feature-list-small { margin-top: 2rem; }
.feature-list-small li { font-size: 0.95rem; margin-bottom: 0.8rem; border-bottom: 1px solid rgba(255,255,255,0.05); padding-bottom: 0.8rem; color: var(--text-muted); }

/* TACHOMETER / STATS */
.stats-grid { 
  display: grid; 
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); 
  gap: 3rem; 
  text-align: center; 
  max-width: 1000px; 
  margin: 0 auto; 
}
.stat-card { 
  display: flex; 
  flex-direction: column; 
  align-items: center; 
}
.stat-circle {
  width: 160px; 
  height: 160px;
  border-radius: 50%;
  border: 4px solid rgba(255, 255, 255, 0.05);
  border-top-color: var(--neon-accent);
  border-right-color: var(--neon-accent);
  display: flex; 
  justify-content: center; 
  align-items: center;
  margin-bottom: 1.5rem;
  background: var(--bg-card);
  box-shadow: inset 0 0 20px rgba(14, 165, 233, 0.05), 0 10px 30px rgba(0,0,0,0.3);
  transform: rotate(-45deg);
}
.stat-inner {
  transform: rotate(45deg);
  display: flex;
  align-items: baseline;
}
.stat-value { 
  font-size: 3rem; 
  font-weight: 900; 
  color: var(--text-main); 
  letter-spacing: -2px; 
}
.stat-suffix { 
  font-size: 1.5rem; 
  font-weight: 700; 
  color: var(--neon-accent); 
  margin-left: 2px; 
}
.stat-label { 
  font-size: 1rem; 
  color: var(--text-muted); 
  text-transform: uppercase; 
  letter-spacing: 2px; 
  font-weight: 600; 
}

/* CONTACT BANNER */
.contact-banner { background: linear-gradient(135deg, #0284c7, var(--neon-accent)); padding: 4rem; border-radius: 16px; display: flex; justify-content: space-between; align-items: center; flex-wrap: w[...]
.contact-banner h3 { margin: 0 0 0.5rem 0; color: #fff; font-size: 2.5rem; }
.contact-banner p { color: rgba(255,255,255,0.9); margin: 0; }
.contact-banner .btn-primary { background: #fff; color: #0f172a; box-shadow: none; }
.contact-banner .btn-primary:hover { background: #f1f5f9; transform: translateY(-2px); }

/* FOOTER */
.footer { background: #0b1120; padding: 5rem 5% 2rem; border-top: 1px solid var(--glass-border); }
.footer-grid { display: grid; grid-template-columns: 2fr 1fr 1fr; gap: 4rem; max-width: 1400px; margin: 0 auto 4rem; }
.footer-links, .footer-contact { display: flex; flex-direction: column; gap: 0.8rem; }
.footer strong { color: var(--text-main); font-size: 1.1rem; margin-bottom: 0.5rem; }
.footer a, .footer p { color: var(--text-muted); font-size: 0.95rem; transition: color 0.3s; }
.footer a:hover { color: var(--neon-accent); }
.footer-bottom { text-align: center; border-top: 1px solid rgba(255,255,255,0.05); padding-top: 2rem; color: #64748b; font-size: 0.85rem; }

/* COOKIE BANNER */
.cookie-banner {
  position: fixed; bottom: 2rem; left: 50%; transform: translateX(-50%);
  background: rgba(15, 23, 42, 0.95); backdrop-filter: blur(20px); border: 1px solid var(--glass-border);
  padding: 2rem; border-radius: 16px; width: 90%; max-width: 800px; z-index: 1000;
  display: flex; justify-content: space-between; align-items: center; gap: 2rem;
  box-shadow: 0 20px 50px rgba(0,0,0,0.5);
}
.cookie-content h4 { font-size: 1.1rem; margin-bottom: 0.5rem; color: var(--text-main); }
.cookie-content p { font-size: 0.9rem; margin: 0; color: var(--text-muted); }
.cookie-actions { display: flex; gap: 1rem; align-items: center; flex-shrink: 0; }

/* ANIMATIONEN */
.reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.8s ease-out, transform 0.8s ease-out; }
.reveal.is-visible { opacity: 1; transform: translateY(0); }
.fade-enter-active, .fade-leave-active { transition: opacity 0.4s ease, transform 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; transform: translate(-50%, 20px); }

/* RESPONSIVE */
@media (max-width: 992px) {
  .showcase { grid-template-columns: 1fr; gap: 4rem; }
  h2 { font-size: 3.5rem; }
  h3 { font-size: 2.5rem; }
  .footer-grid { grid-template-columns: 1fr; gap: 2rem; }
  .cookie-banner { flex-direction: column; align-items: flex-start; }
  .cookie-actions { width: 100%; justify-content: space-between; }
}
@media (max-width: 768px) {
  .nav { display: none; }
  h2 { font-size: 2.8rem; }
  .hero-actions { flex-direction: column; width: 100%; }
}
</style>
