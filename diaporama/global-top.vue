<!--
  Global layer rendered ABOVE every slide (a `global-bottom.vue` layer would
  sit BELOW the slide, hidden behind the opaque Latte background set in
  style.css). Shows "current / total" on every slide except the cover.

  Use $nav (injection-aware: per-printed-page during `slidev export`) rather
  than <SlideCurrentNo />, whose slide context is not provided to global
  layers and would print "1" on every exported page.
-->
<template>
  <footer
    v-if="$nav.currentLayout !== 'cover'"
    class="absolute bottom-0 left-0 right-0 p-2 text-right text-xs op60 pointer-events-none"
  >
    {{ $nav.currentPage }} / {{ $nav.total }}
  </footer>
</template>
