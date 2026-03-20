<template>
  <nav class="navbar" :class="{ 'navbar--scrolled': scrolled, 'navbar--open': menuOpen }">
    <div class="container navbar__inner">
      <!-- Logo -->
      <a href="#home" class="navbar__logo" @click="closeMenu">
        <span class="logo-bracket">&lt;</span>
        <span class="logo-name">MN</span>
        <span class="logo-bracket">/&gt;</span>
      </a>

      <!-- Desktop Links -->
      <ul class="navbar__links">
        <li v-for="link in navLinks" :key="link.href">
          <a
            :href="link.href"
            class="navbar__link"
            :class="{ 'navbar__link--active': activeSection === link.section }"
            @click="closeMenu"
          >
            {{ link.label }}
          </a>
        </li>
      </ul>

      <!-- CTA -->
      <a href="#contact" class="btn btn-primary navbar__cta" @click="closeMenu">
        Hire Me
      </a>

      <!-- Hamburger -->
      <button class="navbar__burger" @click="toggleMenu" :aria-expanded="menuOpen" aria-label="Toggle menu">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>
  </nav>

  <!-- Mobile Menu — teleported to body so it doesn't inherit nav's stacking context -->
  <Teleport to="body">
    <div class="mobile-menu" :class="{ 'mobile-menu--open': menuOpen }">
      <!-- Close button -->
      <button class="mobile-menu__close" @click="closeMenu" aria-label="Close menu">
        <span></span>
        <span></span>
      </button>
      <ul class="mobile-menu__links">
        <li v-for="link in navLinks" :key="link.href">
          <a :href="link.href" class="mobile-menu__link" @click="closeMenu">{{ link.label }}</a>
        </li>
        <li>
          <a href="#contact" class="btn btn-primary mobile-cta" @click="closeMenu">Hire Me</a>
        </li>
      </ul>
    </div>
  </Teleport>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)
const activeSection = ref('home')

const navLinks = [
  { href: '#home', label: 'Home', section: 'home' },
  { href: '#about', label: 'About', section: 'about' },
  { href: '#skills', label: 'Skills', section: 'skills' },
  { href: '#projects', label: 'Projects', section: 'projects' },
  { href: '#experience', label: 'Experience', section: 'experience' },
  { href: '#contact', label: 'Contact', section: 'contact' },
]

function toggleMenu() {
  menuOpen.value = !menuOpen.value
  document.body.style.overflow = menuOpen.value ? 'hidden' : ''
}

function closeMenu() {
  menuOpen.value = false
  document.body.style.overflow = ''
}

function handleScroll() {
  scrolled.value = window.scrollY > 50

  // Active section detection
  const sections = navLinks.map(l => l.section)
  for (const id of [...sections].reverse()) {
    const el = document.getElementById(id)
    if (el && window.scrollY >= el.offsetTop - 120) {
      activeSection.value = id
      break
    }
  }
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 20px 0;
  transition: all 0.3s ease;
}

.navbar--scrolled {
  padding: 14px 0;
  background: rgba(8, 8, 8, 0.9);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border);
  box-shadow: 0 4px 30px rgba(0,0,0,0.4);
}

.navbar__inner {
  display: flex;
  align-items: center;
  gap: 40px;
}

/* Logo */
.navbar__logo {
  font-family: var(--font-mono);
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text-primary);
  text-decoration: none;
  flex-shrink: 0;
  transition: color 0.2s ease;
}

.logo-bracket {
  color: var(--mustard);
}

.logo-name {
  color: var(--text-primary);
  margin: 0 2px;
}

.navbar__logo:hover .logo-name {
  color: var(--mustard);
}

/* Links */
.navbar__links {
  display: flex;
  align-items: center;
  gap: 4px;
  margin: 0 auto;
}

.navbar__link {
  padding: 8px 16px;
  border-radius: var(--radius-full);
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-secondary);
  text-decoration: none;
  transition: all 0.2s ease;
  position: relative;
}

.navbar__link:hover {
  color: var(--text-primary);
  background: var(--mustard-subtle);
}

.navbar__link--active {
  color: var(--mustard);
  background: var(--mustard-subtle);
}

/* CTA */
.navbar__cta {
  flex-shrink: 0;
  padding: 10px 24px;
  font-size: 0.875rem;
}

/* Burger */
.navbar__burger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  padding: 4px;
  background: none;
  border: none;
  margin-left: auto;
  position: relative;
  z-index: 1;
}

.navbar__burger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--text-primary);
  border-radius: 2px;
  transition: all 0.3s ease;
  transform-origin: center;
}

/* Burger → X when open */
.navbar--open .navbar__burger span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}

.navbar--open .navbar__burger span:nth-child(2) {
  opacity: 0;
  transform: scaleX(0);
}

.navbar--open .navbar__burger span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

@media (max-width: 900px) {
  .navbar__links, .navbar__cta {
    display: none;
  }
  .navbar__burger {
    display: flex;
  }
}
</style>

<!-- Mobile menu styles (not scoped so they apply after Teleport) -->
<style>
.mobile-menu {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(8, 8, 8, 0.98);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  z-index: 999;
  padding-top: 100px;
  transform: translateY(-100%);
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.mobile-menu--open {
  transform: translateY(0);
}

.mobile-menu__close {
  display: none;
}

.mobile-menu__links {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  padding: 20px;
}

.mobile-menu__link {
  font-size: 1.5rem;
  font-weight: 700;
  font-family: 'Space Grotesk', sans-serif;
  color: rgba(255,255,255,0.6);
  text-decoration: none;
  padding: 12px 32px;
  border-radius: 12px;
  transition: all 0.2s ease;
  width: 100%;
  text-align: center;
}

.mobile-menu__link:hover {
  color: #D4A017;
  background: rgba(212, 160, 23, 0.08);
}

.mobile-cta {
  margin-top: 12px;
  width: 100%;
  display: flex;
  justify-content: center;
}

@media (max-width: 900px) {
  .mobile-menu {
    display: block;
  }
}
</style>
