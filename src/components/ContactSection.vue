<template>
  <section id="contact" class="section contact">
    <div class="glow-orb glow-mustard" style="width:600px;height:600px;top:50%;left:50%;transform:translate(-50%,-50%);opacity:0.25"></div>

    <div class="container contact__inner">
      <!-- Header -->
      <div class="contact__header">
        <div class="section-tag reveal">Get In Touch</div>
        <h2 class="section-title reveal reveal-delay-1">
          Let's Build Something <span>Amazing</span>
        </h2>
        <p class="section-subtitle reveal reveal-delay-2">
          Whether you have a project in mind, a job opportunity, or just want to say hello —
          my inbox is always open. I'll get back to you within 24 hours.
        </p>
      </div>

      <div class="contact__content">
        <!-- Info cards -->
        <div class="contact__info reveal reveal-delay-2">
          <div v-for="info in contactInfo" :key="info.label" class="contact-info-card">
            <div class="contact-info-card__icon material-symbols-outlined">{{ info.icon }}</div>
            <div>
              <div class="contact-info-card__label">{{ info.label }}</div>
              <a :href="info.href" class="contact-info-card__value" target="_blank" rel="noopener noreferrer">
                {{ info.value }}
              </a>
            </div>
          </div>

          <!-- Social links -->
          <div class="contact__socials">
            <div class="contact__socials-label">Find me online</div>
            <div class="contact__social-links">
              <a v-for="social in socials" :key="social.name" :href="social.href" target="_blank" rel="noopener noreferrer" class="contact-social-btn" :title="social.name">
                <span v-html="social.svg"></span>
                {{ social.name }}
              </a>
            </div>
          </div>

          <!-- Availability badge -->
          <div class="availability-badge">
            <div class="availability-dot"></div>
            <span>Available for freelance &amp; full-time opportunities</span>
          </div>
        </div>

        <!-- Form -->
        <div class="contact__form-wrapper reveal reveal-delay-3">
          <form class="contact-form" @submit.prevent="handleSubmit" novalidate>
            <div class="form-grid">
              <div class="form-group">
                <label class="form-label" for="name">Your Name *</label>
                <input
                  id="name"
                  v-model="form.name"
                  type="text"
                  class="form-input"
                  :class="{ 'form-input--error': errors.name }"
                  placeholder="Alex Smith"
                  autocomplete="name"
                />
                <span v-if="errors.name" class="form-error">{{ errors.name }}</span>
              </div>

              <div class="form-group">
                <label class="form-label" for="email">Email Address *</label>
                <input
                  id="email"
                  v-model="form.email"
                  type="email"
                  class="form-input"
                  :class="{ 'form-input--error': errors.email }"
                  placeholder="alex@example.com"
                  autocomplete="email"
                />
                <span v-if="errors.email" class="form-error">{{ errors.email }}</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label" for="subject">Subject</label>
              <input
                id="subject"
                v-model="form.subject"
                type="text"
                class="form-input"
                placeholder="Project Inquiry / Job Opportunity / Hello"
              />
            </div>

            <div class="form-group">
              <label class="form-label" for="message">Message *</label>
              <textarea
                id="message"
                v-model="form.message"
                class="form-input form-textarea"
                :class="{ 'form-input--error': errors.message }"
                placeholder="Tell me about your project, idea, or what you'd like to discuss..."
                rows="5"
              ></textarea>
              <span v-if="errors.message" class="form-error">{{ errors.message }}</span>
              <span class="form-char-count">{{ form.message.length }} / 1000</span>
            </div>

            <!-- Submit -->
            <button type="submit" class="btn btn-primary form-submit" :disabled="submitting" :class="{ 'btn-success': submitted }">
              <span v-if="submitting" class="btn-spinner"></span>
              <svg v-else-if="submitted" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg>
              <svg v-else width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
              {{ submitted ? 'Message Sent!' : submitting ? 'Sending...' : 'Send Message' }}
            </button>
            <p v-if="submitError" class="form-submit-error">{{ submitError }}</p>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue'
import emailjs from '@emailjs/browser'

// ─── EmailJS config ────────────────────────────────────────────────────────
// Sign up free at https://www.emailjs.com then:
//  1. Add an Email Service (Gmail / Outlook)
//  2. Create an Email Template — template variables used below:
//       {{from_name}}, {{from_email}}, {{subject}}, {{message}}
//  3. Copy your Public Key from Account → API Keys
//  4. Replace the three placeholders below
const EJS_SERVICE  = 'service_of9tnkc'
const EJS_TEMPLATE = 'template_6jbn0ah'
const EJS_KEY      = '7X0VMRUfkg6dkLe2A'
// ───────────────────────────────────────────────────────────────────────────

const form = reactive({ name: '', email: '', subject: '', message: '' })
const errors = reactive({ name: '', email: '', message: '' })
const submitting = ref(false)
const submitted = ref(false)
const submitError = ref('')

const contactInfo = [
  { icon: 'email', label: 'Email', value: 'milanincana@outlook.com', href: 'mailto:milanincana@outlook.com' },
  { icon: 'location_on', label: 'Location', value: 'Cape Town, Western Cape', href: '#' },
  { icon: 'schedule', label: 'Response Time', value: 'Within 24 hours', href: '#' },
]

const socials = [
  {
    name: 'GitHub',
    href: 'https://github.com/MilaniNcana',
    svg: '<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>',
  },
  {
    name: 'LinkedIn',
    href: 'https://linkedin.com/in/milanincana',
    svg: '<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>',
  },
]

