<template>
  <q-page class="row justify-evenly">
    <div class="page-content q-mb-xl">
      <h2>Was is die Kunst des Reparierens?</h2>
      <h4>Vorbereitung</h4>
      <div>
        Die Kunst der Reparierens ist eine asynchrone Multiplayer
        VR-Browser-Anwendung. Dazu werden zwei Spielende benötigt, die gemeinsam
        Rätsel lösen und das in einem Eisenblock befindliche Labyrinth
        durchschreiten müssen. Zum Spielen werden eine VR-Brille, ein PC, Tablet
        oder Smartphone und ein Ausdruck des Reparatur-Handbuchs (am PC auch als
        PDF vorhanden) benötigt.
      </div>
      <h4>Story</h4>
      <div>
        <p>
          Ihr seid neue Mitarbeitende der Firma Kunsterwerkers. Das heißt ihr
          repariert Kunstwerke von verrückten Künstlern und Künstlerinnen. Ihr
          erhaltet einen Auftrag vom Kanzler der Fachhoschule Kiel. Der
          Eisenblock von Ulrich Eller, eine Klangskulptur, hat aufgehört zu
          klingen.
        </p>
        <q-card flat bordered class="q-mb-lg bg-orange-1">
          <q-card-section>
            <div class="text-h6">Auftrag</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            <p>Auftraggeber: <strong>Klaus-Michael Heinze</strong></p>
            <p>Datum: 08.03.2021</p>
          </q-card-section>

          <q-separator inset />

          <q-card-section class="q-ml-xl">
            <p>Objekt: Eisenblock</p>
            <p>Baujahr: 1997</p>
            <p>Künstler/in: Ulrich Eller</p>
            <p>Außenansicht:</p>
            <q-img class="img-size q-mb-md" src="../../public/eisenblock.jpg" />
            <p>Besonderheiten: *</p>
          </q-card-section>

          <q-separator inset />

          <q-card-section>
            <p>
              Systemdiagnose: <strong>drei Klangmaschinen ausgefallen</strong>
            </p>
          </q-card-section>

          <q-separator inset />

          <q-card-section>
            <p>Problembehebung: <strong>Reparatur vor Ort</strong></p>
          </q-card-section>

          <q-separator inset />

          <q-card-section>
            <p>
              Priorität: <strong class="text-red underlined">sehr hoch</strong>
            </p>
          </q-card-section>
          <q-separator inset />

          <q-card-section>
            <p class="ultra-small">
              *: vorherige Techniker/innen sind aus dem Eisenblock nicht
              zurückgekehrt
            </p>
          </q-card-section>
        </q-card>
        <p>
          Einen unpassenderen Zeitpunkt dafür hätte es nicht geben können, denn
          die besten Fachleute der Firma sind im Urlaub, auf Montage, machen
          krank oder haben sich vehement dagegen gewehrt diesen Auftrag
          anzunehmen, da sie "Bedenken wegen mangelnder Sicherheit" haben.
        </p>
        <p>
          Ihr seid also gefragt, denn der Auftraggeber macht Druck. In wenigen
          Stunden wird es auf dem Campus der Fachhochschule Kiel von Menschen
          wimmeln, da renommierte Kunstkritiker den Campus besuchen werden.
          Deren Meinung bestimmt den Fortbestand der Fachhochschule. Und da die
          Fachhochschule euer größter Kunde ist, bestimmen diese Kritiker also
          auch euren Fortbestand.
        </p>
        <p>
          Blöd gelaufen. Ihr müsst euch also beeilen und außerdem gründlich
          arbeiten. Pfusch am Bau wird nämlich bestraft.
        </p>
        <p>
          Als Fachleute auf eurem Gebiet geht ihr arbeitsteilig an diese
          komplexe Herausforderung heran. Ihr schwingt euch beide in eure
          Kunstwerker-Overalls und fahrt mit eurem Firmen-Van so schnell wie
          möglich zum Eisenblock. 2 Blitzerfotos später steht ihr im
          geschlossenem Van vor dem Eisenblock.
        </p>
        <p>Eine beunruhigende Stille macht sich breit.</p>
        <p>
          Ihr spielt eine Runde Stein, Schere, Papier, wer in den Eisenblock
          geht. Der Gewinner unterstützt das arme Schwein im Block. Als Operator
          sitzt du im Van und hast das Reparatur-Handbuch sowie die
          Überwachungssoftware: Eagle Eye vor dir. Ihr wünscht euch beide viel
          Glück und verabschiedet euch.
        </p>
        <div class="row justify-evenly">
          <q-btn
            size="lg"
            type="a"
            label="Handbuch öffnen"
            target="_blank"
            href="documents/Reparatur-Handbuch.pdf"
            dense
            v-close-popup
            class="floor-color q-ma-md q-pl-md q-pr-md"
          />
          <q-btn
            size="lg"
            type="a"
            label="eagle eye starten"
            target="_self"
            href="/#/game"
            dense
            v-close-popup
            class="floor-color q-ma-md q-pl-md q-pr-md"
          />
        </div>
      </div>
    </div>
    <!-- <example-component> </example-component> -->
  </q-page>
</template>

<script lang="ts">
// import ExampleComponent from '../components/CompositionComponent.vue'
import { defineComponent } from '@vue/composition-api'

const title = 'Home'

export default defineComponent({
  name: 'PageIndex',
  meta: {
    title,
    meta: {
      ogTitle: { name: 'og:title', content: title }
    }
  },
  /* components: { ExampleComponent }, */
  setup() {
    return {}
  }
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
.ultra-small {
  font-size: 10px;
}
.img-size {
  max-width: 250px;
}
.floor-color {
  background: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.5)),
    url(../../public/rust.jpg);
  color: #ffffff;
}
</style>
