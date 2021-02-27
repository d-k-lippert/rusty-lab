<template>
  <div>
    <q-dialog v-model="entryInput" persistent>
      <q-card style="min-width: 350px">
        <q-card-section>
          <div class="text-h6">
            Bitte geben Sie die Block-Identifikationsnummer ein, um die
            Satellitenübertragung zu starten.
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-input
            dense
            v-model="blockIdentifier"
            autofocus
            @keyup.enter="sendBlockIdentifier"
          />
        </q-card-section>

        <q-card-actions align="center">
          <q-btn
            color="positive"
            label="Bestätigen"
            @click="sendBlockIdentifier"
          />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from '@vue/composition-api'
import eventBus from 'src/event-bus/event-bus'
import { Notify } from 'quasar'
export default defineComponent({
  name: 'EntryInput',
  setup() {
    const entryInput = ref(true)
    const blockIdentifier = ref('')

    function sendBlockIdentifier() {
      console.log(blockIdentifier.value)
      if (blockIdentifier.value === 'ferrum-magneticum-97') {
        entryInput.value = false
        Notify.create({
          message: 'Eingabe erfolgreich!',
          caption: 'Die Satellitenverbindung wird aufgebaut',
          color: 'positive',
          position: 'center',
          icon: 'success',
          timeout: 2500,
          spinner: true
        })

        eventBus.$emit('connect-server', () => {
          console.log('event emitted to connect to server')
        })
      } else {
        Notify.create({
          message: 'Sie haben eine falsche Block-Kennung eingegeben',
          caption: 'Hat Ihr Partner Ihnen die richtige Kennung mitgeteilt?',
          color: 'negative',
          position: 'center',
          icon: 'warning',
          timeout: 2500
        })
      }
    }

    return { entryInput, blockIdentifier, sendBlockIdentifier }
  }
})
</script>
<style>
.q-dialog__backdrop.fixed-full {
  background: rgba(0, 0, 0, 0.95);
}
</style>
