<template>
  <section id="skills" class="section skills">
    <div class="glow-orb glow-burgundy" style="width:500px;height:500px;top:0;right:-150px;opacity:0.4"></div>

    <div class="container">
      <div class="skills__header">
        <div class="section-tag reveal">Skills &amp; Technologies</div>
        <h2 class="section-title reveal reveal-delay-1">
          My <span>Tech Stack</span>
        </h2>
        <p class="section-subtitle reveal reveal-delay-2">
          A carefully curated toolkit built over years of hands-on development across
          frontend, backend, and everything in between.
        </p>
      </div>

      <!-- Filter tabs -->
      <div class="skills__tabs reveal reveal-delay-2">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          class="tab-btn"
          :class="{ 'tab-btn--active': activeTab === tab.id }"
          @click="activeTab = tab.id"
        >
          {{ tab.label }}
        </button>
      </div>

      <!-- Skills grid -->
      <div class="skills__grid">
        <div
          v-for="skill in filteredSkills"
          :key="skill.name"
          class="skill-card"
          :style="`--skill-level: ${skill.level}%`"
        >
          <div class="skill-card__top">
            <div class="skill-card__icon">
              <span class="material-symbols-outlined">{{ skill.icon }}</span>
            </div>
            <div class="skill-card__info">
              <span class="skill-card__name">{{ skill.name }}</span>
              <span class="skill-card__category">{{ skill.category }}</span>
            </div>
            <span class="skill-card__percent">{{ skill.level }}%</span>
          </div>
          <div class="skill-card__bar-track">
            <div
              class="skill-card__bar-fill"
              :style="`background: ${skill.color}; width: ${skill.level}%`"
            ></div>
          </div>
        </div>
      </div>

      <!-- Extra tools / soft skills -->
      <div class="skills__extras reveal reveal-delay-3">
        <div class="skills__extras-label">Also experienced with:</div>
        <div class="skills__extras-tags">
          <span v-for="tool in extraTools" :key="tool" class="extra-tag">{{ tool }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const activeTab = ref('all')

const tabs = [
  { id: 'all', label: 'All Skills' },
  { id: 'frontend', label: 'Frontend' },
  { id: 'backend', label: 'Backend' },
  { id: 'tools', label: 'Tools & Other' },
  { id: 'support', label: 'Technical Support' },
]

const skills = [
  { name: 'Vue.js', icon: 'hub', level: 90, category: 'frontend', color: 'linear-gradient(90deg, #41B883, #35495E)' },
  { name: 'JavaScript', icon: 'javascript', level: 88, category: 'frontend', color: 'linear-gradient(90deg, #F7DF1E, #D4A017)' },
  { name: 'TypeScript', icon: 'code', level: 78, category: 'frontend', color: 'linear-gradient(90deg, #3178C6, #235A97)' },
  { name: 'HTML5', icon: 'html', level: 92, category: 'frontend', color: 'linear-gradient(90deg, #E34F26, #D4A017)' },
  { name: 'CSS3', icon: 'css', level: 88, category: 'frontend', color: 'linear-gradient(90deg, #1572B6, #7D1128)' },
  { name: 'Bootstrap', icon: 'dashboard', level: 82, category: 'frontend', color: 'linear-gradient(90deg, #7952B3, #5A2D9A)' },
  { name: 'Java', icon: 'local_cafe', level: 85, category: 'backend', color: 'linear-gradient(90deg, #D4A017, #B8880F)' },
  { name: 'Spring Boot', icon: 'eco', level: 80, category: 'backend', color: 'linear-gradient(90deg, #6DB33F, #45A029)' },
  { name: 'REST APIs', icon: 'api', level: 85, category: 'backend', color: 'linear-gradient(90deg, #7D1128, #9B1635)' },
  { name: 'SQL', icon: 'storage', level: 78, category: 'backend', color: 'linear-gradient(90deg, #4479A1, #7D1128)' },
  { name: 'Git', icon: 'account_tree', level: 85, category: 'tools', color: 'linear-gradient(90deg, #F05032, #D4A017)' },
  { name: 'Figma', icon: 'palette', level: 65, category: 'tools', color: 'linear-gradient(90deg, #F24E1E, #A259FF)' },
  { name: 'Windows Support', icon: 'computer', level: 88, category: 'support', color: 'linear-gradient(90deg, #0078D4, #005a9e)' },
  { name: 'Hardware Repair', icon: 'build', level: 80, category: 'support', color: 'linear-gradient(90deg, #7D1128, #9B1635)' },
  { name: 'Networking', icon: 'router', level: 75, category: 'support', color: 'linear-gradient(90deg, #D4A017, #B8880F)' },
  { name: 'User Support', icon: 'support_agent', level: 90, category: 'support', color: 'linear-gradient(90deg, #41B883, #35495E)' },
  { name: 'ITSM', icon: 'settings_suggest', level: 78, category: 'support', color: 'linear-gradient(90deg, #6DB33F, #45A029)' },
]

const extraTools = [
  'GitHub', 'VS Code', 'Unit Testing', 'CORS', 'Agile Development',
  'System Analysis', 'Problem Solving',
]

const filteredSkills = computed(() =>
  activeTab.value === 'all' ? skills : skills.filter(s => s.category === activeTab.value)
)

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) e.target.classList.add('visible')
      })
    },
    { threshold: 0.1, rootMargin: '0px 0px -40px 0px' }
  )
  document.querySelectorAll('#skills .reveal').forEach(el => observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.skills {
  background: var(--bg-surface);
  overflow: hidden;
}

.skills__header {
  text-align: center;
  margin-bottom: 48px;
}

.skills__header .section-subtitle {
  margin: 0 auto;
}

.skills__tabs {
  display: flex;
  justify-content: center;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 48px;
}

.tab-btn {
  padding: 10px 24px;
  border-radius: var(--radius-full);
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--text-secondary);
  background: var(--bg-surface-2);
  border: 1px solid var(--border);
  cursor: pointer;
  transition: all 0.2s ease;
}

