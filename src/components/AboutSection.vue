<template>
  <section id="about" class="section about">
    <!-- Background glow -->
    <div class="glow-orb glow-mustard" style="width:600px;height:600px;top:50%;left:-200px;transform:translateY(-50%);opacity:0.4"></div>

    <div class="container about__inner">
      <!-- Left: Visual -->
      <div class="about__visual reveal" ref="visualRef">
        <div class="avatar-wrapper">
          <!-- Animated avatar placeholder -->
          <div class="avatar">
            <div class="avatar__initials">MN</div>
            <div class="avatar__ring ring-1"></div>
            <div class="avatar__ring ring-2"></div>
            <div class="avatar__ring ring-3"></div>
          </div>

          <!-- Floating badges -->
          <div class="float-badge float-badge--tl">
            <span class="badge badge-mustard">
              <svg width="10" height="10" viewBox="0 0 24 24" fill="currentColor"><circle cx="12" cy="12" r="10"/></svg>
              Available for hire
            </span>
          </div>
          <div class="float-badge float-badge--br">
            <span class="badge badge-burgundy">
              <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>
              Full Stack Dev
            </span>
          </div>
        </div>

        <!-- Tech stack quick icons -->
        <div class="about__tech-icons">
          <div v-for="tech in techIcons" :key="tech.name" class="tech-icon-pill" :title="tech.name">
            <span class="material-symbols-outlined tech-icon-emoji">{{ tech.icon }}</span>
            <span class="tech-icon-name">{{ tech.name }}</span>
          </div>
        </div>
      </div>

      <!-- Right: Content -->
      <div class="about__content">
        <div class="section-tag reveal" ref="tagRef">About Me</div>
        <h2 class="section-title reveal reveal-delay-1" ref="titleRef">
          Crafting <span>Digital</span><br>Experiences
        </h2>
        <div class="divider reveal reveal-delay-1"></div>

        <p class="about__text reveal reveal-delay-2">
          I'm <strong>Milani Ncana</strong>, a Software Developer with a passion for building
          web applications that are not just functional — they're <em>exceptional</em>. I bridge
          the gap between design and engineering, creating interfaces that users love and systems
          that scale.
        </p>
        <p class="about__text reveal reveal-delay-2">
          My journey in software development is driven by curiosity and a love for clean, efficient
          code. Whether I'm building a Spring Boot REST API or crafting a responsive
          Vue.js interface, I bring the same level of dedication and attention to detail.
        </p>

        <!-- Key values -->
        <div class="about__values reveal reveal-delay-3">
          <div v-for="val in values" :key="val.title" class="value-card">
            <div class="value-card__icon material-symbols-outlined">{{ val.icon }}</div>
            <div>
              <div class="value-card__title">{{ val.title }}</div>
              <div class="value-card__desc">{{ val.desc }}</div>
            </div>
          </div>
        </div>

        <!-- CTA -->
        <div class="about__ctas reveal reveal-delay-4">
          <a href="#contact" class="btn btn-primary">Let's Work Together</a>
          <a href="#experience" class="btn btn-outline">View Experience</a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const techIcons = [
  { name: 'Vue.js', icon: 'hub' },
  { name: 'Java', icon: 'local_cafe' },
  { name: 'Spring Boot', icon: 'eco' },
  { name: 'TypeScript', icon: 'code' },
  { name: 'JavaScript', icon: 'javascript' },
  { name: 'Bootstrap', icon: 'dashboard' },
  { name: 'HTML5', icon: 'html' },
  { name: 'SQL', icon: 'storage' },
]

const values = [
  { icon: 'gps_fixed', title: 'Clean Code', desc: 'Readable, maintainable, and well-structured' },
  { icon: 'rocket_launch', title: 'Performance', desc: 'Fast, optimized, and scalable solutions' },
  { icon: 'auto_awesome', title: 'UX Focused', desc: 'User experience is always the priority' },
]

