<script setup lang="ts">
/* ------------------------------------------------------------------
   AppFooter — "Laboratory of Good Health"

   Four zones:
     1. Brand + newsletter + sitemap (Shop / Company / Support)
     2. Oversize italic-Fraunces brand moment ("Be in good health.")
     3. FDA / DSHEA disclaimer, wrapped in a bordered compliance card
     4. Baseline bar — copyright, social, legal

   Motion is intentionally restrained — CSS transitions on hover,
   one on-scroll fade could be added later. Keeps focus on type &
   composition.
------------------------------------------------------------------ */

const email = ref('')
const status = ref<'idle' | 'sending' | 'sent' | 'error'>('idle')

function submit(e: Event) {
  e.preventDefault()
  if (!email.value || status.value === 'sending') return
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email.value)) {
    status.value = 'error'
    return
  }
  status.value = 'sending'
  setTimeout(() => {
    status.value = 'sent'
    email.value = ''
    setTimeout(() => { status.value = 'idle' }, 5000)
  }, 500)
}

const currentYear = new Date().getFullYear()

const shopLinks = [
  { label: 'NuriCell', href: '#' },
  { label: 'Nature Calm', href: '#' },
  { label: 'Turmerific', href: '#' },
  { label: 'Advanced OPC', href: '#' },
  { label: 'Green Bee Propolis', href: '#' },
  { label: 'Deer Horn Reishi', href: '#' },
  { label: 'View all', href: '#' },
]
const companyLinks = [
  { label: 'About', href: '#' },
  { label: 'Our founder', href: '#' },
  { label: 'The science', href: '#' },
  { label: 'Press', href: '#' },
  { label: 'Careers', href: '#' },
]
const supportLinks = [
  { label: 'Help center', href: '#' },
  { label: 'Contact', href: '#' },
  { label: 'Shipping', href: '#' },
  { label: 'Returns', href: '#' },
  { label: 'Take the quiz', href: '#' },
]
</script>

