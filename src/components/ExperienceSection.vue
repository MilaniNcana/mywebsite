<template>
  <section id="experience" class="section experience">
    <div class="glow-orb glow-burgundy" style="width:600px;height:600px;top:0;right:-200px;opacity:0.3"></div>

    <div class="container experience__inner">
      <!-- Header -->
      <div class="experience__header">
        <div class="section-tag reveal">My Journey</div>
        <h2 class="section-title reveal reveal-delay-1">
          Experience &amp; <span>Education</span>
        </h2>
        <p class="section-subtitle reveal reveal-delay-2">
          A timeline of growth, learning, and professional milestones that
          shaped who I am as a developer today.
        </p>
      </div>

      <!-- Tab switcher -->
      <div class="exp-tabs reveal reveal-delay-2">
        <button
          v-for="tab in ['Work Experience', 'Education']"
          :key="tab"
          class="exp-tab-btn"
          :class="{ 'exp-tab-btn--active': activeTab === tab }"
          @click="activeTab = tab"
        >
          {{ tab }}
        </button>
      </div>

      <!-- Timeline -->
      <div class="timeline">
        <TransitionGroup name="slide-up">
          <div
            v-for="(item, i) in activeItems"
            :key="item.title + i"
            class="timeline__item reveal"
            :class="`reveal-delay-${Math.min(i + 1, 5)}`"
          >
            <!-- Connector -->
            <div class="timeline__connector">
              <div class="timeline__dot" :style="`border-color: ${item.color}`">
                <span>{{ item.icon }}</span>
              </div>
              <div class="timeline__line" v-if="i < activeItems.length - 1"></div>
            </div>

            <!-- Card -->
            <div class="timeline__card">
              <div class="timeline__card-top">
                <div class="timeline__card-header">
                  <div class="timeline__company-logo" :style="`background: ${item.logoBg}`">
                    {{ item.abbr }}
                  </div>
                  <div>
                    <div class="timeline__title">{{ item.title }}</div>
                    <div class="timeline__company">{{ item.organization }}</div>
                  </div>
                </div>
                <div class="timeline__meta">
                  <span class="timeline__date">
                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
                    {{ item.period }}
                  </span>
                  <span class="timeline__location">
                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/></svg>
                    {{ item.location }}
                  </span>
                  <span v-if="item.current" class="timeline__current">Current</span>
                </div>
              </div>

              <p class="timeline__desc">{{ item.description }}</p>

              <div v-if="item.skills" class="timeline__skills">
                <span v-for="skill in item.skills" :key="skill" class="timeline__skill-tag">{{ skill }}</span>
              </div>

              <ul v-if="item.highlights" class="timeline__highlights">
                <li v-for="h in item.highlights" :key="h">
                  <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg>
                  {{ h }}
                </li>
              </ul>
            </div>
          </div>
        </TransitionGroup>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const activeTab = ref('Work Experience')

