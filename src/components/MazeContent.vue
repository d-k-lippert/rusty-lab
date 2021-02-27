<template>
  <div class="page-content q-mt-md">
    <div>
      <game-progress :puzzlesSolved="puzzlesSolved"></game-progress>
      <iron-dialog :x="userX" :y="userY"></iron-dialog>
      <cobalt-dialog :x="userX" :y="userY"></cobalt-dialog>
      <nickel-dialog :x="userX" :y="userY"></nickel-dialog>
      <terbium-dialog :x="userX" :y="userY"></terbium-dialog>
      <dysprosium-dialog :x="userX" :y="userY"></dysprosium-dialog>
      <decision-dialog :x="userX" :y="userY"></decision-dialog>
      <entry-input></entry-input>

      <maze-grid :x="userX" :y="userY"> </maze-grid>
      <game-tips :puzzlesSolved="puzzlesSolved"></game-tips>
      <win-dialog
        :puzzlesSolved="puzzlesSolved"
        :timeNeeded="playTime"
      ></win-dialog>
      <q-btn
        size="lg"
        @click="triggerInstantWin"
        label="Instant Win"
        dense
        color="positive"
        class="q-ma-md q-pl-md q-pr-md"
      />
    </div>
    <!-- <div id="output"></div> -->
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from '@vue/composition-api'
import MazeGrid from 'components/MazeGrid.vue'
import GameProgress from 'components/GameProgress.vue'
import GameTips from 'components/GameTips.vue'
import IronDialog from 'components/Dialog/IronDialog.vue'
import CobaltDialog from 'components/Dialog/CobaltDialog.vue'
import NickelDialog from 'components/Dialog/NickelDialog.vue'
import TerbiumDialog from 'components/Dialog/TerbiumDialog.vue'
import DysprosiumDialog from 'components/Dialog/DysprosiumDialog.vue'
import EntryInput from 'components/EntryInput.vue'
import eventBus from 'src/event-bus/event-bus'
import { setInterval } from 'timers'
import DecisionDialog from 'components/Dialog/DecisionDialog.vue'
import WinDialog from 'components/Dialog/WinDialog.vue'

