<script setup lang="ts">
/* ------------------------------------------------------------------
   AppNav — fixed top nav with About / Products / Science / Support.
   Products exposes a hover/focus dropdown styled after the Seed.com
   reference in design-references/seed-navbar.md:
     - light glassmorphic panel
     - each row = product thumbnail + code + name
------------------------------------------------------------------ */

type Product = {
  code: string
  name: string
  image: string
  href: string
}

const products: Product[] = [
  { code: 'OPC-01', name: 'Advanced OPC Formula', image: '/products/advanced-opc-formula.png', href: '#' },
  { code: 'RSH-02', name: 'Deer Horn Reishi',     image: '/products/deer-horn-reishi.png',     href: '#' },
  { code: 'PRP-03', name: 'Green Bee Propolis',   image: '/products/green-bee-propolis.png',   href: '#' },
  { code: 'CLM-04', name: 'Nature Calm',          image: '/products/nature-calm.png',          href: '#' },
  { code: 'CEL-05', name: 'NuriCell',             image: '/products/nuricell.png',             href: '#' },
  { code: 'GRN-06', name: 'Super Green',          image: '/products/super-green.png',          href: '#' },
  { code: 'TRM-07', name: 'Turmerific',           image: '/products/turmerific.png',           href: '#' },
]

const productsOpen = ref(false)
const productsButtonRef = ref<HTMLButtonElement | null>(null)
let closeTimer: ReturnType<typeof setTimeout> | null = null

function openProducts() {
  if (closeTimer) { clearTimeout(closeTimer); closeTimer = null }
  productsOpen.value = true
}

/* Slight close delay so the cursor can travel from the Products
   button to the panel below without losing hover. */
function scheduleClose() {
  if (closeTimer) clearTimeout(closeTimer)
  closeTimer = setTimeout(() => { productsOpen.value = false }, 120)
}

function closeAndReturnFocus() {
  productsOpen.value = false
  productsButtonRef.value?.focus()
}

function onKeydown(e: KeyboardEvent) {
  if (e.key === 'Escape' && productsOpen.value) {
    closeAndReturnFocus()
  }
}

onMounted(() => window.addEventListener('keydown', onKeydown))
onBeforeUnmount(() => {
  window.removeEventListener('keydown', onKeydown)
  if (closeTimer) clearTimeout(closeTimer)
})
</script>

<template>
  <header
    class="fixed inset-x-0 top-0 z-50 bg-black/80 backdrop-blur-xl backdrop-saturate-150"
    role="banner"
  >
    <nav
      class="mx-auto flex h-[72px] max-w-[1200px] items-center justify-between px-6"
      aria-label="Primary"
    >
      <!-- Brand logo -->
      <a
        href="#"
        class="inline-flex items-center transition-opacity duration-150 hover:opacity-80 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-offset-2 focus-visible:ring-offset-black"
        aria-label="BiGH — Be in Good Health, home"
      >
        <img
          src="/brand/bigh-logo-white.png"
          alt="BiGH"
          width="96"
          height="54"
          class="h-[54px] w-auto"
        >
      </a>

      <!-- Nav links -->
      <ul class="flex items-center gap-9 text-[16px] font-medium text-white/85">
        <li>
          <a
            href="#"
            class="transition-colors duration-150 hover:text-white focus-visible:text-white focus-visible:outline-none"
          >
            About
          </a>
        </li>

        <!-- Products with hover dropdown -->
        <li
          class="relative"
          @mouseenter="openProducts"
          @mouseleave="scheduleClose"
        >
          <button
            ref="productsButtonRef"
            type="button"
            class="inline-flex items-center gap-1 transition-colors duration-150 hover:text-white focus-visible:text-white focus-visible:outline-none"
            :aria-expanded="productsOpen"
            aria-haspopup="true"
            aria-controls="nav-products-panel"
            @focus="openProducts"
            @blur="scheduleClose"
          >
            Products
            <span aria-hidden="true" class="text-[11px] opacity-75">▾</span>
          </button>

          <Transition
            enter-active-class="transition duration-200 ease-out"
            enter-from-class="opacity-0 -translate-y-1"
            enter-to-class="opacity-100 translate-y-0"
            leave-active-class="transition duration-150 ease-in"
            leave-from-class="opacity-100 translate-y-0"
            leave-to-class="opacity-0 -translate-y-1"
          >
            <div
              v-if="productsOpen"
              id="nav-products-panel"
              class="absolute left-1/2 top-full z-50 mt-2 w-[380px] -translate-x-1/2
                     rounded-xl border border-black/5
                     bg-white/92 backdrop-blur-2xl backdrop-saturate-150
                     shadow-[0_20px_60px_rgba(0,0,0,0.25)]
                     py-2"
              role="menu"
              @mouseenter="openProducts"
              @mouseleave="scheduleClose"
            >
              <ul>
                <li
                  v-for="p in products"
                  :key="p.code"
                  role="none"
                >
                  <a
                    :href="p.href"
                    role="menuitem"
                    class="group flex items-center gap-4 px-4 py-2.5 transition-colors duration-150 hover:bg-black/5 focus-visible:bg-black/5 focus-visible:outline-none"
                  >
                    <!-- Thumbnail. PNGs are transparent, so wrap in a
                         soft off-white tile so they don't float on
                         the glass panel. -->
                    <div class="flex h-12 w-12 shrink-0 items-center justify-center rounded-md bg-slate-100">
                      <img
                        :src="p.image"
                        :alt="p.name"
                        class="h-11 w-11 object-contain"
                        loading="lazy"
                      >
                    </div>
                    <div class="flex-1 leading-tight">
                      <div class="text-[11px] font-medium uppercase tracking-[0.08em] text-slate-500">
                        {{ p.code }}
                      </div>
                      <div class="mt-0.5 text-[14px] font-semibold text-slate-900">
                        {{ p.name }}
                      </div>
                    </div>
                  </a>
                </li>
              </ul>
            </div>
          </Transition>
        </li>

        <li>
          <a
            href="#"
            class="transition-colors duration-150 hover:text-white focus-visible:text-white focus-visible:outline-none"
          >
            Science
          </a>
        </li>
        <li>
          <a
            href="#"
            class="transition-colors duration-150 hover:text-white focus-visible:text-white focus-visible:outline-none"
          >
            Support
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>
