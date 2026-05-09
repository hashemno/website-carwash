<template>
  <div class="page-shell">
    <header class="site-header">
      <div class="container nav">
        <a href="#start" class="brand">CarWash Premium</a>
        <nav class="nav-links">
          <a href="#leistungen">Leistungen</a>
          <a href="#preise">Preise</a>
          <a href="#galerie">Galerie</a>
          <a href="#kontakt">Kontakt</a>
        </nav>
        <a href="#kontakt" class="btn btn-primary">Termin anfragen</a>
      </div>
    </header>

    <main>
      <section id="start" class="hero">
        <div class="container hero-grid">
          <div class="hero-copy">
            <span class="eyebrow">Professionelle Fahrzeugpflege</span>
            <h1>Sauberer Auftritt für Ihr Fahrzeug.</h1>
            <p>
              Hochwertige Autowäsche, gründliche Innenreinigung und professionelle
              Pflegepakete für Privat- und Firmenkunden.
            </p>
            <div class="hero-actions">
              <a href="#preise" class="btn btn-primary">Preise ansehen</a>
              <button class="btn btn-secondary" @click="openModal('kontakt')">
                Kontakt öffnen
              </button>
            </div>
            <ul class="hero-points">
              <li>Schnelle Terminvergabe</li>
              <li>Faire Paketpreise</li>
              <li>Schonende Reinigung</li>
            </ul>
          </div>

          <div class="hero-card">
            <img
              src="https://images.unsplash.com/photo-1607861716497-e65ab29fc7ac?auto=format&fit=crop&w=1200&q=80"
              alt="Sauberes schwarzes Auto nach professioneller Wäsche"
            />
          </div>
        </div>
      </section>

      <section id="leistungen" class="section">
        <div class="container">
          <div class="section-head">
            <span class="eyebrow">Leistungen</span>
            <h2>Unsere Services</h2>
            <p>
              Klare Leistungen, transparente Angebote und ein gepflegtes Ergebnis
              für jedes Fahrzeug.
            </p>
          </div>

          <div class="grid three">
            <article class="card">
              <h3>Außenwäsche</h3>
              <p>
                Gründliche Reinigung von Karosserie, Scheiben, Spiegeln und Felgen
                mit schonenden Produkten.
              </p>
              <button class="text-link" @click="openModal('kontakt')">
                Jetzt anfragen
              </button>
            </article>

            <article class="card">
              <h3>Innenreinigung</h3>
              <p>
                Staubsaugen, Cockpitpflege, Reinigung von Fußmatten und
                Auffrischung des Innenraums.
              </p>
              <button class="text-link" @click="openModal('kontakt')">
                Jetzt anfragen
              </button>
            </article>

            <article class="card">
              <h3>Premium Paket</h3>
              <p>
                Kombination aus Außenwäsche, Innenreinigung und Detailpflege für
                ein rundum überzeugendes Ergebnis.
              </p>
              <button class="text-link" @click="openModal('kontakt')">
                Jetzt anfragen
              </button>
            </article>
          </div>
        </div>
      </section>

      <section id="preise" class="section section-alt">
        <div class="container">
          <div class="section-head">
            <span class="eyebrow">Preise</span>
            <h2>Einfach und transparent</h2>
            <p>Beispielpreise für eine übersichtliche und vertrauenswürdige Darstellung.</p>
          </div>

          <div class="grid three">
            <article class="price-card">
              <h3>Basic</h3>
              <div class="price">ab 14,90 €</div>
              <ul>
                <li>Außenwäsche</li>
                <li>Scheibenreinigung</li>
                <li>Felgenreinigung</li>
              </ul>
              <button class="btn btn-primary" @click="openModal('kontakt')">
                Buchen
              </button>
            </article>

            <article class="price-card featured">
              <h3>Komfort</h3>
              <div class="price">ab 29,90 €</div>
              <ul>
                <li>Außenwäsche</li>
                <li>Innenreinigung</li>
                <li>Cockpitpflege</li>
              </ul>
              <button class="btn btn-primary" @click="openModal('kontakt')">
                Buchen
              </button>
            </article>

            <article class="price-card">
              <h3>Premium</h3>
              <div class="price">ab 49,90 €</div>
              <ul>
                <li>Komplettreinigung</li>
                <li>Detailpflege</li>
                <li>Finish mit Glanzschutz</li>
              </ul>
              <button class="btn btn-primary" @click="openModal('kontakt')">
                Buchen
              </button>
            </article>
          </div>
        </div>
      </section>

      <section id="galerie" class="section">
        <div class="container">
          <div class="section-head">
            <span class="eyebrow">Galerie</span>
            <h2>Sauber. Gepflegt. Professionell.</h2>
          </div>

          <div class="gallery">
            <img
              src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1000&q=80"
              alt="Sportwagen vor dunklem Hintergrund"
            />
            <img
              src="https://images.unsplash.com/photo-1492144534655-ae79c964c9d7?auto=format&fit=crop&w=1000&q=80"
              alt="Gepflegtes Fahrzeug in Seitenansicht"
            />
            <img
              src="https://images.unsplash.com/photo-1511919884226-fd3cad34687c?auto=format&fit=crop&w=1000&q=80"
              alt="Sauberes Fahrzeug mit hochwertiger Lackoptik"
            />
          </div>
        </div>
      </section>

      <section id="kontakt" class="section section-dark">
        <div class="container contact-grid">
          <div>
            <span class="eyebrow">Kontakt</span>
            <h2>Wir beraten Sie gerne.</h2>
            <p>
              Rufen Sie uns an, schreiben Sie uns eine E-Mail oder besuchen Sie
              uns direkt vor Ort.
            </p>
          </div>

          <div class="contact-card">
            <p><strong>Telefon:</strong> 0123 456789</p>
            <p><strong>E-Mail:</strong> info@carwash-premium.de</p>
            <p><strong>Adresse:</strong> Musterstraße 1, 12345 Musterstadt</p>
            <p><strong>Öffnungszeiten:</strong> Mo–Sa 08:00–18:00 Uhr</p>
            <div class="contact-actions">
              <a class="btn btn-primary" href="tel:0123456789">Anrufen</a>
              <a class="btn btn-secondary" href="mailto:info@carwash-premium.de"
                >E-Mail senden</a
              >
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <div class="container footer-row">
        <p>© 2026 CarWash Premium. Alle Rechte vorbehalten.</p>
        <div class="footer-links">
          <button class="footer-link" @click="openModal('impressum')">Impressum</button>
          <button class="footer-link" @click="openModal('datenschutz')">
            Datenschutz
          </button>
          <button class="footer-link" @click="openModal('cookies')">Cookies</button>
        </div>
      </div>
    </footer>

    <div v-if="showCookieBanner" class="cookie-banner">
      <div class="cookie-inner">
        <p>
          Diese Website verwendet derzeit nur technisch notwendige Funktionen und
          keine aktivierten Analyse- oder Marketing-Cookies. Falls später Tracking
          eingebunden wird, ist dafür grundsätzlich eine vorherige Einwilligung
          erforderlich. [web:66][web:91]
        </p>
        <div class="cookie-actions">
          <button class="btn btn-primary" @click="acceptCookies">Verstanden</button>
          <button class="btn btn-secondary" @click="openModal('cookies')">
            Mehr Infos
          </button>
        </div>
      </div>
    </div>

    <div v-if="activeModal" class="modal-backdrop" @click="closeModal">
      <div class="modal" @click.stop>
        <div class="modal-head">
          <h3>{{ modalTitle }}</h3>
          <button class="close-btn" @click="closeModal">×</button>
        </div>

        <div class="modal-body" v-if="activeModal === 'impressum'">
          <p><strong>Angaben gemäß § 5 DDG</strong></p>
          <p>CarWash Premium</p>
          <p>Max Mustermann</p>
          <p>Musterstraße 1</p>
          <p>12345 Musterstadt</p>
          <p>Deutschland</p>
          <br />
          <p>Telefon: 0123 456789</p>
          <p>E-Mail: info@carwash-premium.de</p>
          <br />
          <p>Umsatzsteuer-ID: Wird ergänzt, sofern vorhanden.</p>
          <p>
            Hinweis: Für geschäftsmäßige Websites müssen Impressumsangaben leicht
            erkennbar, unmittelbar erreichbar und ständig verfügbar sein; verlangt
            werden insbesondere Name/Firma, ladungsfähige Anschrift und schnelle
            Kontaktmöglichkeiten. [page:2][web:88][web:90]
          </p>
        </div>

        <div class="modal-body" v-else-if="activeModal === 'datenschutz'">
          <p>
            Wir verarbeiten personenbezogene Daten nur, soweit dies zur Bereitstellung
            der Website, zur Beantwortung von Anfragen oder zur Kommunikation mit
            Interessenten erforderlich ist. Bei Datenverarbeitung im Internet sind
            insbesondere Verantwortlicher, Zwecke, Rechtsgrundlagen, Empfänger,
            Speicherdauer und Betroffenenrechte transparent zu informieren. [page:1]
          </p>
          <br />
          <p><strong>Verantwortlicher</strong></p>
          <p>CarWash Premium, Max Mustermann, Musterstraße 1, 12345 Musterstadt</p>
          <p>E-Mail: info@carwash-premium.de</p>
          <br />
          <p><strong>Zwecke und Rechtsgrundlagen</strong></p>
          <p>
            Verarbeitung zur Bereitstellung der Website, Bearbeitung von
            Kontaktanfragen und Wahrung berechtigter Interessen an sicherem und
            stabilem Betrieb der Website. Die Informationspflichten nach Art. 13
            DSGVO sollten in der Datenschutzerklärung vollständig abgebildet sein.
            [page:1]
          </p>
          <br />
          <p><strong>Betroffenenrechte</strong></p>
          <p>
            Auskunft, Berichtigung, Löschung, Einschränkung der Verarbeitung,
            Datenübertragbarkeit, Widerspruch sowie Beschwerde bei einer
            Datenschutzaufsichtsbehörde. [page:1]
          </p>
          <br />
          <p><strong>Wichtiger Hinweis</strong></p>
          <p>
            Diese Vorlage ersetzt keine individuelle Rechtsberatung. Sobald du
            Kontaktformular, Karten, Tracking, Newsletter oder externe Dienste
            einsetzt, muss die Erklärung angepasst werden. [page:1]
          </p>
        </div>

        <div class="modal-body" v-else-if="activeModal === 'cookies'">
          <p>
            Nach deutschem Recht ist für nicht notwendige Cookies oder vergleichbare
            Tracking-Technologien grundsätzlich eine vorherige Einwilligung nötig.
            Notwendige Cookies können ohne Einwilligung zulässig sein, wenn sie
            technisch erforderlich sind, um den ausdrücklich gewünschten Dienst
            bereitzustellen. [web:66][web:91]
          </p>
          <br />
          <p>
            Diese Demo-Seite nutzt aktuell kein Analytics- oder Marketing-Tracking.
            Deshalb ist hier nur ein transparenter Hinweis vorgesehen. Falls du
            später Google Analytics, Meta Pixel oder ähnliche Tools einbindest,
            brauchst du ein echtes Consent-Banner mit Ablehnen-Option. [web:66][web:91]
          </p>
        </div>

        <div class="modal-body" v-else-if="activeModal === 'kontakt'">
          <p><strong>Kontakt</strong></p>
          <p>Telefon: 0123 456789</p>
          <p>E-Mail: info@carwash-premium.de</p>
          <p>Adresse: Musterstraße 1, 12345 Musterstadt</p>
          <p>Öffnungszeiten: Mo–Sa 08:00–18:00 Uhr</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const activeModal = ref('')
