<template>
  <div class="page-content q-mt-md">
    <div>
      <maze-grid> </maze-grid>
      <div class="row justify-center">
        <q-btn
          v-if="isConnected"
          @click="connectToServer"
          class="floor-color"
          text-color="white"
          label="Tür öffnen"
        >
        </q-btn>
        <!-- <q-btn
          @click="sendToServer"
          color="secondary"
          label="send to websocket server"
        >
        </q-btn> -->
      </div>
    </div>
    <div id="output"></div>
    <!--     <p>
      {{ isTriggering }}
    </p> -->
    <!-- <q-badge
      v-if="!isTriggering"
      color="orange"
      text-color="black"
      label="hide me with trigger"
    /> -->
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from '@vue/composition-api'
import MazeGrid from 'components/MazeGrid.vue'

export default defineComponent({
  components: { MazeGrid },
  name: 'CompositionComponent',

  setup () {
    const isConnected = ref(true)

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
      writeToScreen("connected from web")
      doSend("web")
    }

    function onClose (evt: CloseEvent) {
      writeToScreen("DISCONNECTED")
    }

    function onMessage (evt: MessageEvent) {
      // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
      writeToScreen('<span style="color: blue;">RESPONSE: ' + evt.data + '</span>')
      // webSocket.close();
    }

    function onError (evt: Event) {
      // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
      writeToScreen('<span style="color: red;">ERROR:</span> ' + evt)
    }

    function doSend (message: string) {
      writeToScreen("SENT: " + message)
      webSocket.send(message)
    }

    function writeToScreen (message: string) {
      var pre = document.createElement("p")
      pre.style.wordWrap = "break-word"
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
      doSend("hit submit")
    }

    return { isConnected, connectToServer, sendToServer }
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
