<template>
  <div class="row justify-center" v-if="amountPuzzlesSolved < 3">
    <!-- style="max-width: 350px" -->
    <div class="q-pa-md maze-wrapper">
      <q-list bordered class="rounded-borders">
        <q-expansion-item
          :content-inset-level="0.5"
          expand-separator
          icon="help"
          label="Tipps"
          caption="3 Tipps verfügbar"
        >
          <q-expansion-item
            :content-inset-level="0.5"
            expand-separator
            icon="info"
            label="Tipp 1"
          >
            <q-card>
              <q-card-section>
                {{ tips.tip1 }}
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            :content-inset-level="0.5"
            expand-separator
            icon="info"
            label="Tipp 2"
          >
            <q-card>
              <q-card-section>
                {{ tips.tip2 }}
              </q-card-section>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            :content-inset-level="0.5"
            expand-separator
            icon="info"
            label="Tipp 3"
          >
            <q-card>
              <q-card-section>
                {{ tips.tip3 }}
              </q-card-section>
            </q-card>
          </q-expansion-item>
        </q-expansion-item>
      </q-list>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@vue/composition-api'

export default defineComponent({
  name: 'GameTips',
  props: { puzzlesSolved: Number },
  setup(props) {
    const amountPuzzlesSolved = ref(0) // start value x

    const tips = {
      tip1: ref(
        'Schaue an die Wand, ist dort etwas Besonderes mit dem interagiert werden kann?'
      ),
      tip2: ref('Miau!'),
      tip3: ref(
        'Gleicht die Formen und Farben ab, es gibt nur eine eindeutige Lösung!'
      )
    }

    watch(
      () => props.puzzlesSolved,
      (oldVal, newVal) => {
        if (typeof props.puzzlesSolved === 'number') {
          amountPuzzlesSolved.value = props.puzzlesSolved
          if (amountPuzzlesSolved.value === 1) {
            tips.tip1.value =
              'Wo siehst du unterschiedliche Farben bei den Elektromagneten im Handbuch?'
            tips.tip2.value = 'Schaue an die Seitenwände'
            tips.tip3.value = 'Betrete die Symbole, die du im Handbuch siehst.'
          }
          if (amountPuzzlesSolved.value === 2) {
            tips.tip1.value = 'Denk an deinen Chemieunterricht'
            tips.tip2.value =
              'Die Knöpfe in den Fenstern müssen gedrückt werden.'
            tips.tip3.value =
              'Rede viel mit deinem Partner bze. deiner Partnerin!'
          }
        }
      }
    )

    return { amountPuzzlesSolved, tips }
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
    width: 60%;
    height: 450px;
  }
}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {
  .maze-wrapper {
    width: 50%;
    height: 450px;
  }
}
@media only screen and (min-width: 1600px) {
  .maze-wrapper {
    width: 40%;
    height: 450px;
  }
}
/* .maze-wrapper {
  width: 30%;
  height: 450px;
} */
</style>
