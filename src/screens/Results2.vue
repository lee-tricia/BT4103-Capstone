<template>
  <div class="result">
    <div class="contents">
    <h2 style="padding-top:2rem; width:65vw">Results</h2>
    <div id="roadcselements">
      <RoadCSElem/>
    </div>
    <div id="grade">
      <Grade/>
    </div>
    <div id="longfrictionfactor">
      <LongFrictFactor/>
    </div>
    <div id="sidefrictionfactor">
      <SideFrictFactor/>
    </div>
    <div id="crossfall">
      <Crossfall/>
    </div>
    <div id="cornerradius">
      <CornerRadius/>
    </div>
    <div id="mergingangle">
      <MergingAngle/>
    </div>
    <div id="lanewidth">
      <LaneWidth/>
    </div>
    <div id="signs" style="margin-bottom: 5%;">
      <Signs/>
    </div>
    </div>
    <div class="pages">
      <PageCircle2 num="1" v-bind:isActive="true"/>
      <PageCircle2 num="2" v-bind:isActive="false" @click="level3"/>
      <PageCircle2 num="3" v-bind:isActive="false" @click="level4"/>
      <PageCircle2 num="4" v-bind:isActive="false" @click="level5"/>
    </div>
    <button id="back" type="button" class="btn btn-outline-secondary" @click="back">
    <i class="bi bi-arrow-left"></i><span>Back to Search</span>
    </button>
    <div class="imageStack">
    <div id="bottomImg">
    <img :src="road" class="road" />
    </div>
    <div id="topImg">
    <img :src="mascot" class="mascot" />
    </div>
  </div>
  </div>
</template>

<script>
import RoadCSElem from "./RoadCross-SectionsElements.vue"
import Grade from "./Grade.vue"
import LongFrictFactor from "./LongitudinalFrictionFactor.vue"
import SideFrictFactor from "./SideFrictionFactor.vue"
import Crossfall from "./Crossfall.vue"
import CornerRadius from "./CornerRadius.vue"
import MergingAngle from "./MergingAngle.vue"
import LaneWidth from "./LaneWidth.vue"
import Signs from "./Signs.vue"
import PageCircle2 from '../components/PageCircle2.vue'

export default {
  name: "Results2",
  components: {
    "RoadCSElem": RoadCSElem,
    "Grade": Grade,
    "LongFrictFactor": LongFrictFactor,
    "SideFrictFactor": SideFrictFactor,
    "Crossfall": Crossfall,
    "CornerRadius": CornerRadius,
    "MergingAngle": MergingAngle,
    "LaneWidth": LaneWidth,
    "Signs" : Signs,
    "PageCircle2": PageCircle2,
  },
  methods: {
    level3() {
      this.$router.push({path: "/results/page2"})
    },
    level4() {
      this.$router.push({path: "/results/page3"})
    },
    level5() {
      this.$router.push({path: "/results/page4"})
    },
    openStorage(){
      return JSON.parse(localStorage.getItem('choice'))
    },
    back(){
      return this.$router.push({path:"/search5"})
    },
    observeSections() {
      if (this.headerObserver != null) {
        try {
          this.headerObserver.disconnect()
        } catch (e) {console.log(e)}
      }
      this.headerObserver = new IntersectionObserver(this.headerObserverHandler, {
        //observe this area of the webpage
        rootMargin: "-20.4% 0% -72.4%"
      })
      const sections = document.querySelectorAll('.sectionHeader')
      sections.forEach(section => {
        //add "marker" to each section
        this.headerObserver.observe(section)
      })
    },
    headerObserverHandler (entries) {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          //if "marker" intersects the area that is observed, update the current section to be highlighted
          this.$emit('sec-change', entry.target.id)
        }
      }
    }
  },
  created(){
    const storedChoice = this.openStorage()
    if (storedChoice){
      this.choice = {
        ...this.choice,
        ...storedChoice
      }
    }
  },
  data() {
    return {
      headerObserver: null,
      road: require("../assets/road.png"),
      mascot: require("../assets/mascot.png")
    };
  },
  mounted() {
    this.observeSections()
  },
  props: {
    currSection: String
  }
};
</script>

<style scoped>
@import url(https://fonts.googleapis.com/css?family=Roboto);

* {
  margin: 0;
  padding: 0;
  font-family: "Roboto", sans-serif;
}
.pages {
  display: flex;
  justify-content: center;
}
#back {
  font-size: 1rem;
  box-shadow:none;
  border:none;
  margin: 1% 5% 2.5%;
  padding:0.4% 0.8%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  width:15%
}
.imageStack{
  display: grid;
  position: relative;
}

/** road image */
.road {
  max-width: 100%;
  width:100%;
  position: relative;
  bottom: 0;
  z-index: 1;
}
/** lta mascot */
.mascot {
  max-width: 16%;
  position: absolute;
  right: 4%;
  transform: rotateY(180deg);
  z-index: 2;
  bottom:30%
}
.result {
  float: right;
  width: 75%;
  background: #e0e0e0;
  position: relative;
}
.contents {
  margin-left:5vw;
}
</style>