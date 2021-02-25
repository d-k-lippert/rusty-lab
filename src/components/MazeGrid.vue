<template>
  <div class="row justify-center">
    <div
      class="maze-wrapper maze-height floor-color q-mb-md row justify-center"
    >
      <div
        style="z-index: 4; touch-action: none; user-select: none"
        v-for="n in 512"
        :key="n"
        :style="computeStyle(n)"
      ><!-- {{n}} --></div>
    </div>
    <!-- {{x}} {{y}} -->
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@vue/composition-api'

export default defineComponent({
  name: 'MazeGrid',
  props: { x: Number, y: Number },
  setup(props) {
    const userX = ref(5) // start value x
    const userY = ref(32) // start value y

    watch(
      () => props.x,
      (oldVal, newVal) => {
        // always watch changes for x values sent from vr-app
        /*       console.log(
        'value für x',
        newVal
      ) */
        const propToPosX = props.x
        if (typeof propToPosX === 'number') {
          userX.value = propToPosX
        }
      }
    )
    // always watch changes for y values sent from vr-app
    watch(
      () => props.y,
      (oldVal, newVal) => {
        /*       console.log(
        'values für y',
        newVal
      ) */
        const propToPosY = props.y
        if (typeof propToPosY === 'number') {
          userY.value = propToPosY
        }
      }
    )

    const computeStyle = (gridPos: number) => {
      const colWidth = 6.25
      // tint walls dark
      if (tintWalls(gridPos)) {
        return {
          position: 'block',
          width: `${colWidth}%`,
          height: `${colWidth / 2}%`,
          /* border: "solid 1px #ffffff", */
          /* background: "#efefef" */
          background:
            'linear-gradient(rgba(0, 0, 0, 0.55), rgba(0, 0, 0, 0.55))'
        }
      } else {
        if (showUser(userX.value, userY.value, gridPos)) {
          return {
            position: 'block',
            width: `${colWidth}%`,
            height: `${colWidth / 2}%`,
            /* border: "solid 1px #ffffff", */
            background: '#afffaf',
            borderRadius: '4px',
            boxShadow: '0px 0px 15px #afffaf'
          }
        }
        else if (gridPos === 210) {
          return {
            position: 'block',
            width: `${colWidth}%`,
            height: `${colWidth / 2}%`,
            background:
            'linear-gradient(rgba(200, 0, 0, 0.55), rgba(200, 0, 0, 0.55))'
          }
        } 
        else if (gridPos === 72 || gridPos === 142 || gridPos === 276 || gridPos === 284 || gridPos === 471) {
          return {
            position: 'block',
            width: `${colWidth}%`,
            height: `${colWidth / 2}%`,
            background:
            'linear-gradient(rgba(200, 200, 0, 0.3), rgba(200, 200, 0, 0.3))'
          }
        }
        else {
          return {
            position: 'block',
            width: `${colWidth}%`,
            height: `${colWidth / 2}%`
            /* border: "solid 1px #ababab" */
          }
        }
      }
    }

    const tintWalls = (gridPos: number): boolean => {
      /* const numRows = 32; */
      const numCols = 16
      const row = Math.floor((gridPos - 1) / numCols) + 1
      const col = ((gridPos - 1) % numCols) + 1

      if (
        col === 1 || // erste spalte
        (col === 16 && row !== 5) || // 16te spalte
        (row === 1 && col !== 14) || // erste reihe mit eingang
        (row === 2 && (col === 6 || col === 8)) || // 2te reihe
        (row === 3 && (col === 3 || col === 4 || col === 8)) || // 3te Reihe
        (row === 4 && col >= 4 && col <= 8) || // 4te reihe
        (row === 5 && col === 2) || // 5te reihe
        (row === 6 && col > 1 && col < 5) || // 6te reihe
        (row === 6 && col > 5 && col <= 8) || // 6te reihe
        (row === 7 && col === 8) || // 7te reihe
        (row === 8 && col >= 3 && col <= 6) || // 8te reihe
        (row === 8 && col === 8) || // 8te reihe
        (row === 9 &&
          (col === 3 || col === 6 || (col >= 8 && col <= 13) || col === 15)) || // 9te reihe
        (row === 10 && (col === 3 || col === 5 || col === 6)) || // 10te reihe
        (row === 11 && (col === 8 || col === 10 || (col >= 12 && col <= 14))) || // 11te reihe
        (row === 12 &&
          (col === 2 ||
            col === 4 ||
            (col >= 6 && col <= 8) ||
            col === 10 ||
            col === 12)) || // 12te reihe
        (row === 13 && (col === 4 || col === 10 || col === 14)) || // 13te reihe
        (row === 14 && col !== 2 && col !== 13) || // 14te reihe
        (row === 15 && (col === 4 || col === 12 || col === 14)) || // 15te reihe
        (row === 16 && (col === 2 || col === 4 || col === 12)) || // 16te reihe
        (row === 17 && (col === 2 || col === 4 || (col >= 12 && col <= 14))) || // 17te reihe
        (row === 18 && (col === 2 || col === 14)) || // 18te reihe
        (row === 19 && (col === 4 || col === 12 || col === 14)) || // 19te reihe
        (row === 20 && (col === 3 || col === 4 || col === 12 || col === 14)) || // 20te reihe
        (row === 21 && (col === 4 || col === 12)) || // 21te reihe
        (row === 22 && col !== 3 && col !== 15) || // 22te reihe
        (row === 23 && (col === 5 || col === 14)) || // 23te reihe
        (row === 24 && (col === 3 || col === 5 || col === 14)) || // 24te reihe
        (row === 24 && col >= 7 && col <= 12) || // 24te reihe
        (row === 25 && (col === 3 || col === 7 || col === 14)) || // 25te reihe
        (row === 26 && col >= 3 && col <= 5) || // 26te reihe
        (row === 26 && (col === 7 || col === 9 || (col >= 11 && col !== 13))) || // 26te reihe
        (row === 27 && (col === 7 || col === 9 || col === 12 || col === 15)) || // 27te reihe
        (row === 28 && col >= 3 && col !== 8 && col !== 10 && col !== 14) || // 28te reihe
        (row === 29 && (col === 3 || col === 7)) || // 29te reihe
        (row === 29 && (col === 9 || col === 10 || col === 11 || col === 13)) || // 29te reihe
        (row === 30 && (col === 3 || col === 9 || col === 13 || col === 14)) || // 30te reihe
        (row === 31 && (col === 3 || col === 7 || col === 11)) || // vorletzte reihe
        (row === 32 && col !== 5) // letzte reihe mit eingang
      ) {
        return true
      } else {
        return false
      }
    }
    const showUser = (x: number, y: number, gridPos: number): boolean => {
      const numCols = 16
      const row = Math.floor((gridPos - 1) / numCols) + 1
      const col = ((gridPos - 1) % numCols) + 1
      if (x === col && y === row) {
        return true
      } else {
        return false
      }
    }
    return { computeStyle }
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