export default defineComponent({
  components: {
    MazeGrid,
    IronDialog,
    CobaltDialog,
    NickelDialog,
    TerbiumDialog,
    DysprosiumDialog,
    EntryInput,
    GameProgress,
    GameTips,
    DecisionDialog,
    WinDialog
  },
  name: 'CompositionComponent',

  setup() {
    const isConnected = ref(true)
    const userX = ref(5)
    const userY = ref(30)
    const playTime = ref(0)

    const puzzlesSolved = ref(0)

    let startTime = new Date()
    let endTime = new Date()

    userX.value = 2
    userY.value = 2

    const wsUri = 'ws://vrusty-server.herokuapp.com'
    /* const wsUri = 'ws://localhost:8080' */
    /* let output: HTMLElement | null */
    let webSocket: WebSocket

    // prevents double triggering off emitted event
    eventBus.$off('move-iron-cube')
    // listen to right answer triggered from iron modal in puzzle room 3
    eventBus.$on('move-iron-cube', () => {
      console.log('Move Iron Cube!')
      doSend('move iron')
    })

    // prevents double triggering off emitted event
    eventBus.$off('move-cobalt-cube')
    // listen to right answer triggered from iron modal in puzzle room 3
    eventBus.$on('move-cobalt-cube', () => {
      console.log('Move Cobalt Cube!')
      doSend('move cobalt')
    })

    // prevents double triggering off emitted event
    eventBus.$off('move-nickel-cube')
    // listen to right answer triggered from iron modal in puzzle room 3
    eventBus.$on('move-nickel-cube', () => {
      console.log('Move Nickel Cube!')
      doSend('move nickel')
    })

    // prevents double triggering off emitted event
    eventBus.$off('move-terbium-cube')
    // listen to right answer triggered from iron modal in puzzle room 3
    eventBus.$on('move-terbium-cube', () => {
      console.log('Move Terbium Cube!')
      doSend('move terbium')
    })

    // prevents double triggering off emitted event
    eventBus.$off('move-dysprosium-cube')
    // listen to right answer triggered from iron modal in puzzle room 3
    eventBus.$on('move-dysprosium-cube', () => {
      console.log('Move Dysprosium Cube!')
      doSend('move dysprosium')
    })

    // prevents double triggering off emitted event
    eventBus.$off('reset-player')
    // listen to wrong answer
    eventBus.$on('reset-player', () => {
      console.log('player got resetted!')
      doSend('reset player')
    })

    // prevents double triggering off emitted event
    eventBus.$off('open-shortcut')
    // listen to shortcut event
    eventBus.$on('open-shortcut', () => {
      console.log('player takes shortcut!')
      doSend('open shortcut door')
    })

    // prevents double triggering off emitted event
    eventBus.$off('open-win-message')
    // listen to shortcut event
    eventBus.$on('open-win-message', () => {
      endTime = new Date()

      const timeNeeded = Math.round(
        (endTime.getTime() - startTime.getTime()) / 60000
      )
      playTime.value = timeNeeded
      console.log(endTime.getTime())
      console.log('benötigte Zeit: in min', timeNeeded)

      console.log('player wins!')
      // doSend('open shortcut door')
    })

    // prevents double triggering off emitted event
    eventBus.$off('connect-server')
    //
    eventBus.$on('connect-server', () => {
      startTime = new Date()

      console.log(startTime.getTime())
      console.log('connected!')
      connectToServer()
    })

    function init() {
      /* output = document.getElementById('output') */
      testWebSocket()
    }
    function testWebSocket() {
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

    function onOpen(evt: any) {
      writeToScreen('connected from web')
      doSend('web')
      setInterval(keepConnectionOpen, 5000)
    }

    function keepConnectionOpen() {
      doSend('web client still there')
    }

    function onClose(evt: CloseEvent) {
      writeToScreen('DISCONNECTED')
      setTimeout(testWebSocket, 5000)
      writeToScreen('Reconnecting...')
    }

    function onMessage(evt: MessageEvent) {
      if (typeof evt.data === 'string') {
        // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
        /*  writeToScreen(
          '<span style="color: blue;">RESPONSE: ' + evt.data.substring(1, evt.data.length) + '</span>') */
        checkAndPassMessage(evt.data) // pass data on to Maze-Grid.vue component
      }
      /* console.log(evt.data) */
      // webSocket.close();
    }

    function onError(evt: Event) {
      // eslint-disable-next-line @typescript-eslint/restrict-plus-operands
      writeToScreen('<span style="color: red;">ERROR:</span> ' + evt)
    }

    function doSend(message: string) {
      /* writeToScreen('SENT: ' + message) */
      webSocket.send(message)
    }

    function writeToScreen(message: string) {
      /*       var pre = document.createElement('p')
      pre.style.wordWrap = 'break-word'
      pre.innerHTML = message
      if (output != null) {
        output.appendChild(pre)
      } */
    }

    function connectToServer() {
      init()
      isConnected.value = false
    }

    function sendToServer() {
      doSend('hit submit')
    }

    function triggerInstantWin() {
      puzzlesSolved.value = 3
    }

    function checkAndPassMessage(message: string) {
      if (message === 'tangramsolved') {
        puzzlesSolved.value = 1 // Display that first puzzle was solved
        /*         console.log(puzzlesSolved.value) */
      }
      if (message === 'schluchtsolved') {
        puzzlesSolved.value = 2 // Display that first puzzle was solved
        /*         console.log(puzzlesSolved.value) */
      }
      if (message === 'schiebesolved') {
        puzzlesSolved.value = 3 // Display that first puzzle was solved
        /*         console.log(puzzlesSolved.value) */
      }
      if (message.includes('X')) {
        userX.value = parseInt(message.substring(1, message.length)) // assign value to userX and pass it to child component to display it in lab
      }
      if (message.includes('Y')) {
        // check if message is a y-coordinate
        userY.value = parseInt(message.substring(1, message.length)) // assign value to userY and pass it to child component to display it in lab
      }
    }

    return {
      isConnected,
      connectToServer,
      sendToServer,
      userX,
      userY,
      puzzlesSolved,
      triggerInstantWin,
      playTime
    }
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
