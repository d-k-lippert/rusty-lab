<template>
  <div class="row justify-center">
    <!-- {{puzzlesSolved}} <br/> -->
    <q-circular-progress
      show-value
      class="text-white q-ma-md"
      :value="amountPuzzlesSolved"
      size="90px"
      :thickness="0.3"
      color="secondary"
      center-color="grey-5"
      track-color="transparent"
      min="0"
      max="3"
    ></q-circular-progress>
    <div class="align-center">
      {{ amountPuzzlesSolved }}/3 Klangmaschinen repariert
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@vue/composition-api'

export default defineComponent({
  name: 'GameProgress',
  props: { puzzlesSolved: Number },
  setup(props) {
    const amountPuzzlesSolved = ref(0) // start value x

    const roundedProgress = ref(0)
    roundedProgress.value = Math.round(amountPuzzlesSolved.value * 33.333333333)
    watch(
      () => props.puzzlesSolved,
      (oldVal, newVal) => {
        if (typeof props.puzzlesSolved === 'number') {
          amountPuzzlesSolved.value = props.puzzlesSolved
          roundedProgress.value = Math.round(
            amountPuzzlesSolved.value * 33.333333333
          )
        }
      }
    )

    return { amountPuzzlesSolved, roundedProgress }
  }
})
</script>
<style scoped>
.maze-heigth {
  height: 80%;
}

.floor-color {
  background: url(../../public/rust.jpg);
}

.align-center {
  display: flex;
  align-items: center;
}

/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {
  .maze-wrapper {
    width: 100%;
    height: 550px;
  }
}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {
  .maze-wrapper {
    width: 100%;
    height: 700px;
  }
}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {
  .maze-wrapper {
    width: 90%;
    height: 800px;
  }
}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {
  .maze-wrapper {
    width: 40%;
    height: 450px;
  }
}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {
  .maze-wrapper {
    width: 30%;
    height: 450px;
  }
}
@media only screen and (min-width: 1600px) {
  .maze-wrapper {
    width: 25%;
    height: 450px;
  }
}
/* .maze-wrapper {
  width: 30%;
  height: 450px;
} */
</style>
