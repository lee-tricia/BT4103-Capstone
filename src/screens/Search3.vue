<template>
  <div style="height:100vh; overflow: hidden; position:relative">
  <div class="header">
    <div class="center">
    <div class="pages">
        <PageCircle num="1" v-bind:isActive="true" @click="$router.push('search')"/>
        <PageCircle num="2" v-bind:isActive="true" @click="$router.push('search2')"/>
        <PageCircle num="3" v-bind:isActive="true"/>
        <PageCircle num="4" v-bind:isActive="false"/>
        <PageCircle num="5" v-bind:isActive="false"/>
    </div>
    <div class="question">
      <h5>Are you working on <u>Undivided (x-lane) Road</u>, <u>Slip Road</u> or <u>Dual (x-lane) Road</u>? Please select below.
      
      <span tabindex="0" data-bs-toggle="tooltip" data-bs-placement="bottom" data-bs-html="true"
      title="
        <u><b>Undivided (x-lane) Road</b>:</u> <br>Bi-directional road with no physical separator/ divider with x-lane in total <p></p>
        <u><b>Slip Road</b>:</u> <br>Connecting road to allow vehicles to enter or exit the interconnecting carriageway and to bypass the intersection at-grade <p></p>
        <u><b>Dual (x-lane) Road</b>:</u> <br>Two directional road (x-lane in each direction) with a physical separator as a central divider (or) median
      ">
        <i class="bi bi-info-circle" id="info" style="font-size: 1rem; padding-left:0.25rem"></i>
      </span>
      
      </h5>
    </div>
    </div>
    <img src="../assets/mascot.png" class="mascot"/>
    <img src="../assets/road.png" class="road"/>
  </div>
  <div class="options">
    <div class="button-group">
      <SearchParamButton text="Undivided (x-lane) Road" v-bind:isActive="true" @click="storeRoadType('undividedRoad');"/>
      <SearchParamButton text="Slip Road" v-bind:isActive="true" @click="storeRoadType('slipRoad');"/>
      <SearchParamButton text="Dual (x-lane) Road" v-bind:isActive="true" @click="storeRoadType('dualRoad');"/>
    </div>
    <button id="back" type="button" class="btn btn-outline-secondary" @click="$router.push('search2')">
      <i class="bi bi-arrow-left"></i>
    </button>
  </div>
  </div>
</template>

<script>
import SearchParamButton from '../components/SearchParamButton.vue'
import PageCircle from '../components/PageCircle.vue'
import { Tooltip } from 'bootstrap/dist/js/bootstrap.esm.min.js'

export default {
  name: 'search3',
  props: ['roadDesign','roadClass'],
  components: {
    PageCircle,
    SearchParamButton
  },
  data() {
    return{
      roadType: '',
    }
  },
  methods:{
    openStorage() {
      return JSON.parse(localStorage.getItem('choice'))
    },
    saveStorage(form) {
      localStorage.setItem('choice',JSON.stringify(form))
    },
    updateChoice(input,value) {
      this.choice[input] = value

      let storedChoice = this.openStorage()
      if(!storedChoice) storedChoice = {}

      storedChoice[input] = value
      this.saveStorage(storedChoice)
    },
    storeRoadType(text) {
      this.updateChoice('roadType',text)
      this.displayRoadType();
      this.$router.push({name:'search4'})
    },
    displayRoadType() {
      console.log(this.choice.role)
      console.log(this.choice.roadDesign)
      console.log(this.choice.roadClass)
      console.log(this.choice.roadType)
    },
  },
  created() {
    const storedChoice = this.openStorage()
    if (storedChoice){
      this.choice = {
        ...this.choice,
        ...storedChoice
      }
    }
  },
  mounted() {
    var tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'))
    tooltipTriggerList.map(function (tooltipTriggerEl) {
      return new Tooltip(tooltipTriggerEl)
    })
  }
}
</script>

<style scoped>
#back {
  position:absolute;
  width:fit-content;
  height:fit-content;
  font-size: 1.5rem;
  top:85%;
  left:5%;
  box-shadow:none;
  border:none;
}
.button-group {
  display: flex;
  justify-content: space-around;
  width: 75%
}
.options {
  background-color: #FAFAFA;
  height: 55%;
  align-items: center;
  padding-top:5%;
  display: flex;
  justify-content: space-around;
}
.header {
  background-color: #E0E0E0;
  height: 45%;
}
.center {
  display:flex;
  align-items: center;
  flex-direction: column;
}
.road {
  height:19vh;
  width:102vw;
  transform: rotate(-2deg);
  position: absolute;
  top: 40%;
  left: -0.5%;
  z-index:1;
}
.mascot {
  height: 20vh;
  width: auto;
  position: absolute;
  top: 30%;
  left: 22.5%;
  z-index:2;
}
.question {
  background-color:white;
  height: fit-content;
  width:35%;
  padding: 1.25rem 2rem;
  border-radius:1.5rem
}
.pages {
  display: flex;
  margin: 3% 0
}
</style>
