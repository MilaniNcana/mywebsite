<template>
  <section id="home" class="hero">
    <!-- Particle Canvas -->
    <canvas ref="canvasRef" class="hero__canvas"></canvas>

    <!-- Background grid -->
    <div class="hero__grid"></div>

    <!-- Glow orbs -->
    <div class="glow-orb glow-mustard" style="width:500px;height:500px;top:-100px;right:-100px;opacity:0.6"></div>
    <div class="glow-orb glow-burgundy" style="width:400px;height:400px;bottom:0;left:-80px;opacity:0.5"></div>

    <div class="container hero__content">
      <!-- Greeting -->
      <div class="hero__greeting reveal" :class="{ visible: loaded }">
        <span class="hero__greeting-text">
          <span class="mono-accent material-symbols-outlined" style="font-size:1.1rem;vertical-align:middle">waving_hand</span> Hello, World! I'm
        </span>
      </div>

      <!-- Name -->
      <h1 class="hero__name reveal reveal-delay-1" :class="{ visible: loaded }">
        <span class="name-word">Milani</span>
        <span class="name-word name-accent">Ncana</span>
      </h1>

      <!-- Typing subtitle -->
      <div class="hero__subtitle reveal reveal-delay-2" :class="{ visible: loaded }">
        <span class="subtitle-prefix">I build</span>
        <span class="typing-wrapper">
          <span class="typing-text">{{ displayText }}</span>
          <span class="typing-cursor" :class="{ blink: !isTyping }">|</span>
        </span>
      </div>

      <!-- Description -->
      <p class="hero__description reveal reveal-delay-3" :class="{ visible: loaded }">
        A Junior Software Developer based in Cape Town, building web and desktop
        applications with Vue.js, Java &amp; Spring Boot. Translating requirements
        into functional systems through clean code and solid engineering.
      </p>

      <!-- CTA Buttons -->
      <div class="hero__ctas reveal reveal-delay-4" :class="{ visible: loaded }">
        <a href="#projects" class="btn btn-primary hero__btn">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>
          View My Work
        </a>
        <a href="#contact" class="btn btn-outline hero__btn">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
          Get In Touch
        </a>
        <a href="mailto:milanincana@outlook.com?subject=CV%20Request&body=Hi%20Milani%2C%0A%0AI%20would%20like%20to%20request%20a%20copy%20of%20your%20CV." class="btn btn-burgundy hero__btn">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
          CV
        </a>
      </div>

      <!-- Stats bar -->
      <div class="hero__stats reveal reveal-delay-5" :class="{ visible: loaded }">
        <div v-for="stat in stats" :key="stat.label" class="hero__stat">
          <span class="stat-value">{{ stat.value }}</span>
          <span class="stat-label">{{ stat.label }}</span>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <a href="#about" class="scroll-indicator" aria-label="Scroll down">
      <span class="scroll-indicator__text">Scroll</span>
      <div class="scroll-indicator__line">
        <div class="scroll-indicator__dot"></div>
      </div>
    </a>

    <!-- Social sidebar -->
    <div class="hero__socials">
      <a href="https://github.com/MilaniNcana" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="GitHub">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
      </a>
      <a href="https://linkedin.com/in/milanincana" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="LinkedIn">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
      </a>
      <a href="mailto:milanincana@outlook.com" class="social-link" aria-label="Email">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      </a>
      <div class="social-line"></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
const loaded = ref(false)
const displayText = ref('')
const isTyping = ref(true)

const stats = [
  { value: '2+', label: 'Years Experience' },
  { value: '15+', label: 'Projects Built' },
  { value: '8+', label: 'Technologies' },
  { value: '100%', label: 'Dedication' },
]

const roles = [
  'Full Stack Applications',
  'Beautiful UIs with Vue.js',
  'Robust APIs with Spring Boot',
  'Scalable Web Solutions',
  'Seamless User Experiences',
]

let roleIndex = 0
let charIndex = 0
let typingTimeout = null

function typeText() {
  const current = roles[roleIndex]
  if (charIndex < current.length) {
    displayText.value = current.slice(0, ++charIndex)
    isTyping.value = true
    typingTimeout = setTimeout(typeText, 60)
  } else {
    isTyping.value = false
    typingTimeout = setTimeout(eraseText, 2200)
  }
}

function eraseText() {
  if (charIndex > 0) {
    displayText.value = displayText.value.slice(0, --charIndex)
    isTyping.value = true
    typingTimeout = setTimeout(eraseText, 35)
  } else {
    roleIndex = (roleIndex + 1) % roles.length
    typingTimeout = setTimeout(typeText, 400)
  }
}

// Canvas Particle System
let animFrame = null
let particles = []

