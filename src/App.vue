<template>
  <v-app>
    <div class="banner d-none" v-bind:class="{'smallBanner': (e1 > 1 && animateBanner), 'd-block' : !$vuetify.breakpoint.mobile}"></div>
    <div class="banner-mobile d-none" v-bind:class="{'d-block' : $vuetify.breakpoint.mobile}">
      <MainSearch v-bind:step="parseInt(e1)" v-bind:mobile="true" style="position: relative; bottom: 15px;"/>
    </div>
    <v-container class="max-width">
        <!-- MAIN SEARCH -->
        <MainSearch v-if="!$vuetify.breakpoint.mobile" v-bind:step="parseInt(e1)" v-bind:mobile="false"/>
        <!-- BACK BUTTON -->
        <v-row v-if="!$vuetify.breakpoint.mobile" v-bind:class="{'show': (e1 > 1)}" class="hide-footer" style="height: 60px;">
          <v-col cols=12>
            <v-btn 
              @click="e1--; resetTitle()" 
              style="height: 25px; width: 25px;"
              class="bg-mainGreen"
              icon outlined fab elevation="2"
              >
              <v-icon
                color="white"
              >
                mdi-chevron-left
              </v-icon>
            </v-btn>
          </v-col>
        </v-row>
        <!-- STEPPER -->
        <v-stepper v-model="e1" :vertical="$vuetify.breakpoint.mobile" :class="{'no-transition' : !animateSteps}">
          <v-stepper-header id="stepper_header" >
            <div :class="$vuetify.breakpoint.mobile ? 'horizontal-scroll-mobile' : 'horizontal-scroll' ">
              <v-stepper-step
                :id="'step1'"
                :complete="e1 > 1"
                step="1"
                :editable="e1 > 1"
                class="first-step"
                @click="resetTitle(1)"
              >
                {{truncateString(vehicle)}}
              </v-stepper-step>

              <v-divider v-if="!$vuetify.breakpoint.mobile"></v-divider>

              <v-stepper-step
                :id="'step2'"
                :complete="e1 > 2"
                step="2"
                :editable="e1 > 2"
                @click="resetTitle(2)"
              >
                {{truncateString(brand)}}
              </v-stepper-step>

              <v-divider v-if="!$vuetify.breakpoint.mobile"></v-divider>

              <v-stepper-step 
                :id="'step3'"
                step="3" 
                :complete="e1 > 3"
                :editable="e1 > 3"
                @click="resetTitle(3)"
              >
                {{truncateString(model)}}
              </v-stepper-step>

              <v-divider v-if="!$vuetify.breakpoint.mobile"></v-divider>

              <v-stepper-step
                :id="'step4'" 
                step="4" 
                :complete="e1 > 4"
                :editable="e1 > 4"
                class="last-step"
                @click="resetTitle(4)"
                >
                {{truncateString(type)}}
              </v-stepper-step>
            </div>
          </v-stepper-header>

          <v-stepper-items id="main-buttons">
            <v-stepper-content step="1" style="padding: 0 !important;">
              <v-container>
                <v-row v-if="!$vuetify.breakpoint.mobile" justify="space-between">
                  <v-col cols=3>
                    <button
                      @click="e1 = 2; vehicle = 'Cars'"
                      @mouseenter="carImg = carImg + '_hover'"
                      @mouseleave="carImg = 'cars'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${carImg}.svg`)" alt="">
                    </button>
                  </v-col>
                  
                  <v-col cols=3>
                    <button
                      @click="e1 = 2; vehicle = 'Light Vehicles'"
                      @mouseenter="lwkImg = lwkImg + '_hover'"
                      @mouseleave="lwkImg = 'lwk'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${lwkImg}.svg`)" alt="">
                    </button>
                  </v-col>

                  <v-col cols=3>
                    <button
                      @click="e1 = 2; vehicle = 'Trucks & Bus'"
                      @mouseenter="truckImg = truckImg + '_hover'"
                      @mouseleave="truckImg = 'trucks'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${truckImg}.svg`)" alt="">
                    </button>
                  </v-col>
                  <v-col cols=3>
                    <button
                      @click="e1 = 2; vehicle = 'Motorcycles'"
                      @mouseenter="motoImg = motoImg + '_hover'"
                      @mouseleave="motoImg = 'motos'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${motoImg}.svg`)" alt="">
                    </button>
                  </v-col>
                </v-row>
                <v-row v-else id="row-mobile-vehicles">
                  <v-col cols=6>
                    <button
                      @click="e1 = 2; vehicle = 'Cars'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/mobile/car.svg`)" alt="">
                    </button>
                  </v-col>
                  <v-col cols=6>
                    <button
                      @click="e1 = 2; vehicle = 'Light Vehicles'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/mobile/lwk.svg`)" alt="">
                    </button>
                  </v-col>
                  <v-col cols=6>
                    <button
                      @click="e1 = 2; vehicle = 'Trucks & Bus'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/mobile/truck.svg`)" alt="">
                    </button>
                  </v-col>
                  <v-col cols=6 style="margin: auto">
                    <button
                      @click="e1 = 2; vehicle = 'Motorcycles'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/mobile/moto.svg`)" alt="">
                    </button>
                  </v-col>
                </v-row>
              </v-container>
              <!-- <VisitBizol  v-if="$vuetify.breakpoint.mobile" /> -->
            </v-stepper-content>

            <v-stepper-content step="2" >
              <Favorites v-bind:class="{'d-block' : $vuetify.breakpoint.mobile}" class="d-none" v-on:setbrand="setbrand"/>
              <List v-on:setbrand="setbrand" class="mb-5"/>
              <Favorites v-bind:class="{'d-block' : !$vuetify.breakpoint.mobile}" class="d-none" v-on:setbrand="setbrand"/>
              <v-btn 
                v-if="$vuetify.breakpoint.mobile && e1 != 5" 
                v-bind:class="{'d-block' : showTopButton}" 
                class="top-btn d-none"
                @click="scrollTop()"
                fab elevation="2" outlined icon 
                >
                <v-icon>
                  mdi-arrow-up
                </v-icon>
              </v-btn>
              <!-- <VisitBizol  v-if="$vuetify.breakpoint.mobile" /> -->
            </v-stepper-content>

            <v-stepper-content step="3" >
                <ListModel v-bind:brand="brand" v-on:setmodel="setmodel" class="mb-5"/>
                <!-- <VisitBizol  v-if="$vuetify.breakpoint.mobile" /> -->
            </v-stepper-content>

            <v-stepper-content step="4" >
                <ListType v-bind:model="model" v-on:settype="settype"  class="mb-5"/>
                <!-- <VisitBizol  v-if="$vuetify.breakpoint.mobile" /> -->
            </v-stepper-content>

            <v-stepper-content step="5" >
                <div :style="$vuetify.breakpoint.mobile ? 'margin-bottom: 100px;' : 'margin-bottom: 50px;'">
                  <h1 class="text-center text-h6 mt-2 mb-4">BIZOL Recommendations</h1>
                  <ExpansionPanel :info="{
                      isScroll: true,
                      title: 'Engine (SVQ20DE) - severe',
                      icon: 'engine.png',
                      buttons: {0:{ title: 'Go', url:'https://bizol.com'}}
                    }" />
                  <ExpansionPanel :info="{
                    isScroll: false,
                    title: 'Diferential, front-normal',
                    icon: 'differential_front_normal.png',
                    buttons: {0:{title: 'SDS', url: 'https://test.com'}, 1:{title: 'PDS', url: 'https://test.com'}}
                    }"/>
                  <ExpansionPanel :info="{
                    isScroll: false,
                    title: 'Cooling system - normal',
                    icon: 'cooling_system.png',
                    specialProduct: true,
                    buttons: {0:{title: 'Contact', url:'https://bizol.com'}}
                    }" />
                  <ExpansionPanel :info="{
                    isScroll: false,
                    title: 'Transmission, automatic (5/1 - normal)',
                    icon: 'transmission_automatic_normal.png',
                    buttons: {0:{title: 'SDS', url: 'https://test.com'}, 1:{title: 'PDS', url: 'https://test.com'}}
                    }"/>
                </div>
                <div :class="{'div-footer-step5' : $vuetify.breakpoint.mobile }">
                  <v-btn
                    v-if="e1 == 5"
                    block 
                    color="success" 
                    :class="{'mt-5 search-again-desktop' : !$vuetify.breakpoint.mobile}"
                    @click="resetTitle(1); e1 = 1;"
                  >
                    Search again
                  </v-btn>
                  <VisitBizol class="pt-0" v-if="$vuetify.breakpoint.mobile" />
                </div>
            </v-stepper-content>
          </v-stepper-items>
          
        </v-stepper>
        
    </v-container>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import List from "./views/List.vue";
