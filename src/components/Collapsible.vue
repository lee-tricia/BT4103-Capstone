<template>
    <div class="content">
      <div class="title" @click="collapse()">
        <div class="collapseTitle-text">
          <b style="grid-column:1; grid-row:1;">{{chapt}}</b><b style="grid-column:2; grid-row:1;">{{title}}</b>
        </div>
        <div class="title-icon">
          <span v-if="!(displayInfo)"><font-awesome-icon icon="angle-down" id="arrow"/></span>
          <span v-if="displayInfo"><font-awesome-icon icon="angle-up" id="arrow"/></span>
        </div>
      </div>
      <div class="information" v-show="displayInfo" style="font-size: 20px; margin-top: 1%;">
        <!-- content encased in this component will be slotted here -->
        <slot/>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      displayInfo: false
    }
  },
  props: {
    title: String,
    chapt: String,
    levelDisplay: Boolean
  },
  methods:{
    collapse: function() {
      //click to toggle between v-if = true or false
      this.displayInfo = !this.displayInfo;
    },
  },
  watch: {
    levelDisplay: function (val) {
      this.displayInfo = val
    },
  }
}
</script>

<style>
.content{
  font-size:18px;
  margin: 2% 10%;
  text-align: justify;
  padding-bottom:1%;
}
.title {
  cursor: pointer;
  display: flex;
  margin-top: 3%;
  padding: 1% 0;
  justify-content: space-between;
}
.collapseTitle-text {
  display: grid;
  align-items: center;
  font-size: 20px;
  grid-template-columns: 5rem auto;
}
.image {
  display: flex;
  justify-content:center;
  width:80%;
  margin-left: 3em; 
}
img {
    width: 100%;
}

p {
  font-size:20px;
}
.tab1 {
 margin-right: 2.5em
}
.tab2 {
 margin-right: 1.7em
}

.tab2a {
  margin-right:1.25em
}
.tab3 {
  margin-right: 1em
}
.tab4 {
  margin-right:0.2em;
}
.tab5 {
  margin-right: 1.2em
}
.img-container2{
  width: 50%;
  height: auto;
  margin-left: auto;
  margin-right: auto;
  margin-top: 3%;
  margin-bottom:3%;
}
.img-container2 img{
  width: 100%;
  height: auto;
}
.img-container4{
  width: 80%;
  height: auto;
  margin-left: 3em; 
}
.img-container4 img{
  width: 100%;
  height: auto;
}
</style>