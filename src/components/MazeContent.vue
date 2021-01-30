<template>
  <div class="page-content q-mt-md">
    <div>
      <maze-grid :x="userX" :y="userY" > </maze-grid>
      <div class="row justify-center">
        <q-btn
          v-if="isConnected"
          @click="connectToServer"
          class="floor-color"
          text-color="white"
          label="connect to server"
        >
        </q-btn>
<!--         <q-btn
          @click="sendToServer"
          color="secondary"
          label="send to websocket server"
          disable
        >
        </q-btn> -->
        <q-toggle
          label="eisen"
          v-model="eisenVal"
          color="green"
        />
        <q-toggle
          label="cobalt"
          v-model="cobaltVal"
          color="red"
        />
        <q-toggle
          label="nickel"
          v-model="nickelVal"
          color="blue"
        />
        <q-toggle
          label="terbium"
          v-model="terbiumVal"
          color="secondary"
        />
        <q-toggle
          label="dysprosium"
          v-model="dysprosiumVal"
          color="tertiary"
        />
      </div>
    </div>
    <div id="output"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@vue/composition-api'
import MazeGrid from 'components/MazeGrid.vue'

export default defineComponent({
  components: { MazeGrid },
  name: 'CompositionComponent',

  setup () {
    const isConnected = ref(true)
    const userX = ref(5)
    const userY = ref(30)

    const eisenVal = ref(false)
    const cobaltVal = ref(false)
    const nickelVal = ref(false)
    const terbiumVal = ref(false)
    const dysprosiumVal = ref(false)

    userX.value = 2
    userY.value = 2

    watch(eisenVal, (newValue, oldValue) => {
      console.log('The new counter value is: ', eisenVal.value)
      if (eisenVal.value === true) {
        doSend('move eisen')
      }
    })
    watch(cobaltVal, (newValue, oldValue) => {
      console.log('The new counter value is: ', cobaltVal.value)
      if (cobaltVal.value === true) {
        doSend('move cobalt')
      }
    })
    watch(nickelVal, (newValue, oldValue) => {
      console.log('The new counter value is: ', nickelVal.value)
      if (nickelVal.value === true) {
        doSend('move nickel')
      }
    })
    watch(terbiumVal, (newValue, oldValue) => {
      console.log('The new counter value is: ', terbiumVal.value)
      if (terbiumVal.value === true) {
        doSend('move terbium')
      }
    })
    watch(dysprosiumVal, (newValue, oldValue) => {
      console.log('The new counter value is: ', dysprosiumVal.value)
      if (dysprosiumVal.value === true) {
        doSend('move dysprosium')
      }
    })
    
    // const wsUri = 'ws://http://vrusty-server.herokuapp.com'
    const wsUri = 'ws://localhost:8080'
    let output: HTMLElement | null
    let webSocket: WebSocket

    function init () {
      output = document.getElementById('output')
      testWebSocket()
    }
    function testWebSocket () {
      webSocket = new WebSocket(wsUri)
      webSocket.onopen = function (evt) {
        onOpen(evt)
      }
      webSocket.onclose = function (evt) {
        onClose(evt)
      }
      webSocket.onmessage = function (evt) {
        onMessage(evt)
      }
      webSocket.onerror = function (evt) {
        onError(evt)
      }
    }

    function onOpen (evt: any) {
      writeToScreen('connected from web')
      doSend('web')
    }

    function onClose (evt: CloseEvent) {
      writeToScreen('DISCONNECTED')
    }

    function onMessage (evt: MessageEvent) {
      if (typeof evt.data === 'string') {
      // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
        writeToScreen(
          '<span style="color: blue;">RESPONSE: ' + evt.data.substring(1, evt.data.length) + '</span>')
        checkAndPassMessage(evt.data) // pass data on to Maze-Grid.vue component
      }
      console.log(evt.data)
      // webSocket.close();
    }

    function onError (evt: Event) {
      // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
      writeToScreen('<span style="color: red;">ERROR:</span> ' + evt)
    }

    function doSend (message: string) {
      writeToScreen('SENT: ' + message)
      webSocket.send(message)
    }

    function writeToScreen (message: string) {
      var pre = document.createElement('p')
      pre.style.wordWrap = 'break-word'
      pre.innerHTML = message
      if (output != null) {
        output.appendChild(pre)
      }
    }

    function connectToServer () {
      init()
      isConnected.value = false
    }

    function sendToServer () {
      doSend('hit submit')
    }

    function checkAndPassMessage (message: string) {
      if (message.includes('X')) {
        userX.value = parseInt(message.substring(1, message.length)) // assign value to userX and pass it to child component to display it in lab
      }
      if (message.includes('Y')) {
        // check if message is a y-coordinate
        userY.value = parseInt(message.substring(1, message.length)) // assign value to userY and pass it to child component to display it in lab
      }
    }

    return { isConnected, connectToServer, sendToServer, userX, userY, eisenVal, cobaltVal, nickelVal, terbiumVal, dysprosiumVal }
  }
})
</script>
<style scoped>
.page-content {
  width: 70%;
}
.floor-color {
  background: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.5)),
    url(../../public/rust.jpg);
}
</style>
