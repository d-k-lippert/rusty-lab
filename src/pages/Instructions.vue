<template>
  <instructions-text> </instructions-text>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'
import InstructionsText from '../components/InstructionsText.vue'

const title = 'Spielanleitung'

export default defineComponent({
  name: 'Instructions',
  meta: {
    title,
    meta: {
      ogTitle: { name: 'og:title', content: title }
    }
  },
  components: { InstructionsText },
  setup() {
    return {}
  }
})
</script>
