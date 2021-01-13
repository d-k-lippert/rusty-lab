<template>
  <q-page class="row justify-center">
    <maze-content
    ></maze-content>
  </q-page>
</template>

<script lang="ts">
import MazeContent from 'components/MazeContent.vue'
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'PageIndex',
  components: { MazeContent },
  setup () {
    return {}
  }
})
</script>
