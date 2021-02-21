<template>
  <div>
    <!-- <q-btn label="show terbium dialog" @click="terbiumModal = true" /> -->
    <q-dialog
      v-model="terbiumModal"
      persistent
      transition-show="scale"
      transition-hide="jump-up"
    >
      <q-card style="width: 300px" class="q-px-sm q-pb-md">
        <q-card-section class="row items-center q-pb-none">
          <!-- <div class="text-h6">Terbium-Cube </div> -->
          <q-space />
        </q-card-section>
        <q-card-section
          class="row items-center justify-between q-pa-md q-ma-md"
        >
          <q-btn
            size="xl"
            label="T"
            color="blue"
            @click="resetPlayer"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            icon="opacity"
            color="positive"
            @click="moveTerbiumCube"
            round
            dense
            v-close-popup
          />
          <q-btn
            size="xl"
            icon="opacity"
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
            icon="opacity"
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
            icon="opacity"
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
            icon="dangerous"
            color="secondary"
            @click="resetPlayer"
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
  name: 'TerbiumDialog',
  props: { x: Number, y: Number },
  setup(props) {
    const terbiumModal = ref(false)
    const terbiumModalSolved = ref(false)

    watch(
      () => props,
      () => {
        /* console.log('deep ', props.x, props.y) */
        if (props.x === 11 && props.y === 3) {
          if (terbiumModalSolved.value === false) {
            terbiumModal.value = true
            console.log('OPEN TERBIUM MODAL!')
          }
        }
      },
      { deep: true }
    )

    function moveTerbiumCube() {
      const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
      // adding class to modal
      modal!.className += ' right-answer'
      eventBus.$emit('move-terbium-cube', () => {
        console.log('terbium emitted')
      })
      terbiumModalSolved.value = true
    }
    function resetPlayer() {
      const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
      modal!.className += ' wrong-answer'
      // console.log(modal)
      eventBus.$emit('reset-player', () => {
        console.log('reset player')
      })
    }
    return { terbiumModal, moveTerbiumCube, resetPlayer }
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