function initCanvas() {
  const canvas = canvasRef.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')

  function resize() {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
  }
  resize()
  window.addEventListener('resize', resize)

  const PARTICLE_COUNT = Math.min(60, Math.floor(window.innerWidth / 20))

  class Particle {
    constructor() { this.reset() }
    reset() {
      this.x = Math.random() * canvas.width
      this.y = Math.random() * canvas.height
      this.size = Math.random() * 2 + 0.5
      this.speedX = (Math.random() - 0.5) * 0.4
      this.speedY = (Math.random() - 0.5) * 0.4
      this.opacity = Math.random() * 0.5 + 0.1
      this.color = Math.random() > 0.6 ? '#D4A017' : Math.random() > 0.5 ? '#7D1128' : '#444'
    }
    update() {
      this.x += this.speedX
      this.y += this.speedY
      if (this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) {
        this.reset()
      }
    }
    draw() {
      ctx.save()
      ctx.globalAlpha = this.opacity
      ctx.fillStyle = this.color
      ctx.beginPath()
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2)
      ctx.fill()
      ctx.restore()
    }
  }

  particles = Array.from({ length: PARTICLE_COUNT }, () => new Particle())

  function drawLines() {
    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x
        const dy = particles[i].y - particles[j].y
        const dist = Math.sqrt(dx * dx + dy * dy)
        if (dist < 120) {
          ctx.save()
          ctx.globalAlpha = (1 - dist / 120) * 0.08
          ctx.strokeStyle = '#D4A017'
          ctx.lineWidth = 0.5
          ctx.beginPath()
          ctx.moveTo(particles[i].x, particles[i].y)
          ctx.lineTo(particles[j].x, particles[j].y)
          ctx.stroke()
          ctx.restore()
        }
      }
    }
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    particles.forEach(p => { p.update(); p.draw() })
    drawLines()
    animFrame = requestAnimationFrame(animate)
  }
  animate()

  return () => {
    window.removeEventListener('resize', resize)
    cancelAnimationFrame(animFrame)
  }
}

let cleanupCanvas = null

onMounted(() => {
  setTimeout(() => { loaded.value = true }, 100)
  typingTimeout = setTimeout(typeText, 800)
  cleanupCanvas = initCanvas()
})

onUnmounted(() => {
  clearTimeout(typingTimeout)
  cleanupCanvas?.()
})
</script>

<style scoped>
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background: var(--bg-base);
}

.hero__canvas {
  position: absolute;
  inset: 0;
  z-index: 0;
}

.hero__grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
  background-size: 60px 60px;
  z-index: 0;
  mask-image: radial-gradient(ellipse at center, black 0%, transparent 70%);
}

.hero__content {
  position: relative;
  z-index: 1;
  padding-top: 120px;
  padding-bottom: 80px;
  max-width: 900px;
}

/* Greeting */
.hero__greeting {
  margin-bottom: 16px;
}

.hero__greeting-text {
  font-family: var(--font-mono);
  font-size: 1rem;
  color: var(--text-secondary);
  letter-spacing: 0.05em;
}

.mono-accent {
  margin-right: 4px;
}

/* Name */
.hero__name {
  font-size: clamp(3.5rem, 10vw, 7rem);
  font-weight: 900;
  line-height: 1.0;
  letter-spacing: -0.03em;
  margin-bottom: 24px;
  display: flex;
  flex-wrap: wrap;
  gap: 0 20px;
}

.name-word {
  display: inline-block;
}

.name-accent {
  color: var(--mustard);
  -webkit-text-stroke: 0;
  text-shadow: 0 0 60px rgba(212, 160, 23, 0.3);
}

/* Subtitle */
.hero__subtitle {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
  font-size: clamp(1.2rem, 3vw, 1.6rem);
  font-weight: 600;
  font-family: var(--font-display);
  margin-bottom: 28px;
  min-height: 2.5rem;
}

.subtitle-prefix {
  color: var(--text-secondary);
}

.typing-wrapper {
  display: inline-flex;
  align-items: center;
  color: var(--mustard);
}

.typing-text {
  border-bottom: 2px solid var(--burgundy);
}

.typing-cursor {
  color: var(--burgundy);
  font-weight: 300;
  margin-left: 2px;
  transition: opacity 0.1s;
}

.typing-cursor.blink {
  animation: blink 0.8s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1 }
  50% { opacity: 0 }
}

/* Description */
.hero__description {
  font-size: 1.05rem;
  color: var(--text-secondary);
  line-height: 1.8;
  max-width: 580px;
  margin-bottom: 40px;
}

/* CTAs */
.hero__ctas {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  margin-bottom: 60px;
}

.hero__btn {
  font-size: 0.95rem;
}

/* Stats */
.hero__stats {
  display: flex;
  flex-wrap: wrap;
  gap: 40px;
  padding-top: 40px;
  border-top: 1px solid var(--border);
}

.hero__stat {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.stat-value {
  font-family: var(--font-display);
  font-size: 2rem;
  font-weight: 800;
  color: var(--mustard);
  line-height: 1;
}

.stat-label {
  font-size: 0.8rem;
  color: var(--text-muted);
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  text-decoration: none;
  z-index: 1;
  opacity: 0.5;
  transition: opacity 0.2s;
}

.scroll-indicator:hover {
  opacity: 1;
}

.scroll-indicator__text {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.scroll-indicator__line {
  width: 1.5px;
  height: 50px;
  background: linear-gradient(to bottom, var(--mustard), transparent);
  position: relative;
  overflow: hidden;
}

.scroll-indicator__dot {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 4px;
  height: 4px;
  border-radius: 50%;
  background: var(--mustard);
  animation: scrollDot 1.5s ease-in-out infinite;
}

@keyframes scrollDot {
  0% { top: 0; opacity: 1; }
  100% { top: 100%; opacity: 0; }
}

/* Social sidebar */
.hero__socials {
  position: fixed;
  bottom: 0;
  left: 32px;
  z-index: 10;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
}

.social-link {
  color: var(--text-muted);
  transition: all 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.social-link:hover {
  color: var(--mustard);
  transform: translateY(-2px);
}

.social-line {
  width: 1.5px;
  height: 80px;
  background: linear-gradient(to bottom, var(--text-muted), transparent);
}

@media (max-width: 768px) {
  .hero__socials {
    display: none;
  }
  .hero__stats {
    gap: 24px;
  }
  .hero__ctas {
    flex-direction: column;
    align-items: flex-start;
  }
  .scroll-indicator {
    display: none;
  }
}
</style>
