<template>
  <footer
    v-if="$nav.currentLayout !== 'cover'"
    class="absolute bottom-4 left-0 right-4 text-right"
  >
    <br/><small><SlideCurrentNo/>/<SlidesTotal/></small><br/>
  </footer>
</template>