import ListModel from "./views/ListModel.vue";
import ListType from "./views/ListType.vue";
import ExpansionPanel from "./views/ExpansionPanel.vue";
import Favorites from "./views/Favorites.vue";
import MainSearch from "./views/MainSearch.vue";
import VisitBizol from "./views/VisitBizol.vue";
import VueScrollTo from 'vue-scrollto';
Vue.use(VueScrollTo);
export default Vue.extend({
  name: "App",
  components: {
    List,
    ListModel,
    ListType,
    ExpansionPanel,
    Favorites,
    MainSearch,
    VisitBizol
  },
  watch: {
    e1: function (val) {
      const offsetVar = 127;
      const options = {
        container: '.horizontal-scroll-mobile',
        easing: 'ease-out',
        lazy: false,
        offset: val == 1 ? 0 : ((window.innerWidth / 2) - offsetVar) * -1,
        force: true,
        cancelable: true,
        x: true,
        y: false
      }
      if(this.$vuetify.breakpoint.mobile) {
        this.$scrollTo('#step'+val.toString(), 500, options); 
      }
    }
  },
  data: () => ({
    animateBanner: false,
    animateSteps: false,
    showTopButton: false,
    e1: 1,
    carImg: 'cars',
    lwkImg: 'lwk',
    truckImg: 'trucks',
    motoImg: 'motos',
    vehicle: '1. Choose your Vehicle',
    brand: '2. Choose your Brand',
    model: '3. Choose your Model',
    type: '4. Choose your Type',
  }),

  mounted() {
    console.log(this.$vuetify)
    window.onscroll = () => {    
        if(window.scrollY > 364) {
            this.$data.showTopButton = true;
        } else {
            this.$data.showTopButton = false;
        }
    };
  },
  methods: {
    truncateString(input: string) {
      
      return input.length > 22 ? `${input.substring(0, 19)}...` : input;
    },
    scrollTop() {
      const options = {
          container: 'body',
          easing: 'ease-out',
          lazy: false,
          offset: 0,
          force: true,
          cancelable: true,
          x: false,
          y: true
      }
      this.$scrollTo('.banner', 500, options); 
    },
    resetTitle(step = null) {
      switch (step ? step : this.$data.e1) {
        case 1:
          this.$data.vehicle = '1. Choose your Vehicle';
          this.$data.brand = '2. Choose your Brand';
          this.$data.model = '3. Choose your Model';
          this.$data.type = '4. Choose your Type';
          break;
        case 2:
          this.$data.brand = '2. Choose your Brand';
          this.$data.model = '3. Choose your Model';
          this.$data.type = '4. Choose your Type';
          break;
        case 3:
          this.$data.model = '3. Choose your Model';
          this.$data.type = '4. Choose your Type';
          break;
        case 4:
          this.$data.type = '4. Choose your Type';
          break;
        default:
          break;
      } 
    },
    setbrand(variable: string) {
        console.log(variable);
        this.$data.brand = variable
        this.$data.e1++;
    },
    setmodel(variable: string) {
        console.log(variable);
        this.$data.model = variable
        this.$data.e1++;
    },
    settype(variable: string) {
        console.log(variable);
        this.$data.type = variable
        this.$data.e1++;
    },
  }
});
</script>

