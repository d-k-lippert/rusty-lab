<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="fence"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title> Die Kunst des Reparierens </q-toolbar-title>
      </q-toolbar>
      <q-img src="../../public/rust.jpg" class="bg-img absolute-top"> </q-img>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label header class="text-grey-8"> Menü </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import EssentialLink from 'components/EssentialLink.vue'

const linksData = [
  {
    title: 'Was ist die Kunst des Reparierens?',
    caption: '/',
    icon: 'help',
    link: '#/',
    target: '_self'
  },
 /*  {
    title: 'Spiel-Anleitung',
    caption: '/anleitung',
    icon: 'description',
    link: '#/anleitung',
    target: '_self'
  }, */
  {
    title: 'Reparatur-Handbuch',
    caption: '/game-doc',
    icon: 'receipt_long',
    link: 'documents/Reparatur-Handbuch.pdf',
    target: '_blank'
  },
  {
    title: 'Eagle Eye',
    caption: '/game',
    icon: 'sports_esports',
    link: '#/game',
    target: '_self'
  }
  /* {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  } */
]

import { defineComponent, ref } from '@vue/composition-api'

export default defineComponent({
  name: 'MainLayout',
  data() {
    return { metaTitle: '' }
  },
  meta() {
    return {
      titleTemplate: (title: string) => `${title} - Die Kunst des Reparierens`
    }
  },
  components: { EssentialLink },
  setup() {
    const leftDrawerOpen = ref(false)
    const essentialLinks = ref(linksData)

    return { leftDrawerOpen, essentialLinks }
  }
})
</script>
<style scoped>
.bg-img {
  height: 100%;
  z-index: -1;
  filter: brightness(50%);
}
</style>
