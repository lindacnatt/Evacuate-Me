<template>
  <div class="time">
    <div class="infotext">Time is relative...</div>
    <div class="content">
      <!-- Inspiration from https://codepen.io/willpaige/pen/ImjGq -->
      <div class="planet-container">
        <div :style="{ animationDuration: daySlider + 's'}" class="planets sun">
          <div class="one ring"></div>
          <div
            :style="{ animationDuration: hourSlider + 's', background: planetColor}"
            class="planet"
          >
            <div class="ring"></div>
            <div class="moon"></div>
          </div>
        </div>
      </div>

      <v-app id="slider">
        <v-container>
          <v-subheader class="header">Hours a day</v-subheader>
          <v-layout row wrap>
            <div class="slider-container">
              <v-flex xs1>
                <i class="fas fa-minus"></i>
              </v-flex>
              <v-flex>
                <v-slider
                  v-model="hourSlider"
                  ticks="always"
                  tick-size="3"
                  :max="10"
                  :min="1"
                  :step="1"
                  :color="ex1.color"
                  :track-color="ex2.color"
                  :thumb-color="ex3.color"
                  @click="setHours()"
                ></v-slider>
              </v-flex>
              <v-flex xs1>
                <i class="fas fa-plus"></i>
              </v-flex>
            </div>
          </v-layout>
          <v-subheader class="header">Days a year</v-subheader>
          <v-layout row wrap>
            <div class="slider-container">
              <v-flex xs1>
                <i class="fas fa-minus"></i>
              </v-flex>
              <v-flex>
                <v-slider
                  v-model="daySlider"
                  ticks="always"
                  tick-size="3"
                  :max="10"
                  :min="1"
                  :step="1"
                  :color="ex1.color"
                  :track-color="ex2.color"
                  :thumb-color="ex3.color"
                  @click="setDays()"
                ></v-slider>
              </v-flex>
              <v-flex xs1>
                <i class="fas fa-plus"></i>
              </v-flex>
            </div>
          </v-layout>
          <v-btn class="nextButton" @click="$router.push('/result')">Done</v-btn>
        </v-container>
      </v-app>
    </div>
  </div>
</template>

<script>
export default {
  name: "Time",
  data() {
    return {
      daySlider: 5,
      hourSlider: 5,
      planetColor: this.$store.state.chosenPlanetColor,
      ex1: { label: "color", val: 25, color: "#c91e00" },
      ex2: { label: "track-color", val: 75, color: "#FFFFFF" },
      ex3: { label: "thumb-color", val: 50, color: "#c91e00" }
    };
  },
  mounted: function() {
    this.$store.state.currentStep = 4;
  },
  methods: {
    setDays: function() {
      this.$store.commit("setChosenOrbitalPeriod", this.daySlider);
    },
    setHours: function() {
      this.$store.commit("setChosenRotationPeriod", this.hourSlider);
    }
  }
};
</script>


<style scoped>
.content {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
}

.slider-container {
  display: flex;
  flex-direction: row;
  align-items: baseline;
}

.slider-container > * {
  margin-right: 10px;
}

.container {
  max-height: 150px;
  max-width: 300px;
  margin-top: 40px;
  margin-bottom: 80px;
}
#slider {
  display: flex;
  justify-content: center;
  margin-left: 10%;
  margin-right: 10%;
  background: transparent;
  color: white !important;
}
.planets div {
  display: inline-block;
  position: absolute;
}
.header {
  font-family: "Roboto Mono", monospace;
  color: white;
}
.ring {
  border: 2px solid rgba(255, 255, 255, 0.5);
  transform: rotate(0);
  box-shadow: none;
}
.one {
  width: 300px;
  height: 300px;
  border-radius: 200px;
  left: -110px;
  top: -110px;
}
.planet {
  width: 52px;
  height: 52px;
  border-radius: 50px;
  background: #ffacac;
  top: 16px;
  left: -132px;
  transform-origin: 26px 26px;
}
.planet > .ring {
  width: 120px;
  height: 120px;
  border-radius: 120px;
  top: -35px;
  left: -35px;
}
.planet-container {
  position: relative;
  width: 540px;
  margin-top: 70px;
  text-align: center;
  height: 450px;
}
.sun {
  width: 80px;
  height: 80px;
  border-radius: 80px;
  top: 170px;
  left: 240px;
  display: inline-block;
  position: absolute;
  background: #f1da36;
  box-shadow: 0 0 50px #f1da36, 0 0 20px #f2ad00, 0 0 5px #c96800,
    0 0 70px #feff8f;
}
.sun {
  animation-name: spin;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
}
.planet {
  animation-name: spin;
  animation-duration: 10s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  box-shadow: 0 0 30px #e8bcbcc2;
}
.moon {
  width: 30px;
  height: 30px;
  border-radius: 50px;
  background: #fff;
  top: -30px;
  left: -30px;
  transform-origin: 15px 15px;
  box-shadow: 0 0 20px #eeede5ec, 0 0 5px #bae6ebe3;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>