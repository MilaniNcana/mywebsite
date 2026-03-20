<template>
  <div id="app-root">
    <!-- Back to top button -->
    <Transition name="fade">
      <button v-if="showBackToTop" class="back-to-top" @click="scrollToTop" aria-label="Back to top">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
          <polyline points="18 15 12 9 6 15"/>
        </svg>
      </button>
    </Transition>

    <!-- Navigation -->
    <NavBar />

    <!-- Main content -->
    <main>
      <HeroSection />
      <AboutSection />
      <SkillsSection />
      <ProjectsSection />
      <ExperienceSection />
      <ContactSection />
    </main>

    <!-- Footer -->
    <FooterSection />

    <!-- Surprise Me floating button -->
    <SurpriseMe />

    <!-- Page loading indicator -->
    <div class="page-loader" :class="{ 'page-loader--done': pageReady }">
      <div class="loader-logo">
        <span class="logo-bracket">&lt;</span>MN<span class="logo-bracket">/&gt;</span>
      </div>
      <div class="loader-bar">
        <div class="loader-bar__fill"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from '@/components/NavBar.vue'
import HeroSection from '@/components/HeroSection.vue'
import AboutSection from '@/components/AboutSection.vue'
import SkillsSection from '@/components/SkillsSection.vue'
import ProjectsSection from '@/components/ProjectsSection.vue'
import ExperienceSection from '@/components/ExperienceSection.vue'
import ContactSection from '@/components/ContactSection.vue'
import FooterSection from '@/components/FooterSection.vue'
import SurpriseMe from '@/components/SurpriseMe.vue'

const showBackToTop = ref(false)
const pageReady = ref(false)

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function handleScroll() {
  showBackToTop.value = window.scrollY > 400
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  // Show page after fonts/assets load
  setTimeout(() => { pageReady.value = true }, 800)
})

onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style>
/* ---- App shell ---- */
#app-root {
  min-height: 100vh;
  background: var(--bg-primary);
}

/* ---- Back to top ---- */
.back-to-top {
  position: fixed;
  bottom: 32px;
  right: 32px;
  z-index: 50;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--mustard);
  color: #0B0B0B;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 20px rgba(212, 160, 23, 0.4);
  transition: all 0.2s ease;
}

.back-to-top:hover {
  background: var(--mustard-light);
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(212, 160, 23, 0.5);
}

/* ---- Page Loader ---- */
.page-loader {
  position: fixed;
  inset: 0;
  background: var(--bg-base);
  z-index: 9999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 24px;
  transition: opacity 0.5s ease, visibility 0.5s ease;
}

.page-loader--done {
  opacity: 0;
  visibility: hidden;
  pointer-events: none;
}

.loader-logo {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 2rem;
  font-weight: 900;
  color: var(--text-primary);
  letter-spacing: -0.02em;
}

.loader-logo .logo-bracket {
  color: var(--mustard);
}

.loader-bar {
  width: 160px;
  height: 3px;
  background: var(--bg-surface-3);
  border-radius: 2px;
  overflow: hidden;
}

.loader-bar__fill {
  height: 100%;
  background: linear-gradient(90deg, var(--mustard), var(--burgundy));
  border-radius: 2px;
  animation: loader-fill 0.7s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

@keyframes loader-fill {
  from { width: 0; }
  to { width: 100%; }
}

/* ---- Fade transition ---- */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

/* ---- Global section alternate bg ---- */
#about { background: var(--bg-primary); }
#skills { background: var(--bg-surface); }
#projects { background: var(--bg-primary); }
#experience { background: var(--bg-surface); }
#contact { background: var(--bg-primary); }
</style>
