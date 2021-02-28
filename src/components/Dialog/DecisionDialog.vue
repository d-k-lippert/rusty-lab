<template>
  <div>
    <q-dialog
      v-model="decisionModal"
      persistent
      transition-show="scale"
      transition-hide="jump-up"
    >
      <q-card style="width: 300px" class="q-px-sm q-pb-md">
        <q-card-section class="row items-center q-pb-none">
          <div class="text-h6 q-mb-md bg-yellow">&nbsp; ACHTUNG! &nbsp;</div>
          <div class="text">
            Möchtest du diese Tür wirklich öffnen? Öffnest du sie, nimmst du
            eine Abkürzung, wirst jedoch nicht alle Klangmaschinen reparieren
            können. Diese Entscheidung wird weitreichende Konsequenzen mit sich
            ziehen.
          </div>
          <q-space />
        </q-card-section>
        <q-card-section
          class="row items-center justify-between q-pa-md q-mt-md q-mb-md"
        >
          <q-btn
            size="md"
            color="negative"
            label="Tür öffnen"
            @click="openShortcut"
            dense
            v-close-popup
          />
          <q-btn
            size="md"
            label="Abbrechen"
            @click="resetShortcut"
            color="positive"
            dense
            v-close-popup
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
  name: 'DecisionDialog',
  props: { doorOpened:Boolean },
  setup(props) {
    const decisionModal = ref(false)
    const decisionModalActivated = ref(false)

    watch(
      () => props,
      () => {
        /* console.log('deep ', props.x, props.y) */

        if (props.doorOpened) {
          if (decisionModalActivated.value === false) {
            decisionModal.value = true
            console.log(props.doorOpened)
            console.log('OPEN DECISION MODAL!')
          }
        }
      },
      { deep: true }
    )

    function openShortcut() {
      const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
      // adding class to modal
      modal!.className += ' right-answer'
      eventBus.$emit('open-shortcut', () => {
        console.log('shortcut emitted')
      })
      decisionModalActivated.value = true
    }
        function resetShortcut() {
      // adding class to modal
      eventBus.$emit('reset-shortcut', () => {
        console.log('reset shortcut emitted')
      })
       decisionModal.value = false
      decisionModalActivated.value = false
    }

    return { decisionModal, openShortcut, resetShortcut }
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
