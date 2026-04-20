<template>
  <section id="projects" class="section projects">
    <div class="glow-orb glow-mustard" style="width:500px;height:500px;bottom:-100px;left:-100px;opacity:0.35"></div>

    <div class="container">
      <div class="projects__header">
        <div class="section-tag reveal">Portfolio</div>
        <h2 class="section-title reveal reveal-delay-1">
          Featured <span>Projects</span>
        </h2>
        <p class="section-subtitle reveal reveal-delay-2">
          A selection of projects that showcase my ability to build full-featured,
          production-ready applications from concept to deployment.
        </p>
      </div>

      <!-- Filter -->
      <div class="projects__filter reveal reveal-delay-2">
        <button
          v-for="f in filters"
          :key="f"
          class="filter-btn"
          :class="{ 'filter-btn--active': activeFilter === f }"
          @click="activeFilter = f"
        >
          {{ f }}
        </button>
      </div>

      <!-- Grid -->
      <div class="projects__grid">
        <TransitionGroup name="project-fade">
          <div
            v-for="(project, i) in filteredProjects"
            :key="project.title"
            class="project-card reveal"
            :class="[`reveal-delay-${Math.min(i % 3 + 1, 5)}`, { 'project-card--featured': project.featured }]"
          >
            <!-- Card header / screenshot area -->
            <div class="project-card__preview" :style="`background: ${project.gradient}`">
              <div class="project-card__mockup">
                <div class="mockup-bar">
                  <span></span><span></span><span></span>
                </div>
                <div class="mockup-content">
                  <div class="mockup-line" style="width:80%"></div>
                  <div class="mockup-line" style="width:60%"></div>
                  <div class="mockup-line" style="width:70%"></div>
                  <div class="mockup-block"></div>
                </div>
              </div>
              <div v-if="project.featured" class="project-card__featured-badge">
                <span class="material-symbols-outlined" style="font-size:12px;vertical-align:middle;line-height:1">star</span> Featured
              </div>
            </div>

            <!-- Card body -->
            <div class="project-card__body">
              <div class="project-card__tags">
                <span v-for="tag in project.tags" :key="tag" class="project-tag">{{ tag }}</span>
              </div>
              <h3 class="project-card__title">{{ project.title }}</h3>
              <p class="project-card__desc">{{ project.description }}</p>

              <!-- Links -->
              <div class="project-card__links">
                <a :href="project.github" target="_blank" class="project-link project-link--github" rel="noopener noreferrer">
                  <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
                  GitHub
                </a>
              </div>
            </div>
          </div>
        </TransitionGroup>
      </div>

      <!-- See more CTA -->
      <div class="projects__cta reveal reveal-delay-3">
        <a href="https://github.com/MilaniNcana" target="_blank" rel="noopener noreferrer" class="btn btn-outline">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
          View All Projects on GitHub
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, watch, nextTick, onMounted, onUnmounted } from 'vue'

const activeFilter = ref('All')
const filters = ['All', 'Full Stack', 'Vue.js', 'Java', 'Frontend']

const projects = [
  {
    title: 'Trogster',
    description: 'A task management system for organizations to create tasks, manage workers, and collect structured field data. I designed and built the entire frontend from scratch, implemented CORS for future Android app development, and consume backend REST endpoints. I also collaborate with the backend developer to define the required API contracts.',
    tags: ['Vue 3', 'Vite', 'TypeScript', 'CORS'],
    category: ['Vue.js', 'Frontend'],
    gradient: 'linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%)',
    featured: true,
    github: 'https://github.com/MilaniNcana',
  },
  {
    title: 'RentMyStuff',
    description: 'A peer-to-peer rental platform built entirely solo — from frontend to backend. Frontend: Vue 3, Vite, JavaScript. Backend: Java, Spring Boot, Spring Microservices using MVC architecture. Database: PostgreSQL in production and MySQL for testing. Full REST API integration throughout.',
    tags: ['Vue 3', 'Java', 'Spring Boot', 'PostgreSQL', 'REST API'],
    category: ['Full Stack', 'Vue.js', 'Java'],
    gradient: 'linear-gradient(135deg, #1e0a2e 0%, #2e1065 50%, #1a0a40 100%)',
    featured: true,
    github: 'https://github.com/MilaniNcana',
  },
  {
    title: 'Car Rental System',
    description: 'An e-commerce website for renting cars. I was responsible for the login and dashboard modules full stack — using the same stack as RentMyStuff (Java, Spring Boot, PostgreSQL, REST API).',
    tags: ['Java', 'Spring Boot', 'PostgreSQL', 'REST API'],
    category: ['Full Stack', 'Java'],
    gradient: 'linear-gradient(135deg, #0a1a0e 0%, #0d2b1b 50%, #0a2010 100%)',
    featured: false,
    github: 'https://github.com/MilaniNcana',
  },
  {
    title: 'StyleForLess',
    description: 'A peer-to-peer platform for buying and selling high-end second-hand clothing. I built the Bootstrap-based frontend using Vue.js — making high-end style accessible to everyone.',
    tags: ['Bootstrap', 'Vue.js', 'CSS'],
    category: ['Frontend', 'Vue.js'],
    gradient: 'linear-gradient(135deg, #1a0e0e 0%, #2e1515 50%, #3a1a1a 100%)',
    featured: false,
    github: 'https://github.com/MilaniNcana',
  },
]