<style lang="scss">
.v-stepper__content {
  padding: 0px !important;
}
#main-buttons {
  .col {
    text-align: center;
  }
}
@import url("https://fonts.googleapis.com/css2?family=Arimo:ital,wght@0,400;0,700;1,400;1,700&display=swap");
$mainGreen: #0c9d30;
.top-btn {
    position: fixed !important;
    bottom: 75px;
    background: white;
    z-index: 1;
    right: 10px;
}
.custom-btn {
  outline: none !important;
  width: 90%;
  height: 90%;
  img{
    width: 100%;
    height: 100%;
    min-height: 223px;
  }
}
.banner {
  transition: all 0.5s;
  background-image: url("../public/assets/header.jpg");
  height: 250px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  background-position-y: 60%;
}
.v-stepper--vertical .v-stepper__header {
  top: 55px !important;
}
.banner-mobile {
  width: 100%;
  position: fixed;
  z-index: 2;
  background-image: url("../src/assets/header-mobile.jpg");
  height: 55px;
  background-repeat: no-repeat;
  background-position: bottom left;
  background-size: cover;
}
.smallBanner {
  transition: all 0.5s;
  height: 180px;
  background-position-y: 60%;
}
.v-sheet.v-card:not(.v-sheet--outlined) {
  box-shadow: none !important;
}
.v-stepper__label {
  width: 230px;
}
.v-stepper__step .v-stepper__step--active {
  .v-stepper__label {
    width: 230px;
  } 
}
.theme--light.v-stepper .v-stepper__step--editable:hover {
  background: none !important;
  .v-stepper__label{
    &::before {
      background-color: #009d00 !important;
    }
    &::after {
      background-color: #009d00 !important;
    }
  }
}
#row-mobile-vehicles {
  .col {
    padding: 0px 6px !important;
  }
  .custom-btn {
    outline: none !important;
    width: 100%;

    height: auto;
    img {
      width: 100%;
      min-height: unset !important;
      height: auto;
    }
  }
}
.v-stepper__step {
  width: 230px;
  span {
    display: none;
  }
}