function validate() {
  let valid = true
  errors.name = ''
  errors.email = ''
  errors.message = ''

  if (!form.name.trim()) { errors.name = 'Name is required.'; valid = false }
  if (!form.email.trim()) {
    errors.email = 'Email is required.'; valid = false
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = 'Please enter a valid email.'; valid = false
  }
  if (!form.message.trim()) { errors.message = 'Message is required.'; valid = false }
  else if (form.message.length > 1000) { errors.message = 'Message must be under 1000 characters.'; valid = false }
  return valid
}

async function handleSubmit() {
  if (!validate()) return
  submitting.value = true
  submitError.value = ''
  try {
    await emailjs.send(
      EJS_SERVICE,
      EJS_TEMPLATE,
      {
        from_name:  form.name,
        from_email: form.email,
        subject:    form.subject || 'Portfolio Contact',
        message:    form.message,
      },
      EJS_KEY
    )
    submitted.value = true
    form.name = ''
    form.email = ''
    form.subject = ''
    form.message = ''
    setTimeout(() => { submitted.value = false }, 4000)
  } catch {
    submitError.value = 'Failed to send. Please try again or email milanincana@outlook.com directly.'
  } finally {
    submitting.value = false
  }
}

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') }),
    { threshold: 0.1, rootMargin: '0px 0px -40px 0px' }
  )
  document.querySelectorAll('#contact .reveal').forEach(el => observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.contact {
  background: var(--bg-primary);
  overflow: hidden;
}

.contact__inner {
  position: relative;
  z-index: 1;
}

.contact__header {
  text-align: center;
  margin-bottom: 64px;
}

.contact__header .section-subtitle {
  margin: 0 auto;
}

.contact__content {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 48px;
  align-items: start;
}

/* Info cards */
.contact__info {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.contact-info-card {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 20px;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  transition: all 0.2s ease;
}

.contact-info-card:hover {
  border-color: var(--border-hover);
}

.contact-info-card__icon {
  font-size: 1.5rem;
  flex-shrink: 0;
  color: var(--mustard);
  line-height: 1;
}

.contact-info-card__label {
  font-size: 0.75rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 3px;
}

.contact-info-card__value {
  font-size: 0.95rem;
  font-weight: 500;
  color: var(--text-primary);
  text-decoration: none;
  transition: color 0.2s;
}

.contact-info-card__value:hover {
  color: var(--mustard);
}

/* Socials */
.contact__socials {
  padding: 20px;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
}

.contact__socials-label {
  font-size: 0.78rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 14px;
}

.contact__social-links {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.contact-social-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background: var(--bg-surface-2);
  border: 1px solid var(--border);
  border-radius: var(--radius-full);
  font-size: 0.82rem;
  font-weight: 500;
  color: var(--text-secondary);
  text-decoration: none;
  transition: all 0.2s ease;
}

.contact-social-btn:hover {
  border-color: var(--mustard);
  color: var(--mustard);
  background: var(--mustard-subtle);
}

/* Availability */
.availability-badge {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 14px 20px;
  background: rgba(212, 160, 23, 0.06);
  border: 1px solid rgba(212, 160, 23, 0.2);
  border-radius: var(--radius-md);
}

.availability-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #4CAF50;
  flex-shrink: 0;
  animation: pulse-dot 2s ease-in-out infinite;
  box-shadow: 0 0 0 0 rgba(76, 175, 80, 0.4);
}

@keyframes pulse-dot {
  0%, 100% { box-shadow: 0 0 0 0 rgba(76, 175, 80, 0.4); }
  50% { box-shadow: 0 0 0 8px rgba(76, 175, 80, 0); }
}

.availability-badge span {
  font-size: 0.85rem;
  color: var(--text-secondary);
  font-weight: 500;
}

/* Form */
.contact__form-wrapper {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 36px;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
  position: relative;
}

.form-label {
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--text-secondary);
  letter-spacing: 0.03em;
}

.form-input {
  background: var(--bg-surface-2);
  border: 1.5px solid var(--border);
  border-radius: var(--radius-md);
  padding: 12px 16px;
  font-size: 0.92rem;
  color: var(--text-primary);
  outline: none;
  transition: all 0.2s ease;
  width: 100%;
}

.form-input::placeholder {
  color: var(--text-muted);
}

.form-input:focus {
  border-color: var(--mustard);
  background: var(--bg-surface-3);
  box-shadow: 0 0 0 3px rgba(212, 160, 23, 0.1);
}

.form-input--error {
  border-color: var(--burgundy-light);
}

.form-input--error:focus {
  box-shadow: 0 0 0 3px rgba(125, 17, 40, 0.15);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
  line-height: 1.6;
}

.form-error {
  font-size: 0.75rem;
  color: #E05070;
  display: flex;
  align-items: center;
  gap: 4px;
}

.form-char-count {
  font-size: 0.72rem;
  color: var(--text-muted);
  text-align: right;
  font-family: var(--font-mono);
}

.form-submit {
  width: 100%;
  justify-content: center;
  padding: 14px;
  font-size: 0.95rem;
  position: relative;
}

.form-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.btn-success {
  background: #2d7a4f !important;
  box-shadow: 0 4px 20px rgba(45, 122, 79, 0.35) !important;
}

.btn-spinner {
  width: 16px;
  height: 16px;
  border: 2px solid rgba(0,0,0,0.2);
  border-top-color: #0B0B0B;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.form-submit-error {
  text-align: center;
  font-size: 0.82rem;
  color: #E05070;
  margin-top: -8px;
}

@media (max-width: 900px) {
  .contact__content {
    grid-template-columns: 1fr;
  }
  .contact__info {
    order: 2;
  }
  .contact__form-wrapper {
    order: 1;
  }
}

@media (max-width: 600px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
  .contact__form-wrapper {
    padding: 24px;
  }
}
</style>