const filteredProjects = computed(() =>
  activeFilter.value === 'All'
    ? projects
    : projects.filter(p => p.category.includes(activeFilter.value))
)

let observer = null

watch(activeFilter, () => {
  nextTick(() => {
    document.querySelectorAll('#projects .project-card').forEach(el => el.classList.add('visible'))
  })
})

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') }),
    { threshold: 0.1, rootMargin: '0px 0px -40px 0px' }
  )
  document.querySelectorAll('#projects .reveal').forEach(el => observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.projects {
  background: var(--bg-primary);
  overflow: hidden;
}

.projects__header {
  text-align: center;
  margin-bottom: 40px;
}

.projects__header .section-subtitle {
  margin: 0 auto;
}

.projects__filter {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 48px;
}

.filter-btn {
  padding: 8px 20px;
  border-radius: var(--radius-full);
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--text-secondary);
  background: var(--bg-surface);
  border: 1px solid var(--border);
  cursor: pointer;
  transition: all 0.2s ease;
}

.filter-btn:hover {
  color: var(--text-primary);
  border-color: var(--mustard);
}

.filter-btn--active {
  background: var(--mustard);
  color: #0B0B0B;
  border-color: var(--mustard);
  font-weight: 600;
  box-shadow: 0 4px 16px rgba(212, 160, 23, 0.3);
}

/* Grid */
.projects__grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 24px;
  margin-bottom: 48px;
  position: relative;
  z-index: 1;
}

/* Card */
.project-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
}

.project-card:hover {
  border-color: var(--border-hover);
  transform: translateY(-6px);
  box-shadow: var(--shadow-lg), 0 0 30px rgba(212, 160, 23, 0.08);
}

.project-card--featured {
  border-color: rgba(212, 160, 23, 0.2);
}

/* Preview area */
.project-card__preview {
  height: 180px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.project-card__mockup {
  width: 80%;
  background: rgba(0,0,0,0.4);
  border-radius: 8px;
  overflow: hidden;
  border: 1px solid rgba(255,255,255,0.08);
}

.mockup-bar {
  background: rgba(255,255,255,0.05);
  padding: 8px 12px;
  display: flex;
  gap: 6px;
  align-items: center;
}

.mockup-bar span {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255,255,255,0.2);
}

.mockup-bar span:first-child { background: var(--burgundy); }
.mockup-bar span:nth-child(2) { background: var(--mustard-dark); }
.mockup-bar span:nth-child(3) { background: rgba(255,255,255,0.1); }

.mockup-content {
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.mockup-line {
  height: 6px;
  background: rgba(255,255,255,0.12);
  border-radius: 3px;
}

.mockup-block {
  height: 40px;
  background: rgba(212, 160, 23, 0.1);
  border: 1px solid rgba(212, 160, 23, 0.15);
  border-radius: 4px;
  margin-top: 4px;
}

.project-card__featured-badge {
  position: absolute;
  top: 12px;
  right: 12px;
  background: rgba(212, 160, 23, 0.15);
  border: 1px solid rgba(212, 160, 23, 0.3);
  color: var(--mustard);
  font-size: 0.72rem;
  font-weight: 600;
  padding: 4px 10px;
  border-radius: var(--radius-full);
  letter-spacing: 0.04em;
}

/* Body */
.project-card__body {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  flex: 1;
}

.project-card__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.project-tag {
  font-size: 0.72rem;
  font-family: var(--font-mono);
  padding: 4px 10px;
  background: var(--bg-surface-2);
  border: 1px solid var(--border);
  border-radius: var(--radius-full);
  color: var(--text-muted);
  letter-spacing: 0.03em;
}

.project-card__title {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-primary);
  line-height: 1.3;
}

.project-card__desc {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.7;
  flex: 1;
}

.project-card__links {
  display: flex;
  gap: 10px;
  margin-top: auto;
  padding-top: 8px;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 0.82rem;
  font-weight: 500;
  padding: 8px 16px;
  border-radius: var(--radius-full);
  transition: all 0.2s ease;
  text-decoration: none;
}

.project-link--demo {
  background: var(--mustard);
  color: #0B0B0B;
}

.project-link--demo:hover {
  background: var(--mustard-light);
  transform: translateY(-1px);
}

.project-link--github {
  background: var(--bg-surface-2);
  color: var(--text-secondary);
  border: 1px solid var(--border);
}

.project-link--github:hover {
  border-color: var(--mustard);
  color: var(--mustard);
}

/* Transition */
.project-fade-enter-active, .project-fade-leave-active {
  transition: all 0.3s ease;
}

.project-fade-enter-from, .project-fade-leave-to {
  opacity: 0;
  transform: scale(0.95);
}

.projects__cta {
  text-align: center;
}

@media (max-width: 768px) {
  .projects__grid {
    grid-template-columns: 1fr;
  }
}
</style>