const workItems = [
  {
    icon: '💼',
    title: 'Software Developer',
    organization: 'Tech Company',
    abbr: 'TC',
    logoBg: 'linear-gradient(135deg, #D4A017, #B8880F)',
    period: '2023 — Present',
    location: 'South Africa',
    current: true,
    color: '#D4A017',
    description: 'Building and maintaining scalable web applications using Vue.js on the frontend and Spring Boot microservices on the backend. Collaborating with cross-functional teams to deliver high-quality software.',
    skills: ['Vue.js', 'Spring Boot', 'Java', 'MySQL', 'REST APIs'],
    highlights: [
      'Developed a multi-tenant SaaS application serving 1000+ users',
      'Reduced API response times by 40% through query optimization',
      'Led frontend migration from vanilla JS to Vue.js',
      'Implemented CI/CD pipelines using GitHub Actions',
    ],
  },
  {
    icon: '🚀',
    title: 'Junior Frontend Developer',
    organization: 'Digital Agency',
    abbr: 'DA',
    logoBg: 'linear-gradient(135deg, #7D1128, #5E0D1E)',
    period: '2022 — 2023',
    location: 'Remote',
    current: false,
    color: '#7D1128',
    description: 'Worked on diverse client projects building responsive web interfaces using HTML, CSS, JavaScript, and Vue.js. Gained experience in agile methodologies and client communication.',
    skills: ['HTML5', 'CSS3', 'JavaScript', 'Vue.js', 'Figma'],
    highlights: [
      'Delivered 8+ client projects on time and within budget',
      'Built reusable component library reducing development time by 30%',
      'Improved website performance scores to 90+ on Lighthouse',
    ],
  },
  {
    icon: '🛠️',
    title: 'Freelance Developer',
    organization: 'Self-Employed',
    abbr: 'FL',
    logoBg: 'linear-gradient(135deg, #333, #222)',
    period: '2021 — 2022',
    location: 'South Africa',
    current: false,
    color: '#666',
    description: 'Independently developed websites and web applications for small businesses and startups. Managed full project lifecycle from requirements gathering to deployment.',
    skills: ['HTML', 'CSS', 'JavaScript', 'PHP', 'WordPress'],
    highlights: [
      'Successfully completed 10+ freelance projects',
      'Built e-commerce solutions for local businesses',
      'Maintained 5-star client satisfaction rating',
    ],
  },
]

const educationItems = [
  {
    icon: '🎓',
    title: 'Bachelor of Science in Computer Science',
    organization: 'University of Technology',
    abbr: 'UT',
    logoBg: 'linear-gradient(135deg, #D4A017, #7D1128)',
    period: '2019 — 2023',
    location: 'South Africa',
    current: false,
    color: '#D4A017',
    description: 'Comprehensive study of computer science fundamentals, software engineering principles, data structures, algorithms, and modern software development practices.',
    skills: ['Java', 'Python', 'Data Structures', 'Algorithms', 'Software Engineering'],
    highlights: [
      'Graduated with distinction — GPA 3.8/4.0',
      'Final year project: Full-stack web application using Spring Boot & Vue.js',
      'Member of the Computer Science Society',
      'Dean\'s List for academic excellence',
    ],
  },
  {
    icon: '📜',
    title: 'Full Stack Web Development Bootcamp',
    organization: 'Online Certification',
    abbr: 'OC',
    logoBg: 'linear-gradient(135deg, #7D1128, #5E0D1E)',
    period: '2021',
    location: 'Online',
    current: false,
    color: '#9B1635',
    description: 'Intensive bootcamp covering modern full-stack development including JavaScript frameworks, REST APIs, databases, and deployment strategies.',
    skills: ['Node.js', 'React', 'MongoDB', 'Express.js', 'Git'],
    highlights: [
      'Completed 300+ hours of hands-on coding',
      'Built 5 full-stack projects as part of curriculum',
      'Earned certification with distinction',
    ],
  },
  {
    icon: '🏅',
    title: 'AWS Cloud Practitioner',
    organization: 'Amazon Web Services',
    abbr: 'AWS',
    logoBg: 'linear-gradient(135deg, #FF9900, #CC7700)',
    period: '2022',
    location: 'Online',
    current: false,
    color: '#FF9900',
    description: 'Cloud fundamentals certification covering AWS services, security, and architectural best practices.',
    skills: ['AWS', 'Cloud Architecture', 'S3', 'EC2', 'Lambda'],
    highlights: [
      'Passed certification on first attempt',
      'Scored in the top 15% of candidates',
    ],
  },
]

