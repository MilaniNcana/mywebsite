<template>
  <!-- Floating trigger button -->
  <button class="surprise-btn" @click="trigger" :class="{ 'surprise-btn--spin': spinning }" aria-label="Surprise Me">
    <span class="material-symbols-outlined">auto_awesome</span>
    <span class="surprise-btn__label">Surprise Me</span>
  </button>

  <!-- Modal overlay -->
  <Teleport to="body">
    <Transition name="surprise-fade">
      <div v-if="show" class="surprise-overlay" @click.self="close">
        <div class="surprise-card" :class="{ 'surprise-card--pop': popped }">
          <!-- Close -->
          <button class="surprise-close" @click="close" aria-label="Close">
            <span class="material-symbols-outlined">close</span>
          </button>

          <!-- Type badge -->
          <div class="surprise-type">
            <span class="material-symbols-outlined surprise-type__icon">{{ current.typeIcon }}</span>
            {{ current.type }}
          </div>

          <!-- Content -->
          <div class="surprise-content">
            <div class="surprise-visual">
              <span class="material-symbols-outlined surprise-visual__icon">{{ current.icon }}</span>
            </div>
            <h2 class="surprise-title">{{ current.title }}</h2>
            <p class="surprise-body">{{ current.body }}</p>
            <div v-if="current.tags" class="surprise-tags">
              <span v-for="tag in current.tags" :key="tag" class="surprise-tag">{{ tag }}</span>
            </div>
          </div>

          <!-- Footer -->
          <div class="surprise-footer">
            <button class="surprise-next" @click="next">
              <span class="material-symbols-outlined">shuffle</span>
              Another one
            </button>
            <span class="surprise-count">{{ clickCount }} {{ clickCount === 1 ? 'surprise' : 'surprises' }} so far</span>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { ref, computed } from 'vue'

const show = ref(false)
const spinning = ref(false)
const popped = ref(false)
const clickCount = ref(0)
const currentIndex = ref(0)

const items = [
  // Projects
  {
    type: 'Project',
    typeIcon: 'folder_special',
    icon: 'hub',
    title: 'Trogster',
    body: 'A task management system where I designed and built the entire frontend from scratch using Vue 3, Vite & TypeScript. CORS is already in place for when the Android app ships.',
    tags: ['Vue 3', 'TypeScript', 'CORS', 'Vite'],
  },
  {
    type: 'Project',
    typeIcon: 'folder_special',
    icon: 'storefront',
    title: 'RentMyStuff',
    body: 'Built entirely solo — frontend in Vue 3 + JavaScript and a full Spring Boot microservices backend with PostgreSQL in production. A peer-to-peer rental marketplace.',
    tags: ['Vue 3', 'Spring Boot', 'PostgreSQL', 'Microservices'],
  },
  {
    type: 'Project',
    typeIcon: 'folder_special',
    icon: 'directions_car',
    title: 'Car Rental System',
    body: 'Responsible for the login and full dashboard module — full stack using Java, Spring Boot, and PostgreSQL. Clean MVC architecture throughout.',
    tags: ['Java', 'Spring Boot', 'PostgreSQL'],
  },
  {
    type: 'Project',
    typeIcon: 'folder_special',
    icon: 'checkroom',
    title: 'StyleForLess',
    body: 'A second-hand fashion marketplace. I built the Bootstrap-based frontend using Vue.js — making high-end style accessible to everyone.',
    tags: ['Bootstrap', 'Vue.js'],
  },
  // Skills
  {
    type: 'Skill',
    typeIcon: 'code',
    icon: 'hub',
    title: 'Vue 3 & TypeScript',
    body: 'My primary frontend stack. I love the Composition API, reactivity system, and how TypeScript makes large codebases maintainable.',
    tags: ['Vue 3', 'Vite', 'TypeScript', 'Composition API'],
  },
  {
    type: 'Skill',
    typeIcon: 'code',
    icon: 'eco',
    title: 'Spring Boot',
    body: 'I build production REST APIs with Spring Boot — from endpoint design to service layers, JPA repositories, and MVC architecture.',
    tags: ['Java', 'REST API', 'MVC', 'JPA'],
  },
  {
    type: 'Skill',
    typeIcon: 'code',
    icon: 'terminal',
    title: 'Python',
    body: 'Used Python during my internship at EOH for enterprise system development — scripting, data handling, and automation tasks.',
    tags: ['Python', 'Scripting', 'Automation'],
  },
  {
    type: 'Skill',
    typeIcon: 'code',
    icon: 'support_agent',
    title: 'Technical Support',
    body: 'At Manyano High School I handled everything — hardware repairs, networking, system imaging, and training staff on new technology.',
    tags: ['L1/L2 Support', 'Windows', 'Networking', 'Training'],
  },
  // Fun Facts
  {
    type: 'Fun Fact',
    typeIcon: 'lightbulb',
    icon: 'location_city',
    title: 'Cape Town Born & Built',
    body: 'Every line of code was written in Cape Town — one of Africa\'s fastest-growing tech hubs, right between the mountains and the sea.',
    tags: [],
  },
  {
    type: 'Fun Fact',
    typeIcon: 'lightbulb',
    icon: 'school',
    title: 'Three Qualifications',
    body: 'Milani holds a National Diploma in ICT Application Development, a Higher Certificate in IT Service Management, and a National Certificate in IT & Computer Science — all from Cape Town institutions.',
    tags: ['CPUT', 'False Bay College'],
  },
  {
    type: 'Fun Fact',
    typeIcon: 'lightbulb',
    icon: 'devices',
    title: 'Android Is Coming',
    body: 'CORS is already implemented in Trogster\'s frontend — an Android app is on the roadmap and the groundwork is laid.',
    tags: ['Mobile', 'CORS', 'Trogster'],
  },
  {
    type: 'Fun Fact',
    typeIcon: 'lightbulb',
    icon: 'psychology',
    title: 'Teacher at Heart',
    body: 'Before writing production code, Milani trained school staff on how to use technology — proving that great developers also make great communicators.',
    tags: [],
  },
]

