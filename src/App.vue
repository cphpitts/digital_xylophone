<template>
  <div id="app" class="h-100">
    <HeaderNav />
    <div class="container xylophone h-75">
      <div class="row h-100">
        <!-- Loops through array of xylophone keys and generates a div -->
        <div v-for="item  in xylophoneKeys" :key="item.note" class="col h-100 px-4" >
          <Sound :note="item.note" :color="item.color" :height="item.height" :trigger="item.triggerKey" />
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import HeaderNav from './components/HeaderNav.vue'
import Sound from './components/Sound.vue'
import { EventBus } from './event-bus.js';
// import Tone from 'tone'

export default {
  name: 'App',
  components: {
    Sound,
    HeaderNav
  },

  mounted() {
    var fired = false;
    window.addEventListener('keydown', e => {
      if (!fired) {
        EventBus.$emit('keyPressed', String.fromCharCode(e.keyCode));
        fired = true;
      }
    },
    window.addEventListener('keyup', function() {
      fired = false
    })
  )},
  data: function() {
    return {
      keyStep: 15,
      xylophoneKeys: [
        {note: "C4", color: "red", height: "100%", triggerKey: "A" },
        {note: "D4", color: "orange", height: "93%", triggerKey: "S"  },
        {note: "E4", color: "yellow", height: "84%", triggerKey: "D"  },
        {note: "F4", color: "green", height: "77%", triggerKey: "F"  },
        {note: "G4", color: "blue", height: "70%", triggerKey: "G"  },
        {note: "A4", color: "indigo", height: "63%", triggerKey: "H"  },
        {note: "B4", color: "violet", height: "56%", triggerKey: "J"  },
        {note: "C5", color: "red", height: "49%", triggerKey: "K"  }
      ]
    }
  }
}
</script>

<style>

html, body {
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}

</style>
