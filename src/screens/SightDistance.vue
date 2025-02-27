<template>
  <table class="table table-borderless">
    <thead class="table">
      <tr>
      <td id="sightdistance" class="sectionHeader">&nbsp;&nbsp; 12 &nbsp; Sight Distance
      <span class="title-icon" @click=levelCollapse()>
        <span v-if="!levelDisplay">Expand All &nbsp;<i class="bi bi-caret-down-fill"></i></span>
        <span v-if="levelDisplay">Collapse All &nbsp;<i class="bi bi-caret-up-fill"></i></span>
      </span>
      </td>
      </tr>
    </thead>
    <tbody>
      <tr>
      <td scope="row">
      <Collapsible chapt="12.1" title="Stopping Sight Distance" :levelDisplay="levelDisplay">
      <!-- Display content of sub section 12.1 -->
        <p> The minimum stopping sight distance for various road gradient shall be determined by the following formula:</p>
          <div class="img-container2">
            <ZoomImage imgSrc="10.4.2.2.1.png"/>
          </div>
        <p style="font-size: 16px;"> Referenced from:
          <a href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=203" target='_blank'>
            CDC 10.4.2.2.1 - Stopping Sight Distance (page 203)</a>
        </p>
      </Collapsible>

      <Collapsible v-show="isUndivided" title="Intermediate Sight Distance" chapt="12.2" :levelDisplay="levelDisplay">
      <!-- Display content of sub section 12.2, v-show on top filters the content here, displaying it only if user chose undivided road -->
        <ol v-show="isUndivided" type="a">
        <li v-show="isUndivided"> Intermediate sight distance is equal to 2 times stopping sight distance. </li>
        <li v-show="isUndivided"> Intermediate sight distance is only applicable to undivided 2-lane road. </li>
        <li v-show="isUndivided"> Where intermediate sight distance is unachievable because of site constraint, 
        the stopping sight distance shall be used and the appropriate control measures to 
        prohibit overtaking shall be introduced.</li>
        </ol>
        <p v-show="isUndivided" style="font-size: 16px;"> Referenced from:
          <a v-show="isUndivided" href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=203" target='_blank'>
          CDC 10.4.2.2.2 - Intermediate Sight Distance (page 203)</a>
        </p>
      </Collapsible>

      <Collapsible v-show="isUndivided" chapt="12.3" title="Overtaking Sight Distance" :levelDisplay="levelDisplay">
      <!-- Display content of sub section 12.3 -->
        <p v-show="isUndivided">The following sight distances are to be considered in the design. If overtaking sight distance 
          for an undivided road cannot be achieved, the intermediate sight distance shall be adopted.</p>
        <p v-show="isUndivided"><u>Note:</u> Overtaking sight distance is only applicable to undivided 2-lane road.</p>
        <div class="img-container4">
          <img v-show="isUndivided" src="Table10.5.png"/>
        </div>  <br>
        <p v-show="isUndivided" style="font-size: 16px;"> Referenced from:
          <a v-show="isUndivided" href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=204" target='_blank'>
            CDC 10.4.2.2.3 - Overtaking Sight Distance (page 204)</a>
        </p>
      </Collapsible>

      <Collapsible chapt="12.4" title="Intersection Sight Distance" :levelDisplay="levelDisplay">
      <!-- Display content of sub section 12.4 -->
        <p>The desirable intersection sight distance at unsignalised junction can be derived 
          from the following formula and to be read in conjunction with Figure 10.2.</p>
        <div class="img-container2">
          <ZoomImage imgSrc="10.4.2.2.4.png"/>
        </div>
        <div class="img-container">
          <ZoomImage imgSrc="Figure10.2.png"/>
        </div>
        <p style="font-size: 16px;"> Referenced from:
          <a href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=204" target='_blank'>
            CDC 10.4.2.2.4 - Intersection Sight Distance (page 204)</a>,
          <a href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=226" target='_blank'>
            CDC Figure 10.2 (page 226)</a>
        </p>
      </Collapsible>

      <Collapsible chapt="12.5" title="Offset Distance" :levelDisplay="levelDisplay">
      <!-- Display content of sub section 12.5 -->
        <p>On a horizontal curve where the obstruction on the inside of the curve cannot be removed, 
          offset distance to the obstruction shall be provided. 
          The offset distance can be derived from the following formula and shall be read in conjunction with Figure 10.3.</p>
        <div class="img-container2">
          <ZoomImage imgSrc="10.4.2.2.5.png"/>
        </div>
        <div class="img-container">
          <ZoomImage imgSrc="Figure10.3.png"/>
        </div>
        <p style="font-size: 16px;"> Referenced from:
          <a href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=205" target='_blank'>
            CDC 10.4.2.2.5 - Sight Distance on Horizontal Curve (page 205)</a>,
          <a href="https://www.lta.gov.sg/content/dam/ltagov/industry_innovations/industry_matters/development_construction_resources/civil_standards/pdf/EGD09106A2_Overall.pdf#page=227" target='_blank'>
            CDC Figure 10.3 (page 226)</a>
        </p>
      </Collapsible>
      </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
/** Collapsible to expand and collapse the sub-sections */
import Collapsible from '../components/Collapsible.vue';
/** ZoomImage to zoom onto the image */
import ZoomImage from '../components/ZoomImage.vue'

export default {
  name:'SightDistance',
  components: {
    Collapsible,
    ZoomImage
  },
  data(){
    return{
      choice:{
        role: "",
        roadDesign: "",
        roadClass: "",
        roadType: "",
        designSpeed: "",
        grad_curv_change:"",
        specific_param:"",
      },
      /*isUndivided checks if the exisitng user's road Type selected is undivided Road or not, and returns True or False respectively*/
      isUndivided: this.$parent.choice.roadType === 'undividedRoad' ? true : false,
      levelDisplay: false
    }
  },
  methods:{
    openStorage(){
      return JSON.parse(localStorage.getItem('choice'))
    },
    levelCollapse: function() {
      this.levelDisplay = !this.levelDisplay;
    },
  },
  mounted(){
    const storedChoice = this.openStorage()
    if (storedChoice){
      this.choice = {
        ...this.choice,
        ...storedChoice
      }
    }
    console.log("SightDistance: " + this.isUndivided)
  }
}
</script>


<style scoped>
table {
  width: 65vw;
  height: auto;
  margin-top: 5vh;
  border-radius: 15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.1);
  z-index: 999;
}
.table thead td {
  background-color: #273B8C;
  color: white;
  height: 7.25vh;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  font-size:22px;
  vertical-align: middle;
}
tbody tr{
  background-color: #ffffff;
}
tbody tr:last-child td{ 
  border-bottom-right-radius: 15px;
  border-bottom-left-radius: 15px; 
  padding-bottom: 2%;
}
.sectionHeader {
  display: flex;
  width: auto;
  justify-content: space-between;
  align-items: center;
}
.title-icon {
  font-size:0.95rem;
  color:lavender;
  cursor:pointer;
  padding: 0 1rem 0 1.5rem;
  border-left: inset;
  border-color: lightblue
}
li {
  padding-left:0.5rem;
  margin: 10px 0
}
</style>