<template>
  <footer class="relative overflow-hidden bg-midnight text-cream">
    <!-- Grain for warmth on the dark base -->
    <div
      aria-hidden="true"
      class="pointer-events-none absolute inset-0 opacity-[0.04] mix-blend-overlay bg-[url('data:image/svg+xml;utf8,<svg%20xmlns=%22http://www.w3.org/2000/svg%22%20width=%22240%22%20height=%22240%22><filter%20id=%22n%22><feTurbulence%20type=%22fractalNoise%22%20baseFrequency=%220.9%22%20numOctaves=%222%22%20stitchTiles=%22stitch%22/></filter><rect%20width=%22240%22%20height=%22240%22%20filter=%22url(%23n)%22/></svg>')]"
    />

    <!-- Mint glow ring at the top edge — hints the section is lit from above -->
    <div
      aria-hidden="true"
      class="pointer-events-none absolute left-1/2 top-0 h-[520px] w-[1100px] -translate-x-1/2 -translate-y-1/2 rounded-full bg-amber/[0.08] blur-3xl"
    />

    <div class="relative mx-auto max-w-[1200px] px-6 pt-20 pb-10 md:px-10">

      <!-- ZONE 1 — Brand + newsletter + sitemap -->
      <div class="grid grid-cols-1 gap-14 md:grid-cols-[1.3fr_1fr_1fr_1fr] md:gap-10">

        <!-- Brand + newsletter -->
        <div>
          <div class="inline-flex items-center gap-2 font-mono text-[11px] uppercase tracking-[0.22em] text-amber">
            <span class="inline-block h-1.5 w-1.5 rounded-full bg-amber" aria-hidden="true" />
            Be in Good Health
          </div>
          <div class="font-display mt-3 text-[56px] font-medium leading-none tracking-tight">
            BiGH
          </div>
          <p class="mt-5 max-w-[340px] text-[14px] leading-[1.55] text-cream/70">
            Be sharper. Weekly. Straight-talk brain-health science from Dr. Liu's team &mdash; no hype.
          </p>

          <form
            novalidate
            class="mt-7 max-w-[380px]"
            @submit="submit"
          >
            <label for="newsletter-email" class="sr-only">Email address</label>
            <div
              class="relative flex items-center rounded-full border border-cream/15 bg-ink-slate/40 backdrop-blur-sm transition-[border-color,background-color] duration-200 focus-within:border-amber/60 focus-within:bg-ink-slate/60"
            >
              <input
                id="newsletter-email"
                v-model="email"
                type="email"
                required
                :disabled="status === 'sending' || status === 'sent'"
                placeholder="you@example.com"
                autocomplete="email"
                :aria-invalid="status === 'error'"
                :aria-describedby="status === 'error' ? 'newsletter-error' : 'newsletter-help'"
                class="min-w-0 flex-1 bg-transparent py-3 pl-5 pr-2 text-[14px] text-cream outline-none placeholder:text-cream/40 disabled:opacity-60"
                @input="status === 'error' && (status = 'idle')"
              >
              <button
                type="submit"
                :disabled="!email || status === 'sending' || status === 'sent'"
                class="mr-1 inline-flex h-10 items-center justify-center rounded-full bg-amber px-5 font-mono text-[11px] font-semibold uppercase tracking-[0.14em] text-midnight transition-[background-color,transform] duration-200 hover:bg-amber-soft active:scale-[0.98] disabled:opacity-50"
              >
                {{ status === 'sending' ? 'Sending…' : status === 'sent' ? '✓ Sent' : 'Subscribe' }}
              </button>
            </div>
            <div aria-live="polite" class="mt-2 min-h-[18px] font-mono text-[11px] uppercase tracking-[0.14em]">
              <span v-if="status === 'error'" id="newsletter-error" role="alert" class="text-danger">
                ✕ Please enter a valid email.
              </span>
              <span v-else-if="status === 'sent'" role="status" class="text-amber">
                ✓ Subscribed &mdash; check your inbox.
              </span>
              <span v-else id="newsletter-help" class="text-cream/40">
                No spam. One email a week.
              </span>
            </div>
          </form>
        </div>

        <!-- Shop -->
        <nav aria-label="Shop">
          <div class="mb-5 flex items-baseline gap-2 font-mono text-[11px] uppercase tracking-[0.2em] text-amber">
            <span class="text-cream/35">01</span>
            Shop
          </div>
          <ul class="space-y-3">
            <li v-for="l in shopLinks" :key="l.label">
              <a
                :href="l.href"
                class="group inline-flex items-baseline gap-1.5 text-[14px] text-cream/80 transition-colors duration-150 hover:text-amber"
              >
                <span class="-ml-3 w-2 text-amber opacity-0 transition-opacity duration-150 group-hover:opacity-100" aria-hidden="true">→</span>
                {{ l.label }}
              </a>
            </li>
          </ul>
        </nav>

        <!-- Company -->
        <nav aria-label="Company">
          <div class="mb-5 flex items-baseline gap-2 font-mono text-[11px] uppercase tracking-[0.2em] text-amber">
            <span class="text-cream/35">02</span>
            Company
          </div>
          <ul class="space-y-3">
            <li v-for="l in companyLinks" :key="l.label">
              <a
                :href="l.href"
                class="group inline-flex items-baseline gap-1.5 text-[14px] text-cream/80 transition-colors duration-150 hover:text-amber"
              >
                <span class="-ml-3 w-2 text-amber opacity-0 transition-opacity duration-150 group-hover:opacity-100" aria-hidden="true">→</span>
                {{ l.label }}
              </a>
            </li>
          </ul>
        </nav>

        <!-- Support -->
        <nav aria-label="Support">
          <div class="mb-5 flex items-baseline gap-2 font-mono text-[11px] uppercase tracking-[0.2em] text-amber">
            <span class="text-cream/35">03</span>
            Support
          </div>
          <ul class="space-y-3">
            <li v-for="l in supportLinks" :key="l.label">
              <a
                :href="l.href"
                class="group inline-flex items-baseline gap-1.5 text-[14px] text-cream/80 transition-colors duration-150 hover:text-amber"
              >
                <span class="-ml-3 w-2 text-amber opacity-0 transition-opacity duration-150 group-hover:opacity-100" aria-hidden="true">→</span>
                {{ l.label }}
              </a>
            </li>
          </ul>
        </nav>
      </div>

      <!-- ZONE 2 — the brand promise, oversized -->
      <div class="mt-24 border-t border-cream/10 pt-20 text-center md:mt-32 md:pt-24">
        <div class="inline-flex items-center gap-2 font-mono text-[11px] uppercase tracking-[0.22em] text-amber">
          <span class="h-px w-6 bg-amber/50" aria-hidden="true" />
          The promise
          <span class="h-px w-6 bg-amber/50" aria-hidden="true" />
        </div>
        <h2
          class="font-display mt-6 leading-[0.9] text-cream"
          style="font-size: clamp(3.5rem, 12vw, 10rem);"
        >
          Be <em class="font-display-italic text-amber">in good</em> health.
        </h2>
      </div>

      <!-- ZONE 3 — FDA / DSHEA disclaimer card -->
      <div class="mx-auto mt-24 max-w-[720px]">
        <div class="mb-4 flex items-center justify-center gap-2.5 font-mono text-[10px] uppercase tracking-[0.24em] text-cream/45">
          <span class="h-px w-6 bg-cream/30" aria-hidden="true" />
          04 · Compliance Note
          <span class="h-px w-6 bg-cream/30" aria-hidden="true" />
        </div>
        <div class="relative rounded-2xl border border-cream/20 bg-ink-slate/40 px-6 py-7 backdrop-blur-sm md:px-10 md:py-8">
          <!-- Small asterisk mark, anchored at the top border -->
          <div
            aria-hidden="true"
            class="absolute -top-[11px] left-1/2 -translate-x-1/2 bg-midnight px-3 font-mono text-[14px] font-semibold text-amber"
          >
            *
          </div>
          <p class="text-center font-display-italic text-[15px] leading-[1.7] text-cream/80 md:text-[16px]">
            These statements have not been evaluated by the Food and Drug Administration. This product is not intended to diagnose, treat, cure or prevent any disease.
          </p>
        </div>
      </div>

      <!-- ZONE 4 — baseline: copyright, social, legal -->
      <div class="mt-16 border-t border-cream/10 pt-6">
        <div class="flex flex-col items-center gap-6 md:flex-row md:justify-between">
          <div class="font-mono text-[11px] uppercase tracking-[0.16em] text-cream/50">
            &copy; {{ currentYear }} BiGH &middot; Be in Good Health
          </div>

          <div class="flex items-center gap-3" aria-label="Social">
            <a
              href="#"
              aria-label="Instagram"
              class="flex h-9 w-9 items-center justify-center rounded-full border border-cream/15 text-cream/70 transition-[color,border-color,transform] duration-200 hover:-translate-y-0.5 hover:border-amber/60 hover:text-amber"
            >
              <svg class="h-4 w-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <rect x="2.5" y="2.5" width="19" height="19" rx="5" />
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z" />
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5" />
              </svg>
            </a>
            <a
              href="#"
              aria-label="X (Twitter)"
              class="flex h-9 w-9 items-center justify-center rounded-full border border-cream/15 text-cream/70 transition-[color,border-color,transform] duration-200 hover:-translate-y-0.5 hover:border-amber/60 hover:text-amber"
            >
              <svg class="h-[13px] w-[13px]" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z" />
              </svg>
            </a>
            <a
              href="#"
              aria-label="LinkedIn"
              class="flex h-9 w-9 items-center justify-center rounded-full border border-cream/15 text-cream/70 transition-[color,border-color,transform] duration-200 hover:-translate-y-0.5 hover:border-amber/60 hover:text-amber"
            >
              <svg class="h-[15px] w-[15px]" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M20.5 2h-17A1.5 1.5 0 0 0 2 3.5v17A1.5 1.5 0 0 0 3.5 22h17a1.5 1.5 0 0 0 1.5-1.5v-17A1.5 1.5 0 0 0 20.5 2zM8 19H5v-9h3zM6.5 8.25A1.75 1.75 0 1 1 8.3 6.5a1.78 1.78 0 0 1-1.8 1.75zM19 19h-3v-4.74c0-1.42-.6-1.93-1.38-1.93A1.74 1.74 0 0 0 13 14.19a.66.66 0 0 0 0 .14V19h-3v-9h2.9v1.3a3.11 3.11 0 0 1 2.7-1.4c1.55 0 3.36.86 3.36 3.66z" />
              </svg>
            </a>
          </div>

          <div class="flex flex-wrap items-center gap-x-6 gap-y-2 font-mono text-[11px] uppercase tracking-[0.16em] text-cream/50">
            <a href="#" class="transition-colors duration-150 hover:text-amber">Privacy</a>
            <a href="#" class="transition-colors duration-150 hover:text-amber">Terms</a>
            <a href="#" class="transition-colors duration-150 hover:text-amber">Sitemap</a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>