.v-stepper__step .v-stepper__label {
  // padding: 0 !important;
}
.v-application--is-ltr .v-stepper__label {
  text-align: center !important;
}
@media (max-width: 600px) {
  .v-list-item--link:before {
    
    border: none !important;
    border-radius: 6px;
  }
  .favorites {
    .custom-btn {
      width: 100px !important;
      height: 100px !important;
      img {
        min-height: unset !important;
      }
    }
  }
  .v-stepper--vertical .v-stepper__step {
    padding: 0px 24px 0px !important;
    margin-right: 33px;
  }
  #stepper_header {
    width: calc(100% - 24px) !important;
  }
  .v-stepper__step .v-stepper__label {
    padding: 10px !important;
  }
  .banner {
    height: 75px;
  }

  .input-search {
    outline: none;
    width: 100% ;
    border: 1px solid gray;
    border-radius: 6px !important;
    height: 36px;
  }
  .dropdown-content {
    height: unset !important;
    border: none;
    ul {
      -webkit-column-count: 1 !important;
      -moz-column-count: 1 !important;
      column-count: 1 !important;
      min-height: unset !important;
      padding: 0 !important;
    }
  }
  .list-model {
    max-height: unset !important;
    min-height: 300px ;
    height: unset !important;
    overflow-x: hidden;
    ul {
        -webkit-column-count: 1 !important;
        -moz-column-count: 1 !important;
        column-count: 1 !important;
    }
  }
}
.v-list-item--link:before {
  background-color: transparent !important;
  border: 1px solid $mainGreen;
  border-radius: 6px;
}
.theme--light.v-list-item:hover::before {
  opacity: 1 !important;
}
.v-stepper--vertical .v-stepper__content {
  padding: 0 15px !important;
}
.v-application--is-ltr .v-stepper--vertical .v-stepper__content {
  margin: 0 !important;
}
.v-stepper--vertical {
  padding-bottom: 0 !important;
  .v-stepper__header {
      background-color: white;
      position: fixed;
      z-index: 2;
      top: 85px;
      height: 72px;
      /* align-items: stretch; */
      display: flex;
      flex-wrap: nowrap;
      overflow-x: auto;
      white-space: nowrap;
      justify-content: space-between;
  }
  .v-stepper__items {
    margin-top: 140px;
  }
}

.hide {
  opacity: 0;
  transition: all 0.5s;
}
.hide-footer {
  display: none;
  transition: all 0.5s;
}
.display-footer {
  display: block;
}
.show {
  display: block;
}
.display {
  opacity: 1;
  transition: all 0.5s;
}
.scroll-fav {
  height: 100px;
  display: block;
  flex-wrap: nowrap;
  overflow-x: scroll;
  white-space: nowrap;
  overflow-y: hidden;
  align-items: stretch;
}
  .horizontal-scroll-mobile::-webkit-scrollbar-track, .scroll-fav::-webkit-scrollbar-track
  {
      display: none;
  }

  .horizontal-scroll-mobile::-webkit-scrollbar, .scroll-fav::-webkit-scrollbar
  {
      display: none;
  }

  .horizontal-scroll-mobile::-webkit-scrollbar-thumb, .scroll-fav::-webkit-scrollbar-thumb
  {
      display: none;
  }

.favorites {
  position: relative;
  bottom: 0;
  .custom-btn {
    outline: none !important;
    width: 175px;
    height: 175px;
    img{
      width: 100%;
      height: auto;
    }
  }
  
}
.v-stepper__step {
  padding: 0px 24px 0px !important;
}