const visualRef = ref(null)
const tagRef = ref(null)
const titleRef = ref(null)

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible')
        }
      })
    },
    { threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
  )
  document.querySelectorAll('#about .reveal').forEach(el => observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.about {
  background: var(--bg-primary);
  overflow: hidden;
}

.about__inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
  position: relative;
  z-index: 1;
}

/* ---- Visual Side ---- */
.about__visual {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 32px;
}

.avatar-wrapper {
  position: relative;
}

.avatar {
  width: 300px;
  height: 300px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--bg-surface-3), var(--bg-surface));
  border: 2px solid rgba(212, 160, 23, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: visible;
}

.avatar__initials {
  font-family: var(--font-display);
  font-size: 5rem;
  font-weight: 900;
  color: var(--mustard);
  text-shadow: 0 0 40px rgba(212, 160, 23, 0.4);
  z-index: 1;
}

.avatar__ring {
  position: absolute;
  border-radius: 50%;
  border: 1px solid;
  pointer-events: none;
}

.ring-1 {
  inset: -12px;
  border-color: rgba(212, 160, 23, 0.2);
  animation: rotate 12s linear infinite;
}

.ring-2 {
  inset: -28px;
  border-color: rgba(125, 17, 40, 0.15);
  animation: rotate 20s linear infinite reverse;
}

.ring-3 {
  inset: -48px;
  border-color: rgba(212, 160, 23, 0.07);
  animation: rotate 30s linear infinite;
}

/* Small dots on rings */
.ring-1::before, .ring-2::before {
  content: '';
  position: absolute;
  top: 0;
  left: 50%;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--mustard);
  transform: translateX(-50%) translateY(-50%);
}

.ring-2::before {
  background: var(--burgundy-light);
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* Float badges */
.float-badge {
  position: absolute;
  animation: float 4s ease-in-out infinite;
}

.float-badge--tl {
  top: 20px;
  left: -20px;
  animation-delay: 0s;
}

.float-badge--br {
  bottom: 30px;
  right: -20px;
  animation-delay: 2s;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

/* Tech icons */
.about__tech-icons {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
  max-width: 380px;
}

.tech-icon-pill {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 6px 12px;
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-full);
  transition: all 0.2s ease;
  cursor: default;
}

.tech-icon-pill:hover {
  border-color: var(--mustard);
  background: var(--mustard-subtle);
  transform: translateY(-2px);
}

.tech-icon-emoji {
  font-size: 1rem;
  line-height: 1;
}

.tech-icon-name {
  font-size: 0.78rem;
  font-weight: 500;
  color: var(--text-secondary);
}

/* ---- Content Side ---- */
.about__content {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.about__text {
  font-size: 1rem;
  line-height: 1.85;
  color: var(--text-secondary);
  margin-bottom: 16px;
}

.about__text strong {
  color: var(--text-primary);
  font-weight: 600;
}

.about__text em {
  color: var(--mustard);
  font-style: normal;
  font-weight: 500;
}

.about__values {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin: 24px 0 32px;
}

.value-card {
  display: flex;
  align-items: flex-start;
  gap: 16px;
  padding: 16px 20px;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  transition: all 0.2s ease;
}

.value-card:hover {
  border-color: var(--border-hover);
  background: var(--bg-card-hover);
  transform: translateX(4px);
}

.value-card__icon {
  font-size: 1.4rem;
  flex-shrink: 0;
  color: var(--mustard);
  line-height: 1;
}

.value-card__title {
  font-weight: 600;
  font-size: 0.9rem;
  color: var(--text-primary);
  margin-bottom: 2px;
}

.value-card__desc {
  font-size: 0.82rem;
  color: var(--text-muted);
}

.about__ctas {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

/* Responsive */
@media (max-width: 900px) {
  .about__inner {
    grid-template-columns: 1fr;
    gap: 48px;
  }
  .about__visual {
    order: -1;
  }
  .avatar {
    width: 220px;
    height: 220px;
  }
  .avatar__initials {
    font-size: 3.5rem;
  }
}
</style>
