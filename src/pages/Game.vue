<template>
  <q-page class="row justify-center">
    <maze-content></maze-content>
  </q-page>
</template>

<script lang="ts">
import MazeContent from '../components/MazeContent.vue'
import { defineComponent } from '@vue/composition-api'

const title = 'Spiel'

export default defineComponent({
  name: 'PageIndex',
  meta: {
    title,
    meta: {
      ogTitle: { name: 'og:title', content: title }
    }
  },
  components: { MazeContent },
  setup() {
    return {}
  }
})
</script>
