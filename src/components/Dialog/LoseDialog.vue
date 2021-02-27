<template>
  <div>
    <q-dialog
      v-model="loseModal"
      persistent
      transition-show="scale"
      transition-hide="jump-up"
    >
      <q-card
        style="width: 300px"
        class="q-px-sm q-pb-md bg-red-6 text-white"
      >
        <q-card-section class="row items-center q-pb-none">
          <div class="text-h6 q-mb-md">Störung! &nbsp;</div>
          <div class="text">
            <p>Verbindung unterbrochen. Das hätte nicht passieren dürfen.</p>
            <p>
              Es wurden technische Schwierigkeiten festgestellt. Mehrere Versuche Sie mit 
              der Bodeneinheit zu verbinden sind fehlgeschlagen. 
            </p>
            <p>
              Das Objekt mit der Kennung: <br>
              <code>ferrum-magneticum-97</code> <br>
               wurde unwiderruflich verriegelt. Wir bitten um Ihr Verständnis.
            </p>
          </div>
          <q-space />
        </q-card-section>
        <q-card-section
          class="row items-center justify-center q-pa-md q-mt-md q-mb-md"
        >
          <q-btn
            size="md"
            type="a"
            label="Führungsetage kontaktieren"
            target="_self"
            href="tel:+4915784444905"
            dense
            color="orange"
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
  name: 'LoseDialog',
  props: { gameLost: Boolean, timeNeeded: Number },
  setup(props) {
    const loseModal = ref(false)
    const loseModalActivated = ref(false)

    // decomment to show message
    /*     if (loseModalActivated.value === false) {
            loseModal.value = true
            console.log(props.puzzlesSolved)
            console.log('OPEN LOSE MODAL!')
          } */

    watch(
      () => props,
      () => {
        if (props.gameLost === true) {
          if (loseModalActivated.value === false) {
            loseModal.value = true
            console.log(props.gameLost)
            console.log('OPEN LOSE MODAL!')
            sendLoseMessage()
          }
        }
      },
      { deep: true }
    )

    function sendLoseMessage() {
      // adding class to modal
/*       eventBus.$emit('open-lose-message', () => {
        console.log('lose message emitted')
      }) */
      loseModalActivated.value = true
    }

    return { loseModal, sendLoseMessage }
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
