<template>
<div>
    <!-- <q-btn label="show cobalt dialog" @click="cobaltModal = true" /> -->
    <q-dialog v-model="cobaltModal" persistent transition-show="scale" transition-hide="jump-up">
      <q-card style="width: 300px" class="q-px-sm q-pb-md">
        <q-card-section class="row items-center q-pb-none ">
        <div class="text-h6">Kobalt-Cube </div>
        <q-space />
        </q-card-section>
         <q-card-section class="row items-center justify-between q-pa-md q-ma-md">
          <q-btn size="xl" label="C" color="blue" @click="resetPlayer" round dense v-close-popup />
          <q-btn size="xl" icon="close" color="positive" @click="resetPlayer"  round dense v-close-popup />
          <q-btn size="xl" icon="close" color="warning" @click="resetPlayer"  round dense v-close-popup />
        </q-card-section>
         <q-card-section class="row items-center justify-between q-pa-md q-ma-md">
          <q-btn size="xl" icon="close" color="accent" @click="resetPlayer" round dense v-close-popup />
          <q-btn size="xl" icon="close" @click="moveCobaltCube" round dense v-close-popup />
          <q-btn size="xl" icon="anchor" color="red" @click="resetPlayer" round dense v-close-popup />
        </q-card-section>
         <q-card-section class="row items-center justify-between q-pa-md q-ma-md">
          <q-btn size="xl" icon="change_history" color="primary" @click="resetPlayer" round dense v-close-popup />
          <q-btn size="xl" icon="dangerous" color="secondary" @click="resetPlayer" round dense v-close-popup />
          <q-btn size="xl" label="9" color="black" @click="resetPlayer" round dense v-close-popup />
        </q-card-section>
      </q-card>
    </q-dialog>
</div>
</template>

<script lang="ts">
import { defineComponent, Ref, ref, watch } from '@vue/composition-api'
import eventBus from 'src/event-bus/event-bus'
export default defineComponent({
  name: 'CobaltDialog',
  props: { x: Number, y: Number },
  setup (props) {

    const cobaltModal = ref(false)

    const propX = ref(props.x)
    const propY = ref(props.y)

    watch(() => props, () => {
      console.log("deep ", props.x, props.y);
      if(props.x === 12 && props.y === 5){
            cobaltModal.value=true
            console.log('OPEN COBALT MODAL!')
        }
    },
    { deep: true }
    );
        
    function moveCobaltCube () {
        const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
        // adding class to modal
         modal!.className+=' right-answer'
      eventBus.$emit('move-cobalt-cube', () => {
      
    })
    }
    function resetPlayer () {
        const modal = document.querySelector('.q-dialog__backdrop.fixed-full')
         modal!.className+=' wrong-answer'
         //console.log(modal)
      eventBus.$emit('reset-player', () => {
      /* console.log('Custom event triggered!') */
    })
    }
    return { cobaltModal, moveCobaltCube, resetPlayer }
  }
})
</script>
<style>
.right-answer{
    background: rgba(8, 65, 8, 0.6);
}
.wrong-answer{
    background: rgba(65, 15, 8, 0.6);
}
</style>
