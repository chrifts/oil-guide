<template>
  <v-app>
    <div class="banner" v-bind:class="{'smallBanner': (e1 > 1 && !$vuetify.breakpoint.mobile)}"></div>
      <v-container class="max-width" style="padding: 0;">
          <v-row v-if="!$vuetify.breakpoint.mobile" v-bind:class="{'hide-footer': (e1 > 1)}" >
            <v-col md=10 class="my-auto">
              <input type="text" name="" id="" placeholder="Search by name (enter al lest 3 letters)" class="input-search">
            </v-col>
            <v-col md=2>
              <v-btn
                color="success"
                width="100%"
              >
                SEARCH
              </v-btn>
            </v-col>
            
          </v-row>
          <v-row v-if="!$vuetify.breakpoint.mobile" v-bind:class="{'show': (e1 > 1)}" class="hide-footer">
            <v-col cols=12>
              <v-btn @click="e1--; resetTitle()" color="success">back</v-btn>
            </v-col>
          </v-row>
          <v-stepper v-model="e1" :vertical="$vuetify.breakpoint.mobile">
            <v-stepper-header id="stepper_header">
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
            </v-stepper-header>

            <v-stepper-items style="">
              <v-stepper-content step="1" style="padding: 0 !important;">
                <v-container>
                  <v-row v-if="!$vuetify.breakpoint.mobile" justify="space-between">
                    <button
                      
                      @click="e1 = 2; vehicle = 'Cars'"
                      @mouseenter="carImg = carImg + '_hover'"
                      @mouseleave="carImg = 'cars'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${carImg}.svg`)" alt="">
                    </button>

                    <button
                      @click="e1 = 2; vehicle = 'Light Vehicles'"
                      @mouseenter="lwkImg = lwkImg + '_hover'"
                      @mouseleave="lwkImg = 'lwk'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${lwkImg}.svg`)" alt="">
                    </button>
                    <button
                      @click="e1 = 2; vehicle = 'Trucks & Bus'"
                      @mouseenter="truckImg = truckImg + '_hover'"
                      @mouseleave="truckImg = 'trucks'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${truckImg}.svg`)" alt="">
                    </button>
                    <button
                      @click="e1 = 2; vehicle = 'Motorcycles'"
                      @mouseenter="motoImg = motoImg + '_hover'"
                      @mouseleave="motoImg = 'motos'"
                      class="custom-btn"
                    >
                      <img :src="require(`@/assets/standard/${motoImg}.svg`)" alt="">
                    </button>
                    
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
              </v-stepper-content>

              <v-stepper-content step="2" >
                <Favorites v-bind:class="{'d-block' : $vuetify.breakpoint.mobile}" class="d-none" v-on:setbrand="setbrand"/>
                <List v-on:setbrand="setbrand"/>
                <Favorites v-bind:class="{'d-block' : !$vuetify.breakpoint.mobile}" class="d-none" v-on:setbrand="setbrand"/>
                <v-btn v-if="$vuetify.breakpoint.mobile" v-bind:class="{'d-block' : showTopButton}" class="top-btn d-none" @click="scrollTop()">top</v-btn>
              </v-stepper-content>

              <v-stepper-content step="3" >
                  <ListModel v-bind:brand="brand" v-on:setmodel="setmodel"/>
              </v-stepper-content>

              <v-stepper-content step="4" >
                  <ListType v-bind:model="model" v-on:settype="settype"  />
              </v-stepper-content>

              <v-stepper-content step="5" >
                  <div style="min-height: 480px">
                    <h1 class="text-center">BIZOL Recommendations</h1>
                    <h2 class="text-center">Choose a category and find your BIZOL solution</h2>
                    <ExpansionPanel />
                    <ExpansionPanel />
                    <ExpansionPanel />
                    <ExpansionPanel />
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
  },
  watch: {
    e1: function (val) {
      const options = {
        container: '#stepper_header',
        easing: 'ease-out',
        lazy: false,
        offset: val == 1 ? 0 : ((window.innerWidth / 2) - 115) * -1,
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
      return input.length > 22 ? `${input.substring(0, 22)}...` : input;
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
@import url("https://fonts.googleapis.com/css2?family=Arimo:ital,wght@0,400;0,700;1,400;1,700&display=swap");
.top-btn {
    position: fixed !important;
    bottom: 10px;
    z-index: 1;
    right: 10px;
}
.custom-btn {
  width: 250px;
  height: 250px;
  img{
    width: 250px;
    height: 250px;
  }
}
.banner {
  transition: all 0.5s;
  background-image: url("../public/assets/header.jpg");
  height: 470px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
.smallBanner {
  transition: all 0.5s;
  height: 235px;
  background-position-y: -150px;
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
  .custom-btn {
    width: 100%;

    height: auto;
    img {
      width: 100%;
      
      
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
  padding: 0 !important;
}
.v-application--is-ltr .v-stepper__label {
  text-align: center !important;
}
@media (max-width: 768px) {
  .v-stepper__step .v-stepper__label {
    padding: 10px !important;
  }
  .banner {
    height: 75px;
  }

  .input-search {
    outline: none;
    width: 100% !important;
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
.v-stepper--vertical .v-stepper__content {
  padding: 0 15px !important;
}
.v-application--is-ltr .v-stepper--vertical .v-stepper__content {
  margin: 0 !important;
}
.v-stepper--vertical {
  .v-stepper__header {
        height: 72px;
        /* align-items: stretch; */
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        white-space: nowrap;
        justify-content: space-between;
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
  height: 90px;
  display: block;
  flex-wrap: nowrap;
  overflow-x: scroll;
  white-space: nowrap;
  overflow-y: hidden;
  align-items: stretch;
}
.favorites {
  position: relative;
  bottom: 0;
  .custom-btn {
    width: 100px;
    height: 100px;
    img{
      width: 100%;
      height: auto;
    }
  }
  
}
.v-stepper--vertical .v-stepper__step {
  padding: 17px 24px 16px !important;
  margin-right: 33px;
}
.v-list--three-line .v-list-item, .v-list-item--three-line {
  min-height: 72px !important;
}
.v-expansion-panel {
  background-color: black !important;
  color: white !important;
  .ico-exp {
    flex: none !important;
  }
}
.v-expansion-panel-content {
  background-color: white !important;
  color: black !important;
}
.v-application--is-ltr .v-expansion-panel-header {
  height: 60px;
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
.v-stepper__header, .v-stepper {
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
      height: 50px;
      width: 125px;
      background-color: green !important;
      transform: skewX(-20deg);
    }
    &::after {
      position: absolute;
      z-index: -1;
      content: "";
      right: 0px;
      top: 15px;
      height: 50px;
      width: 115px;
      background-color: green !important;
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
      height: 50px;
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
      height: 50px;
      width: 115px;
      background-color: gray;
      transform: skewX(-20deg);
    }
    padding: 10px;
    z-index: 1;
  }
}

.v-stepper__header {  
  height: 83.54px !important;
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
    height: 480px;
    width: 100%;
    padding: 10px;
    border: 1px solid green;
    border-radius: 10px;
    overflow-y: scroll ;
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

</style>