const activeItems = computed(() =>
  activeTab.value === 'Work Experience' ? workItems : educationItems
)

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') }),
    { threshold: 0.1, rootMargin: '0px 0px -40px 0px' }
  )
  document.querySelectorAll('#experience .reveal').forEach(el => observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.experience {
  background: var(--bg-surface);
  overflow: hidden;
}

.experience__inner {
  position: relative;
  z-index: 1;
}

.experience__header {
  text-align: center;
  margin-bottom: 40px;
}

.experience__header .section-subtitle {
  margin: 0 auto;
}

/* Tabs */
.exp-tabs {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-bottom: 48px;
}

.exp-tab-btn {
  padding: 10px 28px;
  border-radius: var(--radius-full);
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-secondary);
  background: var(--bg-surface-2);
  border: 1px solid var(--border);
  cursor: pointer;
  transition: all 0.2s ease;
}

.exp-tab-btn--active {
  background: var(--mustard);
  color: #0B0B0B;
  border-color: var(--mustard);
  font-weight: 600;
  box-shadow: 0 4px 16px rgba(212, 160, 23, 0.3);
}

/* Timeline */
.timeline {
  display: flex;
  flex-direction: column;
  gap: 0;
  max-width: 800px;
  margin: 0 auto;
}

.timeline__item {
  display: grid;
  grid-template-columns: 60px 1fr;
  gap: 24px;
}

.timeline__connector {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
}

.timeline__dot {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--bg-surface-2);
  border: 2px solid;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.1rem;
  flex-shrink: 0;
  z-index: 1;
}

.timeline__line {
  flex: 1;
  width: 2px;
  background: linear-gradient(to bottom, rgba(212, 160, 23, 0.2), transparent);
  margin: 4px 0;
  min-height: 40px;
}

/* Card */
.timeline__card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 24px;
  margin-bottom: 24px;
  transition: all 0.2s ease;
}

.timeline__card:hover {
  border-color: var(--border-hover);
  transform: translateX(4px);
}

.timeline__card-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 16px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.timeline__card-header {
  display: flex;
  align-items: center;
  gap: 14px;
}

.timeline__company-logo {
  width: 44px;
  height: 44px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  font-weight: 800;
  color: #fff;
  letter-spacing: 0.02em;
  flex-shrink: 0;
  font-family: var(--font-display);
}

.timeline__title {
  font-weight: 700;
  font-size: 1.05rem;
  color: var(--text-primary);
  margin-bottom: 2px;
}

.timeline__company {
  font-size: 0.85rem;
  color: var(--mustard);
  font-weight: 500;
}

.timeline__meta {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  align-items: center;
}

.timeline__date, .timeline__location {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 0.78rem;
  color: var(--text-muted);
  font-family: var(--font-mono);
}

.timeline__current {
  font-size: 0.72rem;
  font-weight: 700;
  padding: 3px 10px;
  border-radius: var(--radius-full);
  background: rgba(212, 160, 23, 0.12);
  color: var(--mustard);
  border: 1px solid rgba(212, 160, 23, 0.25);
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

.timeline__desc {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.75;
  margin-bottom: 16px;
}

.timeline__skills {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 16px;
}

.timeline__skill-tag {
  font-size: 0.72rem;
  font-family: var(--font-mono);
  padding: 4px 10px;
  background: var(--bg-surface-2);
  border: 1px solid var(--border);
  border-radius: var(--radius-full);
  color: var(--text-muted);
}

.timeline__highlights {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.timeline__highlights li {
  display: flex;
  align-items: flex-start;
  gap: 8px;
  font-size: 0.85rem;
  color: var(--text-secondary);
  line-height: 1.5;
}

.timeline__highlights li svg {
  color: var(--mustard);
  flex-shrink: 0;
  margin-top: 2px;
}

/* Slide up transition */
.slide-up-enter-active {
  transition: all 0.35s ease;
}
.slide-up-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

@media (max-width: 600px) {
  .timeline__item {
    grid-template-columns: 40px 1fr;
    gap: 12px;
  }
  .timeline__dot {
    width: 36px;
    height: 36px;
    font-size: 0.9rem;
  }
  .timeline__card-top {
    flex-direction: column;
  }
}
</style>
