<template>
  <div>
    <q-dialog
      v-model="winModal"
      persistent
      transition-show="scale"
      transition-hide="jump-up"
    >
      <q-card
        style="width: 300px"
        class="q-px-sm q-pb-md bg-green-6 text-white"
      >
        <q-card-section class="row items-center q-pb-none">
          <div class="text-h6 q-mb-md">Glückwunsch &nbsp;</div>
          <div class="text">
            Ihr habt alle Klangmaschinen rechtzeitig repariert. Die
            Führungsetage ist zufrieden, der Auftraggeber ist zufrieden und die
            Kunstkritiker loben den FH Campus. Ihr habt's echt drauf!
          </div>
          <q-space />
        </q-card-section>
        <q-card-section
          class="row items-center justify-center q-pa-md q-mt-md q-mb-md"
        >
          <q-btn
            size="lg"
            type="a"
            label="Feierabend machen"
            target="_self"
            href="/#/"
            dense
            color="positive"
            v-close-popup
            class="q-ma-md q-pl-md q-pr-md"
          />
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@vue/composition-api'
import eventBus from 'src/event-bus/event-bus'
export default defineComponent({
  name: 'WinDialog',
  props: { puzzlesSolved: Number },
  setup(props) {
    const winModal = ref(false)
    const winModalActivated = ref(false)

// decomment to show message 
/*     if (winModalActivated.value === false) {
            winModal.value = true
            console.log(props.puzzlesSolved)
            console.log('OPEN WIN MODAL!')
          } */

    watch(
      () => props,
      () => {
        if (props.puzzlesSolved === 3) {
          if (winModalActivated.value === false) {
            winModal.value = true
            console.log(props.puzzlesSolved)
            console.log('OPEN WIN MODAL!')
          }
        }
      },
      { deep: true }
    )

    function sendWinMessage() {
      const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
      // adding class to modal
      modal!.className += ' right-answer'
/*       eventBus.$emit('open-win-message', () => {
        console.log('win message emitted')
      }) */
      winModalActivated.value = true
    }

    return { winModal, sendWinMessage }
  }
})
</script>
<style>
.right-answer {
  background: rgba(8, 65, 8, 0.6);
}
.wrong-answer {
  background: rgba(65, 15, 8, 0.6);
}
</style>
