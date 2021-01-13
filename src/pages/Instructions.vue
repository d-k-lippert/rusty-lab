<template>
  <instructions-text>
  </instructions-text>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'
import InstructionsText from 'components/InstructionsText.vue'

export default defineComponent({
  name: 'Instructions',
  components: { InstructionsText },
  setup () {
    return {}
  }
})
</script>
