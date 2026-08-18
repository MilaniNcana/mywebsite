<template>
  <section id="projects" class="section projects">

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
            <!-- Card thumbnail -->
            <div class="project-card__thumb" :style="`background: ${project.gradient}`">
              <!-- Trogster sneak peek -->
              <div v-if="project.preview === 'trogster'" class="trogster-preview">
                <div class="tp-topbar">
                  <span class="tp-topbar__logo">T</span>
                  <span class="tp-topbar__title">Trogster</span>
                  <div class="tp-topbar__statuses">
                    <span class="tp-status-pill tp-status-pill--done">3 Done</span>
                    <span class="tp-status-pill tp-status-pill--active">2 Active</span>
                  </div>
                </div>
                <div class="tp-body">
                  <div class="tp-sidebar">
                    <div class="tp-sidebar__item tp-sidebar__item--active">
                      <svg width="10" height="10" viewBox="0 0 24 24" fill="currentColor"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>
                    </div>
                    <div class="tp-sidebar__item">
                      <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/><circle cx="9" cy="7" r="4"/></svg>
                    </div>
                    <div class="tp-sidebar__item">
                      <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="9 11 12 14 22 4"/><path d="M21 12v7a2 2 0 01-2 2H5a2 2 0 01-2-2V5a2 2 0 012-2h11"/></svg>
                    </div>
                    <div class="tp-sidebar__item">
                      <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.07 4.93a10 10 0 010 14.14"/><path d="M4.93 4.93a10 10 0 000 14.14"/></svg>
                    </div>
                  </div>
                  <div class="tp-tasks">
                    <div class="tp-task">
                      <span class="tp-dot tp-dot--done"></span>
                      <span class="tp-task__bar" style="width:58%"></span>
                      <span class="tp-badge tp-badge--done">Done</span>
                    </div>
                    <div class="tp-task">
                      <span class="tp-dot tp-dot--active"></span>
                      <span class="tp-task__bar" style="width:42%"></span>
                      <span class="tp-badge tp-badge--active">Active</span>
                    </div>
                    <div class="tp-task">
                      <span class="tp-dot tp-dot--active"></span>
                      <span class="tp-task__bar" style="width:67%"></span>
                      <span class="tp-badge tp-badge--active">Active</span>
                    </div>
                    <div class="tp-task">
                      <span class="tp-dot tp-dot--pending"></span>
                      <span class="tp-task__bar" style="width:35%"></span>
                      <span class="tp-badge tp-badge--pending">Pending</span>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Default letter thumbnail -->
              <span v-else class="project-thumb__letter">{{ project.title.charAt(0) }}</span>
              <div v-if="project.featured" class="project-card__featured-badge">Featured</div>
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
                <a v-if="project.demo" :href="project.demo" target="_blank" class="project-link project-link--demo" rel="noopener noreferrer">
                  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
                  {{ project.demoLabel || 'Live Demo' }}
                </a>
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
    preview: 'trogster',
    demoLabel: 'Visit Site',
    github: 'https://github.com/MilaniNcana',
    demo: 'https://trogster.com',
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

/* Thumbnail */
.project-card__thumb {
  height: 140px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.project-thumb__letter {
  font-size: 5.5rem;
  font-weight: 900;
  font-family: var(--font-display);
  color: rgba(255, 255, 255, 0.1);
  letter-spacing: -0.05em;
  user-select: none;
  line-height: 1;
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

/* Trogster sneak peek */
.trogster-preview {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  font-family: var(--font-mono);
  overflow: hidden;
}

.tp-topbar {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 6px 10px;
  background: rgba(0, 0, 0, 0.35);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  flex-shrink: 0;
}

.tp-topbar__logo {
  width: 16px;
  height: 16px;
  background: var(--mustard);
  color: #0B0B0B;
  font-size: 0.6rem;
  font-weight: 900;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 3px;
  flex-shrink: 0;
}

.tp-topbar__title {
  font-size: 0.6rem;
  color: rgba(255,255,255,0.7);
  font-weight: 600;
  flex: 1;
  letter-spacing: 0.04em;
}

.tp-topbar__statuses {
  display: flex;
  gap: 4px;
}

.tp-status-pill {
  font-size: 0.5rem;
  padding: 1px 5px;
  border-radius: 20px;
  font-weight: 600;
  letter-spacing: 0.02em;
}

.tp-status-pill--done { background: rgba(109, 179, 63, 0.2); color: #6DB33F; border: 1px solid rgba(109,179,63,0.3); }
.tp-status-pill--active { background: rgba(212, 160, 23, 0.2); color: var(--mustard); border: 1px solid rgba(212,160,23,0.3); }

.tp-body {
  display: flex;
  flex: 1;
  overflow: hidden;
}

.tp-sidebar {
  width: 28px;
  background: rgba(0, 0, 0, 0.25);
  border-right: 1px solid rgba(255,255,255,0.06);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 6px 0;
  gap: 6px;
  flex-shrink: 0;
}

.tp-sidebar__item {
  width: 20px;
  height: 20px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255,255,255,0.25);
  transition: all 0.2s;
}

.tp-sidebar__item--active {
  background: rgba(212, 160, 23, 0.15);
  color: var(--mustard);
}

.tp-tasks {
  flex: 1;
  padding: 6px 8px;
  display: flex;
  flex-direction: column;
  gap: 5px;
  overflow: hidden;
}

.tp-task {
  display: flex;
  align-items: center;
  gap: 5px;
  height: 16px;
}

.tp-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  flex-shrink: 0;
}

.tp-dot--done { background: #6DB33F; }
.tp-dot--active { background: var(--mustard); }
.tp-dot--pending { background: rgba(255,255,255,0.2); border: 1px solid rgba(255,255,255,0.15); }

.tp-task__bar {
  height: 4px;
  background: rgba(255,255,255,0.1);
  border-radius: 2px;
  flex: 1;
  max-width: 70%;
}

.tp-badge {
  font-size: 0.45rem;
  padding: 1px 4px;
  border-radius: 3px;
  font-weight: 700;
  letter-spacing: 0.03em;
  white-space: nowrap;
  margin-left: auto;
}

.tp-badge--done { background: rgba(109,179,63,0.2); color: #6DB33F; }
.tp-badge--active { background: rgba(212,160,23,0.2); color: var(--mustard); }
.tp-badge--pending { background: rgba(255,255,255,0.06); color: rgba(255,255,255,0.3); }

@media (max-width: 768px) {
  .projects__grid {
    grid-template-columns: 1fr;
  }
}
</style>