const current = computed(() => items[currentIndex.value])

function pickRandom(exclude) {
  let idx
  do { idx = Math.floor(Math.random() * items.length) } while (idx === exclude && items.length > 1)
  return idx
}

function trigger() {
  spinning.value = true
  setTimeout(() => { spinning.value = false }, 600)
  currentIndex.value = pickRandom(currentIndex.value)
  clickCount.value++
  show.value = true
  setTimeout(() => { popped.value = true }, 20)
}

function next() {
  popped.value = false
  setTimeout(() => {
    currentIndex.value = pickRandom(currentIndex.value)
    clickCount.value++
    popped.value = true
  }, 150)
}

function close() {
  popped.value = false
  setTimeout(() => { show.value = false }, 200)
}
</script>

<style scoped>
/* ── Floating button ── */
.surprise-btn {
  position: fixed;
  bottom: 88px;
  right: 32px;
  z-index: 49;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 18px;
  background: linear-gradient(135deg, #7D1128, #9B1635);
  color: #fff;
  border: none;
  border-radius: 999px;
  font-size: 0.85rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  box-shadow: 0 4px 24px rgba(125, 17, 40, 0.45);
  transition: all 0.25s ease;
}

.surprise-btn:hover {
  transform: translateY(-3px) scale(1.04);
  box-shadow: 0 8px 32px rgba(125, 17, 40, 0.6);
}

.surprise-btn .material-symbols-outlined {
  font-size: 1.1rem;
  transition: transform 0.6s ease;
}

.surprise-btn--spin .material-symbols-outlined {
  transform: rotate(360deg);
}

.surprise-btn__label {
  white-space: nowrap;
}

@media (max-width: 600px) {
  .surprise-btn {
    bottom: 80px;
    right: 16px;
    padding: 10px 14px;
  }
  .surprise-btn__label {
    display: none;
  }
}

/* ── Overlay ── */
.surprise-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(8px);
  z-index: 1001;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

/* ── Card ── */
.surprise-card {
  background: var(--bg-card, #141414);
  border: 1px solid rgba(212, 160, 23, 0.25);
  border-radius: 20px;
  padding: 36px;
  max-width: 480px;
  width: 100%;
  position: relative;
  transform: scale(0.88) translateY(20px);
  opacity: 0;
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1), opacity 0.25s ease;
  box-shadow: 0 24px 80px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(212,160,23,0.1);
}

.surprise-card--pop {
  transform: scale(1) translateY(0);
  opacity: 1;
}

/* ── Close ── */
.surprise-close {
  position: absolute;
  top: 16px;
  right: 16px;
  background: rgba(255,255,255,0.06);
  border: none;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: rgba(255,255,255,0.5);
  transition: all 0.2s;
}

.surprise-close:hover {
  background: rgba(255,255,255,0.12);
  color: #fff;
}

.surprise-close .material-symbols-outlined {
  font-size: 1rem;
}

/* ── Type badge ── */
.surprise-type {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #D4A017;
  background: rgba(212, 160, 23, 0.1);
  border: 1px solid rgba(212, 160, 23, 0.2);
  border-radius: 999px;
  padding: 4px 12px;
  margin-bottom: 24px;
}

.surprise-type__icon {
  font-size: 0.85rem;
}

/* ── Content ── */
.surprise-content {
  text-align: center;
  margin-bottom: 28px;
}

.surprise-visual {
  width: 72px;
  height: 72px;
  background: linear-gradient(135deg, rgba(212,160,23,0.15), rgba(125,17,40,0.15));
  border: 1px solid rgba(212,160,23,0.2);
  border-radius: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px;
}

.surprise-visual__icon {
  font-size: 2rem;
  color: #D4A017;
}

.surprise-title {
  font-size: 1.4rem;
  font-weight: 800;
  color: #fff;
  margin-bottom: 12px;
  font-family: 'Space Grotesk', sans-serif;
}

.surprise-body {
  font-size: 0.9rem;
  color: rgba(255,255,255,0.65);
  line-height: 1.75;
  margin-bottom: 16px;
}

.surprise-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  justify-content: center;
}

.surprise-tag {
  padding: 4px 12px;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 999px;
  font-size: 0.75rem;
  color: rgba(255,255,255,0.5);
  font-family: 'JetBrains Mono', monospace;
}

/* ── Footer ── */
.surprise-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 20px;
  border-top: 1px solid rgba(255,255,255,0.08);
  gap: 12px;
}

.surprise-next {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 9px 20px;
  background: #D4A017;
  color: #0B0B0B;
  border: none;
  border-radius: 999px;
  font-size: 0.85rem;
  font-weight: 700;
  font-family: inherit;
  cursor: pointer;
  transition: all 0.2s ease;
}

.surprise-next:hover {
  background: #e0b020;
  transform: translateY(-1px);
}

.surprise-next .material-symbols-outlined {
  font-size: 1rem;
}

.surprise-count {
  font-size: 0.75rem;
  color: rgba(255,255,255,0.3);
  font-family: 'JetBrains Mono', monospace;
}

/* ── Transition ── */
.surprise-fade-enter-active,
.surprise-fade-leave-active {
  transition: opacity 0.2s ease;
}
.surprise-fade-enter-from,
.surprise-fade-leave-to {
  opacity: 0;
}
</style>