.tab-btn:hover {
  color: var(--text-primary);
  border-color: var(--mustard);
}

.tab-btn--active {
  background: var(--mustard);
  color: #0B0B0B;
  border-color: var(--mustard);
  font-weight: 600;
  box-shadow: 0 4px 16px rgba(212, 160, 23, 0.3);
}

/* Skills grid */
.skills__grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 16px;
  margin-bottom: 48px;
}

.skill-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 20px;
  transition: all 0.25s ease;
}

.skill-card:hover {
  border-color: var(--border-hover);
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
}

.skill-card__top {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 16px;
}

.skill-card__icon {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  background: var(--bg-surface-2);
  border-radius: 8px;
  color: var(--mustard);
}

.skill-card__icon .material-symbols-outlined {
  font-size: 1.2rem;
}

.skill-card__info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.skill-card__name {
  font-weight: 600;
  font-size: 0.95rem;
  color: var(--text-primary);
}

.skill-card__category {
  font-size: 0.72rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-muted);
}

.skill-card__percent {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--mustard);
}

.skill-card__bar-track {
  height: 5px;
  background: var(--bg-surface-3);
  border-radius: 3px;
  overflow: hidden;
}

.skill-card__bar-fill {
  height: 100%;
  border-radius: 3px;
  transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Extras */
.skills__extras {
  text-align: center;
  padding-top: 24px;
  border-top: 1px solid var(--border);
}

.skills__extras-label {
  font-size: 0.85rem;
  color: var(--text-muted);
  margin-bottom: 16px;
  font-family: var(--font-mono);
  letter-spacing: 0.05em;
}

.skills__extras-tags {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
}

.extra-tag {
  padding: 6px 14px;
  background: var(--bg-surface-2);
  border: 1px solid var(--border);
  border-radius: var(--radius-full);
  font-size: 0.8rem;
  color: var(--text-secondary);
  transition: all 0.2s ease;
}

.extra-tag:hover {
  border-color: var(--mustard);
  color: var(--mustard);
  background: var(--mustard-subtle);
}
</style>
