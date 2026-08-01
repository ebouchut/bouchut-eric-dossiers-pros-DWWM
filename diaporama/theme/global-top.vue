<!--
  Global layer of the theme, rendered ABOVE every slide (a `global-bottom`
  layer would sit BELOW the slide, hidden behind the opaque background the
  theme paints on .slidev-layout). Shows "current / total" on every slide
  except the cover.

  Use $nav (injection-aware: per-printed-page during `slidev export
  --per-slide`) rather than <SlideCurrentNo />, whose slide context is not
  provided to global layers and would print "1" on every exported page.

  The color comes from a semantic token: global layers live OUTSIDE
  .slidev-layout, so they inherit the app default (white) instead of the
  theme text color -- the tokens are declared on :root precisely so they
  stay resolvable here.
-->
<template>
  <footer
    v-if="!['cover', 'intro', 'end'].includes($nav.currentLayout)"
    class="absolute bottom-0 left-0 right-0 p-2 text-right text-xs pointer-events-none"
  >
    {{ $nav.currentPage }} / {{ $nav.total }}
  </footer>
</template>

<style scoped>
footer {
  color: var(--ld-page-number);
}
</style>