.v-list--three-line .v-list-item, .v-list-item--three-line {
  min-height: 72px !important;
}
.v-expansion-panel {
  background-color: black !important;
  a {
    min-width: 40px;
    background-color: $mainGreen;
    color: white !important;
    padding: 10px;
    margin-right: 5px;
  }
  color: white !important;
  .ico-exp {
    flex: none !important;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
    margin-right: 5px;
  }
}
.v-expansion-panel-content {
  background-color: white !important;
  color: black !important;
}
.v-application--is-ltr .v-expansion-panel-header {
  height: 50px;
}
.v-expansion-panel--active > .v-expansion-panel-header {
  min-height: 50px;
  border-bottom-left-radius: 4px !important;
}
.v-expansion-panel-content__wrap {
  padding: 0 !important;
}
.v-expansion-panel-header {
  padding: 0px 10px 0px 0px !important;
}

.max-width {
  max-width: 1185px !important;
}
.v-stepper {
  box-shadow: none !important;
}
.v-stepper__label {
  color: white !important;
}
.first-step {
    .v-stepper__label {
      padding-left: 0px !important;
      &::before {
        transform: skewX(0) !important;
      }
      &::after {
        transform: skewX(-20deg);
      } 
    }
}

.input-search {
  outline: none;
  width: 100%;
  border: 1px solid gray;
  border-radius: 6px;
  height: 36px;
}

.last-step {
    .v-stepper__label {
      &::before {
        transform: skewX(-20deg) !important;
      }
      &::after {
        transform: skewX(0) !important;
      } 
    }
}
.v-stepper__step--complete {
  .v-stepper__label {
      &::before {
        background-color: black !important;
      }
      &::after {
        background-color: black !important;
      } 
    }
}
.v-application--is-ltr .theme--light.v-stepper--vertical .v-stepper__content:not(:last-child) {
  border: none !important;
}
.v-stepper__step--active {
  .v-stepper__label{
    &::before {
      position: absolute;
      z-index: -1;
      content: "";
      right: 105px;
      top: 15px;
      height: 35px;
      width: 125px;
      background-color: $mainGreen !important;
      transform: skewX(-20deg);
    }
    &::after {
      position: absolute;
      z-index: -1;
      content: "";
      right: 0px;
      top: 15px;
      height: 35px;
      width: 115px;
      background-color: $mainGreen !important;
      transform: skewX(-20deg);
    }
    padding: 10px;
    z-index: 1;
  }
}

.v-stepper__step {
  .v-stepper__label{
    &::before {
      position: absolute;
      z-index: -1;
      content: "";
      right: 105px;
      top: 15px;
      height: 35px;
      width: 125px;
      background-color: gray;
      transform: skewX(-20deg);
    }
    &::after {
      position: absolute;
      z-index: -1;
      content: "";
      right: 0px;
      top: 15px;
      height: 35px;
      width: 115px;
      background-color: gray;
      transform: skewX(-20deg);
    }
    padding: 10px;
    z-index: 1;
  }
}
.horizontal-scroll-mobile {
    
    display: flex;
    overflow: scroll !important;
    white-space: nowrap;
    justify-content: space-between;
    width: 100vw;
}
.horizontal-scroll {
    overflow-x: hidden;
    overflow-y: none;
    align-items: stretch;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 100%;
}
.v-stepper__header {  
  height: 65px !important;
  box-shadow: 0pt 3pt 3pt 3pt white !important;
}
.v-stepper--vertical {
  .v-stepper__header{
    .last-step{
      .v-stepper__label{
        &::after{
          // right: -160px;
        }
      }
    }
  }
}
.list-model {
    max-height: 400px;
    width: 100%;
    padding: 12px;
    // border: 1px solid $mainGreen;
    // border-radius: 10px;
    overflow-y: auto ;
    overflow-x: hidden;
    ul {
        -webkit-column-count: 5;
        -moz-column-count: 5;
        column-count: 5;

        li {
            list-style-type: none;
            cursor: pointer;
            &:hover {
                background-color: #009d00;
                border-radius: 6px;
                padding: 0px 5px;
            }
        }
    }
}
.search-again-desktop {
  display: block;
  margin-left: 40%;
  width: 20% !important;
  min-width: 200px !important;
}
.no-transition {
  .v-stepper__content { transition: none !important; }
}
.v-stepper--vertical .v-stepper__items {
  margin-top: 110px !important;
}
.bg-mainGreen {
  background: $mainGreen;
}
.div-footer-step5 {
    box-shadow: 0pt 0pt 9pt -2pt #202020;
    z-index: 2;
    background: white;
    position: fixed;
    display: flex;
    bottom: 0px;
    width: -webkit-fill-available;
    justify-content: space-between;
    flex-wrap: nowrap;
    button {
      min-width: unset !important;
      margin: 5px;
    }
    left: 0;
}
</style>
