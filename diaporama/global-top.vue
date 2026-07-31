<!--
  Global layer rendered ABOVE every slide (a `global-bottom.vue` layer would
  sit BELOW the slide, hidden behind the opaque Latte background set in
  style.css). Shows "current / total" on every slide except the cover.

  Use $nav (injection-aware: per-printed-page during `slidev export
  --per-slide`) rather than <SlideCurrentNo />, whose slide context is not
  provided to global layers and would print "1" on every exported page.

  The color is set explicitly: global layers live OUTSIDE .slidev-layout, so
  they inherit the app default (white) instead of the theme text color --
  white at 60% opacity is invisible on the light Latte background.
-->
<template>
  <footer
    v-if="$nav.currentLayout !== 'cover'"
    class="absolute bottom-0 left-0 right-0 p-2 text-right text-xs pointer-events-none"
  >
    {{ $nav.currentPage }} / {{ $nav.total }}
  </footer>
</template>

<style scoped>
footer {
  /* Catppuccin Latte "subtext0": subtle but readable on the #eff1f5 base */
  color: #6c6f85;
}
</style>
