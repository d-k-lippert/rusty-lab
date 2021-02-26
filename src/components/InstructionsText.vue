<template>
  <q-page class="row justify-evenly">
    <div class="page-content">
      <h2>Spiel-Anleitung</h2>
      <h4>Vorbereitung</h4>
      <p class="text-body1">
        Um die Kunst des Raparierens zu spielen, sind zwei Spieler:innen notwendig.
        Player 1 befindet sich in der VR-Anwendung und somit im Eisenblock vom Künstler Ulrich Eller. Player 2 ist der Operator und hilft Player 1 mit dieser
        Web-Anwendung durch das darin befindliche Labyrinth zu navigieren und die Rätsel darin zu lösen.
      </p>
      <h4>Ziel</h4>
      <h4>Hintergrund</h4>
      <h4>Story</h4>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'InstructionsText'
})
</script>
<style scoped>
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {
  .page-content {
    width: 95%;
  }
  h2 {
    font-size: 3.5em;
  }
}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {
  .page-content {
    width: 95%;
  }
}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {
  .page-content {
    width: 80%;
  }
}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {
  .page-content {
    width: 60%;
  }
}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {
  .page-content {
    width: 60%;
  }
}
@media only screen and (min-width: 1600px) {
  .page-content {
    width: 60%;
  }
}

.floor-color {
  background: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.5)),
    url(../../public/rust.jpg);
}
</style>
