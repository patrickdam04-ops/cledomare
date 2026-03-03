# Product Requirements Document (PRD) Avanzato: Cledo Mare Luxury Stay
**Versione:** 2.0 (Premium Showcase) | **Tipologia:** Single Page Application (Statica)

## 1. Architettura e Stack Tecnologico
Il progetto richiede un'esecuzione frontend "pixel-perfect" e ad altissime prestazioni, ottimizzata per Core Web Vitals (Target Lighthouse: 95+).
- **Core:** HTML5 Semantico.
- **Styling:** Tailwind CSS (via CDN) con configurazione estesa tramite script per variabili custom (Colori, Font, Spaziature).
- **Interattività:** Vanilla JavaScript (ES6+). Divieto di utilizzo di framework pesanti (React/Vue/Angular) o librerie come jQuery.
- **Smooth Scrolling:** Integrazione di **Lenis.js** via CDN per un'esperienza di scorrimento fluida e inerziale (tipica dei siti Awwwards), senza bloccare il native scroll.

## 2. Design System & Tipografia Fluida (Fluid UI)
Il design deve comunicare lusso silenzioso ("quiet luxury") attraverso un uso matematico dello spazio bianco.
- **Tipografia Fluida:** Utilizzare la funzione CSS `clamp()` per scalare i font in modo dinamico tra mobile e desktop, evitando salti bruschi nei breakpoint.
  - *Headings (H1, H2):* 'Cormorant Garamond' o 'Playfair Display' (Google Fonts). Lettere leggermente spaziate (`tracking-tight` per H1, `tracking-wide` per subtitoli).
  - *Body/Paragrafi:* 'Inter' o 'Outfit' (Google Fonts), peso 300/400, line-height `1.6` o `1.8` per massima leggibilità.
- **Palette Colori Estesa (Hex Codes preferenziali):**
  - `--bg-primary`: `#FAFAFA` (Bianco caldo/Off-white)
  - `--bg-secondary`: `#F3F2EE` (Greige leggero per staccare le sezioni)
  - `--text-primary`: `#1C1C1C` (Quasi nero per contrasto elevato)
  - `--text-muted`: `#6B7280` (Grigio elegante per descrizioni)
  - `--accent-gold`: `#D4AF37` (Uso rarissimo, solo per dettagli microscopici o underline)

## 3. Micro-interazioni e Reveal Animations (No Scrollytelling)
Nessuna animazione legata in modo sincrono alla scrollbar (no GSAP/ScrollTrigger pesanti). Utilizzare l'**Intersection Observer API** nativa per gestire l'ingresso degli elementi nella viewport.
- **Custom Easing:** Tutte le transizioni CSS devono usare curve di bezier personalizzate e lussuose, es: `cubic-bezier(0.76, 0, 0.24, 1)` (effetto morbido ed elegante).
- **Fade-Up Reveal:** Testi e card degli appartamenti devono apparire con un leggero `translateY(20px)` e `opacity: 0` -> `1` con una durata di `800ms` quando entrano nel campo visivo.
- **Hover States:** - *Immagini:* Effetto "Image Reveal" o leggerissimo scale `scale(1.03)` al passaggio del mouse, con `overflow-hidden` sul container.
  - *Bottoni:* Stile magnetico o riempimento del colore di background fluido.

## 4. Struttura Semantica dei Componenti
1. **Hero Section (`<header>`):** - Immagine full-viewport (`100dvh`). Caricamento prioritario (evitare lazy loading qui).
   - Overlay a gradiente lineare sottile (dal nero trasparente in basso a zero in alto) per garantire la leggibilità del titolo H1 bianco.
2. **Introduzione (`<section>`):** Layout asimmetrico. Testo a sinistra, una singola immagine di dettaglio (es. un vaso di design o uno scorcio di mare) a destra.
3. **Appartamenti (`<article>` per Cledo A e Cledo B):** - Architettura CSS Grid. Layout alternato (Immagine a sinistra/Testo a destra per l'A, viceversa per il B).
   - Utilizzo di tag `<ul>` minimali per i comfort, con icone SVG inline (es. Feather Icons).
4. **Galleria (`<section>`):**
   - CSS Grid Masonry Layout reale. Nessun margine/bordo visibile tra le foto, solo gap calcolati in `rem` (es. `gap-4` o `gap-6`).
   - Implementazione del **Lazy Loading** (`loading="lazy"`) per tutte le immagini sotto the fold.

## 5. Logica di Conversione e Infrastruttura Business
Il sito ha l'obiettivo di generare lead e dirottare le prenotazioni, mantenendo un'operatività snella in assenza di partita IVA. Di conseguenza, l'infrastruttura di checkout e l'integrazione di gateway di pagamento complessi (es. Stripe) sono rigorosamente escluse dal progetto.
- **Conversion Point 1 (Automated):** Bottoni "Verifica Disponibilità" stilizzati come Primary CTA, con link tracciabili diretti alle rispettive landing page di Booking.com.
- **Conversion Point 2 (Direct):** Pulsante flottante in basso a destra (Z-index elevato) per l'API di WhatsApp (`wa.me/numero`), con icona minimale e tooltip "Chatta con noi".
- Nessun carrello, nessun form di prenotazione interno con date-picker.

## 6. Accessibilità (A11Y) e SEO Tecnica
- Tutti i tag `<img>` devono avere attributi `alt` descrittivi.
- Contrasti colore verificati secondo standard WCAG 2.1 AA.
- Tag `<meta>` corretti per OpenGraph (per far apparire bene l'anteprima del sito quando il link viene condiviso su WhatsApp o Instagram).