const showCookieBanner = ref(true)

const openModal = (name) => {
  activeModal.value = name
}

const closeModal = () => {
  activeModal.value = ''
}

const acceptCookies = () => {
  showCookieBanner.value = false
}

const modalTitle = computed(() => {
  if (activeModal.value === 'impressum') return 'Impressum'
  if (activeModal.value === 'datenschutz') return 'Datenschutzerklärung'
  if (activeModal.value === 'cookies') return 'Cookie-Hinweis'
  if (activeModal.value === 'kontakt') return 'Kontakt'
  return ''
})
</script>

<style scoped>
:global(*) {
  box-sizing: border-box;
}

:global(html) {
  scroll-behavior: smooth;
}

:global(body) {
  margin: 0;
  font-family: Inter, Arial, sans-serif;
  background: #0b1220;
  color: #111827;
}

:global(a) {
  color: inherit;
}

.page-shell {
  background: #ffffff;
}

.container {
  width: min(1120px, calc(100% - 32px));
  margin: 0 auto;
}

.site-header {
  position: sticky;
  top: 0;
  z-index: 30;
  background: rgba(8, 15, 28, 0.88);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.nav {
  min-height: 76px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}

.brand {
  color: #ffffff;
  text-decoration: none;
  font-size: 24px;
  font-weight: 800;
}

.nav-links {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.nav-links a {
  color: #dbe4f0;
  text-decoration: none;
  font-size: 15px;
}

.hero {
  padding: 96px 0 72px;
  background:
    linear-gradient(135deg, rgba(5, 10, 20, 0.88), rgba(10, 32, 57, 0.72)),
    #0f172a;
  color: white;
}

.hero-grid {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 32px;
  align-items: center;
}

.eyebrow {
  display: inline-block;
  margin-bottom: 14px;
  color: #7dd3fc;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-size: 12px;
}

.hero-copy h1 {
  font-size: clamp(36px, 6vw, 64px);
  line-height: 1.04;
  margin: 0 0 18px;
}

.hero-copy p {
  font-size: 18px;
  line-height: 1.7;
  color: #dbe4f0;
  max-width: 60ch;
  margin: 0 0 28px;
}

.hero-actions,
.contact-actions,
.cookie-actions,
.footer-links {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

.hero-points {
  list-style: none;
  padding: 0;
  margin: 24px 0 0;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  color: #dbe4f0;
}

.hero-points li {
  background: rgba(255, 255, 255, 0.08);
  padding: 10px 14px;
  border-radius: 999px;
  font-size: 14px;
}

.hero-card img,
.gallery img {
  width: 100%;
  display: block;
  border-radius: 24px;
  object-fit: cover;
}

.hero-card img {
  min-height: 460px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
}

.section {
  padding: 88px 0;
}

.section-alt {
  background: #f3f7fb;
}

.section-dark {
  background: #0f172a;
  color: white;
}

.section-head {
  margin-bottom: 28px;
}

.section-head h2 {
  font-size: clamp(28px, 4vw, 44px);
  margin: 0 0 12px;
}

.section-head p {
  margin: 0;
  color: #4b5563;
  font-size: 17px;
  line-height: 1.7;
  max-width: 64ch;
}

.section-dark p,
.section-dark h2 {
  color: white;
}

.grid.three {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 22px;
}

.card,
.price-card,
.contact-card {
  background: white;
  border-radius: 20px;
  padding: 28px;
  box-shadow: 0 12px 30px rgba(15, 23, 42, 0.08);
}

.card h3,
.price-card h3 {
  margin-top: 0;
  margin-bottom: 12px;
  font-size: 24px;
}

.card p,
.price-card li,
.contact-card p,
.modal-body p {
  line-height: 1.7;
  font-size: 16px;
}

.text-link {
  background: transparent;
  border: none;
  padding: 0;
  margin-top: 18px;
  color: #0284c7;
  cursor: pointer;
  font-weight: 700;
}

.price-card {
  position: relative;
}

.price-card.featured {
  border: 2px solid #0ea5e9;
  transform: translateY(-4px);
}

.price {
  font-size: 34px;
  font-weight: 800;
  margin-bottom: 14px;
  color: #0f172a;
}

.price-card ul {
  padding-left: 18px;
  margin: 0 0 24px;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

.gallery img {
  height: 260px;
}

.contact-grid {
  display: grid;
  grid-template-columns: 0.9fr 1.1fr;
  gap: 24px;
  align-items: start;
}

.contact-card {
  color: #111827;
}

.site-footer {
  background: #08101d;
  color: #dbe4f0;
  padding: 28px 0;
}

.footer-row {
  display: flex;
  justify-content: space-between;
  gap: 18px;
  align-items: center;
  flex-wrap: wrap;
}

.footer-link,
.close-btn {
  background: transparent;
  border: none;
  color: inherit;
  cursor: pointer;
  font: inherit;
}

.btn {
  border: none;
  border-radius: 999px;
  padding: 14px 22px;
  font-weight: 700;
  cursor: pointer;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-primary {
  background: #0ea5e9;
  color: white;
}

.btn-secondary {
  background: white;
  color: #0f172a;
}

.cookie-banner {
  position: fixed;
  left: 16px;
  right: 16px;
  bottom: 16px;
  z-index: 60;
}

.cookie-inner {
  max-width: 980px;
  margin: 0 auto;
  background: #0f172a;
  color: white;
  border-radius: 20px;
  padding: 18px;
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.25);
}

.cookie-inner p {
  margin-top: 0;
  line-height: 1.7;
}

.modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(2, 6, 23, 0.72);
  display: grid;
  place-items: center;
  padding: 24px;
  z-index: 70;
}

.modal {
  width: min(760px, 100%);
  max-height: 85vh;
  overflow: auto;
  background: white;
  border-radius: 24px;
  padding: 24px;
}

.modal-head {
  display: flex;
  justify-content: space-between;
  gap: 16px;
  align-items: center;
  margin-bottom: 10px;
}

.modal-head h3 {
  margin: 0;
  font-size: 28px;
}

.close-btn {
  font-size: 28px;
  color: #111827;
}

@media (max-width: 900px) {
  .hero-grid,
  .grid.three,
  .gallery,
  .contact-grid {
    grid-template-columns: 1fr;
  }

  .nav {
    padding: 14px 0;
    align-items: flex-start;
    flex-direction: column;
  }

  .hero {
    padding-top: 52px;
  }

  .hero-card img {
    min-height: 300px;
  }
}

@media (max-width: 640px) {
  .section {
    padding: 64px 0;
  }

  .btn {
    width: 100%;
  }

  .footer-row,
  .hero-actions,
  .contact-actions,
  .cookie-actions {
    flex-direction: column;
    align-items: stretch;
  }
}
</style>