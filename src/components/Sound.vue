<template lang="html">
  <div class="h-100">
    <div v-on:click="playSound" v-bind:style="{ backgroundColor: color, height: height }" class="xylophoneKey">
      <div class="xylophoneRivet"></div>
      <div class="xylophoneNote">
        {{ note }}<br/>
        <span class="xlyophoneKey">({{ trigger }})</span>
      </div>
      <div class="xylophoneRivet bottomRivet"></div>
    </div>
  </div>
</template>

<script>
import { FMSynth } from 'tone'
import { EventBus } from '../event-bus.js'

export default {
  props: ['note', 'color', 'height', 'trigger'],

  // Listens for keyPressed event. Calls checkKey function
  created: function() {
    EventBus.$on('keyPressed', this.checkKey)

  },
  methods: {
    // plays the appropriate sound
    playSound: function() {
      this.xylophone = new FMSynth(
        {
          "harmonicity":8,
          "modulationIndex": 2,
          "oscillator" : {
              "type": "sine"
          },
          "envelope": {
              "attack": 0.001,
              "decay": 2,
              "sustain": 0.1,
              "release": 2
          },
          "modulation" : {
              "type" : "square"
          },
          "modulationEnvelope" : {
              "attack": 0.002,
              "decay": 0.2,
              "sustain": 0,
              "release": 0.2
          }
        }
      ).toDestination();
    this.xylophone.triggerAttackRelease(this.note,"8n")
  },
    // triggered by keyPressed custom event. If the pressed key matches triggerKey value, calls the playSound function
    checkKey: function(keyPressed) {
      if (keyPressed == this.trigger) {
        this.playSound()
      }
    }
  },
  data: function() {
    return {
      keyHeight: 100 - 15 * this.height
    }
  }
}



</script>

<style lang="css" scoped >
.xylophoneKey {
  position: relative;
}

.xylophoneNote {
    color: #3c3c3c;
    background-color: rgba(255, 255, 255, 0.5);
    width: 72%;
    margin: 77px auto;
    font-size: 3em;
    font-family: monospace;
    font-weight: bold;
    line-height: 1em;
    padding: 8%;
    display: inline-block;
}

.xylophoneNote .xlyophoneKey {
    font-size: 0.5em;
    font-weight: normal;
}

.xylophoneRivet {
  background-color: white;
  width: 30%;
  position: absolute;
  top: 26px;
  left: 50%;
  border-radius: 100%;
  margin-left: -15%;
  display: block;
}

.bottomRivet {
  top: initial;
  bottom: 26px;
}

.xylophoneRivet:after {content: "";display: block;padding-bottom: 100%;}
</style>
