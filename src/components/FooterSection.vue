<template>
  <footer class="footer">
    <div class="footer__top">
      <div class="container footer__top-inner">
        <!-- Brand -->
        <div class="footer__brand">
          <a href="#home" class="footer__logo">
            <span class="logo-bracket">&lt;</span>MN<span class="logo-bracket">/&gt;</span>
          </a>
          <p class="footer__tagline">
            Building digital experiences that matter.<br>
            One line of code at a time.
          </p>
          <div class="footer__social">
            <a href="https://github.com/MilaniNcana" target="_blank" rel="noopener noreferrer" class="footer-social-link" aria-label="GitHub">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
            </a>
            <a href="https://linkedin.com/in/milanincana" target="_blank" rel="noopener noreferrer" class="footer-social-link" aria-label="LinkedIn">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
            </a>
            <a href="mailto:milanincana@outlook.com" class="footer-social-link" aria-label="Email">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
            </a>
          </div>
        </div>

        <!-- Navigation -->
        <div class="footer__nav">
          <div class="footer__nav-group">
            <h4 class="footer__nav-title">Navigation</h4>
            <ul class="footer__nav-list">
              <li><a href="#home">Home</a></li>
              <li><a href="#about">About</a></li>
              <li><a href="#skills">Skills</a></li>
              <li><a href="#projects">Projects</a></li>
              <li><a href="#experience">Experience</a></li>
              <li><a href="#contact">Contact</a></li>
            </ul>
          </div>
          <div class="footer__nav-group">
            <h4 class="footer__nav-title">Technologies</h4>
            <ul class="footer__nav-list">
              <li><span>Vue.js</span></li>
              <li><span>React</span></li>
              <li><span>Java</span></li>
              <li><span>Spring Boot</span></li>
              <li><span>JavaScript</span></li>
              <li><span>REST APIs</span></li>
            </ul>
          </div>
          <div class="footer__nav-group">
            <h4 class="footer__nav-title">Let's Connect</h4>
            <ul class="footer__nav-list">
              <li><a href="https://github.com/MilaniNcana" target="_blank" rel="noopener noreferrer">GitHub →</a></li>
              <li><a href="https://linkedin.com/in/milanincana" target="_blank" rel="noopener noreferrer">LinkedIn →</a></li>
              <li><a href="mailto:milanincana@outlook.com">Email Me →</a></li>
              <li><a href="#contact">Hire Me →</a></li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <!-- Bottom bar -->
    <div class="footer__bottom">
      <div class="container footer__bottom-inner">
        <span class="footer__copy">
          © {{ new Date().getFullYear() }} Milani Ncana. All rights reserved.
        </span>
        <span class="footer__built">
          Built with
          <span class="footer__heart">♥</span>
          using
          <span class="footer__tech">Vue.js</span>
          ·
          <span class="footer__tech">Vite</span>
          ·
          <span class="footer__tech">Vercel</span>
        </span>
      </div>
    </div>
  </footer>
</template>

<script setup>
</script>

<style scoped>
.footer {
  background: var(--bg-base);
  border-top: 1px solid var(--border);
}

.footer__top {
  padding: 64px 0 40px;
}

.footer__top-inner {
  display: grid;
  grid-template-columns: 1.2fr 2fr;
  gap: 64px;
}

/* Brand */
.footer__brand {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.footer__logo {
  font-family: var(--font-mono);
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--text-primary);
  text-decoration: none;
  transition: color 0.2s;
}

.logo-bracket {
  color: var(--mustard);
}

.footer__logo:hover .logo-bracket {
  color: var(--mustard-light);
}

.footer__tagline {
  font-size: 0.9rem;
  color: var(--text-muted);
  line-height: 1.7;
  max-width: 260px;
}

.footer__social {
  display: flex;
  gap: 12px;
}

.footer-social-link {
  width: 38px;
  height: 38px;
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-muted);
  transition: all 0.2s ease;
  text-decoration: none;
}

.footer-social-link:hover {
  border-color: var(--mustard);
  color: var(--mustard);
  background: var(--mustard-subtle);
  transform: translateY(-2px);
}

/* Nav */
.footer__nav {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

.footer__nav-title {
  font-size: 0.78rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--text-muted);
  margin-bottom: 16px;
}

.footer__nav-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.footer__nav-list li a,
.footer__nav-list li span {
  font-size: 0.88rem;
  color: var(--text-secondary);
  text-decoration: none;
  transition: color 0.2s;
}

.footer__nav-list li a:hover {
  color: var(--mustard);
}

/* Bottom */
.footer__bottom {
  padding: 20px 0;
  border-top: 1px solid var(--border);
}

.footer__bottom-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
}

.footer__copy {
  font-size: 0.82rem;
  color: var(--text-muted);
}

.footer__built {
  font-size: 0.82rem;
  color: var(--text-muted);
  display: flex;
  align-items: center;
  gap: 4px;
  flex-wrap: wrap;
}

.footer__heart {
  color: var(--burgundy-light);
}

.footer__tech {
  color: var(--mustard);
  font-weight: 500;
}

/* Back to top (hidden, uses scroll) */

@media (max-width: 900px) {
  .footer__top-inner {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .footer__nav {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .footer__nav {
    grid-template-columns: 1fr 1fr;
  }
  .footer__bottom-inner {
    flex-direction: column;
    text-align: center;
  }
}
</style>
