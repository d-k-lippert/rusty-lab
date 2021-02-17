<template>
  <div>
    <!-- <q-btn label="show nickel dialog" @click="nickelModal = true" /> -->
    <q-dialog
      v-model="nickelModal"
      persistent
      transition-show="scale"
      transition-hide="jump-up"
    >
      <q-card style="width: 300px" class="q-px-sm q-pb-md">
        <q-card-section class="row items-center q-pb-none">
          <!-- <div class="text-h6">Nickel-Cube </div> -->
          <q-space />
        </q-card-section>
        <q-card-section
          class="row items-center justify-between q-pa-md q-ma-md"
        >
          <q-btn
            size="xl"
            label="N"
            color="blue"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            icon="anchor"
            color="positive"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            icon="anchor"
            color="warning"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
        </q-card-section>
        <q-card-section
          class="row items-center justify-between q-pa-md q-ma-md"
        >
          <q-btn
            size="xl"
            icon="anchor"
            color="accent"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            icon="close"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            icon="anchor"
            color="red"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
        </q-card-section>
        <q-card-section
          class="row items-center justify-between q-pa-md q-ma-md"
        >
          <q-btn
            size="xl"
            icon="change_history"
            color="primary"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            label="3"
            color="secondary"
            @click="moveNickelCube"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            label="9"
            color="black"
            @click="resetPlayer"
            round
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
  name: 'NickelDialog',
  props: { x: Number, y: Number },
  setup(props) {
    const nickelModal = ref(false)
    const nickelModalSolved = ref(false)

    watch(
      () => props,
      () => {
        console.log('deep ', props.x, props.y)
        if (props.x === 11 && props.y === 6) {
          if (nickelModalSolved.value === false) {
            nickelModal.value = true
            console.log('OPEN NICKEL MODAL!')
          }
        }
      },
      { deep: true }
    )

    function moveNickelCube() {
      const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
      // adding class to modal
      modal!.className += ' right-answer'
      eventBus.$emit('move-nickel-cube', () => {
        console.log('nickel emitted')
      })
      nickelModalSolved.value = true
    }
    function resetPlayer() {
      const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
      modal!.className += ' wrong-answer'
      // console.log(modal)
      eventBus.$emit('reset-player', () => {
        console.log('reset player')
      })
    }
    return { nickelModal, moveNickelCube, resetPlayer }
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
