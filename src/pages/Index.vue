<template>
  <q-page class="row justify-evenly">
    <div class="page-content">
      <h2>Index</h2>
    </div>
    <example-component> </example-component>
  </q-page>
</template>

<script lang="ts">
import ExampleComponent from '../components/CompositionComponent.vue'
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
  components: { ExampleComponent },
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
</style>
