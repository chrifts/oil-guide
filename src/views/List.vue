<template>
    <v-container :class="{'cont-mob-list' : !$vuetify.breakpoint.mobile}">
        <v-row >
            <!-- <v-icon
                large
                color="green darken-2"
                style="display: inline; width: 20%; text-align: center"
                align-center
            >
                mdi-magnify
            </v-icon> -->
            <input type="text" v-on:keyup="filterData(brands, $event.target.value)" class="input-search" placeholder=' Filter: eg. Audi'>
        </v-row>
        <!-- DESKTOP -->
        <v-row v-if="!$vuetify.breakpoint.mobile" justify="space-between">
            <v-col cols=12>
                <!-- DESKTOP ROW FILTERED -->
                <v-row v-if="filterBrands != null">
                    <div class="dropdown-content">
                        <v-row>
                            <v-list-item
                                class="col-md-3"
                                v-for="(item, index2) in filterBrands['filter']"
                                v-bind:item="item"
                                v-bind:index="index2"
                                v-bind:key="index2"
                                @click="setBrand(item)"
                            >
                                <v-list-item-avatar>
                                    <v-img src="@/assets/noimg.png"></v-img>
                                </v-list-item-avatar>
                                <v-list-item-content>
                                    <v-list-item-title>{{item}}</v-list-item-title>
                                </v-list-item-content>
                            </v-list-item>
                        </v-row>
                    </div>
                    
                </v-row>
                <!-- DESKTOP ROW ALL LETTERS -->
                <v-row v-else>
                    <div
                        v-bind:class="{'hovered' : letter == index}"
                        v-for="(item, index) in brands"
                        v-bind:item="item"
                        v-bind:index="index"
                        v-bind:key="index"
                        class="dropdown"
                        @mouseenter="letter = index"
                    >
                        
                        <span class=''>{{index}}</span>
                    </div>
                    <div class="dropdown-content">
                        <!-- <ul>
                            <li v-for="(item, index) in brands[letter]"
                                v-bind:item="item"
                                v-bind:index="index"
                                v-bind:key="index"
                                @click="setBrand(item)"
                            >
                                {{item}}
                            </li>
                        </ul> -->
                        <v-row>
                            <v-list-item
                                v-bind:class="brands[letter].length <= 3 ? 'col-'+((12 / brands[letter].length)) : 'col-3'"
                                v-for="(item, index) in brands[letter]"
                                v-bind:item="item"
                                v-bind:index="index"
                                v-bind:key="index"
                                @click="setBrand(item)"
                            >
                                    <v-list-item-avatar>
                                        <v-img src="@/assets/noimg.png"></v-img>
                                    </v-list-item-avatar>

                                    <v-list-item-content>
                                    <v-list-item-title>{{item}}</v-list-item-title>
                                </v-list-item-content>
                            </v-list-item>
                        </v-row>
                    </div>
                </v-row>
            </v-col>
        </v-row>
        <!-- MOBILE -->
        
        <v-row v-else id='mobile-letters'>
            
            <v-col cols=12>
                <!-- ROW ALL LETTERS -->
                
                <v-row v-if="filterBrands == null" id="list-brands">
                    
                    <div 
                        v-for="(arrBrand, letter) in brands"
                        v-bind:item="arrBrand"
                        v-bind:index="letter"
                        v-bind:key="letter"
                        class="dropdown"
                        
                    >
                        <span >{{letter}}</span>
                        <v-list three-line>
                            <template v-for="(theBrand, index2) in brands[letter]">
                                <v-divider :key="index2" ></v-divider>
                                <v-list-item
                                @click="setBrand(theBrand)"
                                :key="theBrand + index2 + Math.random().toString()"
                                >
                                    <!-- Checquear: NO pueden haber duplicados de theBrand -->
                                    <v-list-item-avatar>
                                        <v-img src="@/assets/noimg.png"></v-img>
                                    </v-list-item-avatar>

                                    <v-list-item-content>
                                        <v-list-item-title v-html="theBrand"></v-list-item-title>
                                        
                                    </v-list-item-content>
                                </v-list-item>
                            </template>
                        </v-list>  
                    </div>
                </v-row>
                <!-- ROW FILTERED -->
                <v-row v-else>
                    <div class="dropdown">
                        <v-list three-line>
                            <template  v-for="(item, index2) in filterBrands['filter']">

                                <v-divider
                                :key="index2"
                                ></v-divider>

                                <v-list-item
                                @click="setBrand(item)"
                                :key="item + index2 + Math.random().toString()"
                                >
                                <v-list-item-avatar>
                                    <v-img src="@/assets/noimg.png"></v-img>
                                </v-list-item-avatar>

                                <v-list-item-content>
                                    <v-list-item-title v-html="item"></v-list-item-title>
                                    
                                </v-list-item-content>
                                </v-list-item>
                            </template>
                        </v-list>  
                    </div>
                    
                </v-row>
            </v-col>
        </v-row>
        
    </v-container>
</template>

<script lang='ts'>
import Vue from "vue";
import VueScrollTo from 'vue-scrollto';
Vue.use(VueScrollTo);
export default Vue.extend({
    name: "List",
    methods: {
        setBrand(item: string) {
            this.$data.brand = item;
            this.$emit('setbrand', this.$data.brand)
        },
        filterData(raw: Record<string, any>, allowed: string) {
            let filterBrands: any = {}
            if(allowed == '') {
                filterBrands = null;    
            } else {
                filterBrands = {
                    "filter" : [

                    ]
                }
                Object.entries(raw).forEach(
                    ([key, value]) => {
                        value.filter(function (el: string) {
                            if(el.toLowerCase().includes(allowed.toLowerCase())) {
                                if(!filterBrands.filter.includes(el)) {
                                    filterBrands.filter.push(el)
                                }
                            }
                        });
                    }
                );
            }
            this.$data.filterBrands = filterBrands;
        },
        fillAllBrand() {
            Object.keys(this.$data.brands).forEach(key => {
                if(key != 'ALL') {
                    this.$data.brands[key].forEach((element: string) => {
                        this.$data.brands['ALL'].push(element);
                    });
                }
            });
        }
    },
    mounted() {
        console.log();
        this.fillAllBrand();
        if(this.$vuetify.breakpoint.mobile) {
            delete this.$data.brands.ALL;
        } else {
            this.$data.brands.ALL = []
            this.fillAllBrand();
        }
    },
    data: () => ({
        noimgsrc: '/assets/noimg.png',
        letter: 'ALL',
        brand: "",
        filterBrands: null,
        brands: {
            "ALL": [],
            "A": ['Audi', 'Abrath'],
            "B": ['Bmw'],
            "C": ['Chrysler', 'Chevrolet'],
            "D": ['Daihatsu', 'D Brand 2', 'D Brand 3'],
            "E": ['E Brand 1', 'E Brand 2', 'E Brand 3'],
            "F": ['Ford', 'Fiat'],
            "G": ['GMC', 'G Brand 2'],
            "H": ['Honda', 'Hiunday', 'H Brand 3'],
            "I": ['I Brand 1', ' I Brand 2', 'I Brand 3'],
            "J": ['Jeep', 'J Brand 2', 'J Brand 3'],
            "K": ['K Brand 1', 'K Brand 2', 'K Brand 3'],
            "L": ['Brand 1', 'Brand 2', 'Brand 3'],
            "M": ['Brand 1', 'Brand 2', 'Brand 3'],
            "N": ['Nissan (DongFeng) (CHN)', 'Nissan (EU)', 'Nissan (RUS)', 'Nissan (USA/CAN)', 'Nobel'],
            "O": ['Brand 1', 'Brand 2', 'Brand 3'],
            "P": ['Brand 1', 'Brand 2', 'Brand 3'],
            "Q": ['Brand 1', 'Brand 2', 'Brand 3'],
            "R": ['Brand 1', 'Brand 2', 'Brand 3'],
            "S": ['Brand 1', 'Brand 2', 'Brand 3'],
            "T": ['Brand 1', 'Brand 2', 'Brand 3'],
            "U": ['Brand 1', 'Brand 2', 'Brand 3'],
            "V": ['Brand 1', 'Brand 2', 'Brand 3'],
            "W": ['Brand 1', 'Brand 2', 'Brand 3'],
            "X": ['Brand 1', 'Brand 2', 'Brand 3'],
            "Y": ['Brand 1', 'Brand 2', 'Brand 3'],
            "Z": ['Brand 1', 'Brand 2', 'Brand 3'],
        },
    })
});
</script>

<style lang="scss">
$mainGreen: #0c9d30;
@media (max-width: 600px) {
    .dropdown {
        width: 100%;
        &:hover {
            background-color: unset !important;
            border: none !important;
            color: black !important;
        }
        &:focus {
            
            border: none !important;
            color: black !important;
        }
        span {
            text-align: left;
            display: block;
        }
    }
}
.dropdown {
    font-size: 18px;
    flex-grow: 1;
    text-align: center;
    cursor: default;
    span{
        padding:4px 7px;
    }
    &:hover {
        background-color: $mainGreen;
        border: 1px solid $mainGreen;
        border-radius: 10px 10px 0 0;
        color: white;
    }
    position: relative;
    display: inline-block;
}
.hovered {
    background-color: $mainGreen;
    border: 1px solid $mainGreen;
    border-radius: 10px 10px 0 0;
    color: white;
}

.dropdown-content {
    overflow-y: auto;
    overflow-x: hidden;
    ul {
        -webkit-column-count: 5;
        -moz-column-count: 5;
        column-count: 5;
        min-height: 15vh;
        max-height: 100%;   
        
        height: 100%;
        li {
            list-style-type: none;
            cursor: pointer;
            &:hover {
                background-color: #009d00;
                border-radius: 6px;

            }
        }
    }
    height: 250px;
    position: relative;
    width: 100%;
    // background-color: #fafafa85;
    min-width: 160px;
    // box-shadow: 7pt 6pt 8pt -10pt black;
    border: 1px solid #e0e0e0;
    border-radius: 0px 0px 10px 10px;
    padding: 12px 16px;
    z-index: 1;
}

.dropdown-content:hover  {
    display: block;
}

.dropdown-content::-webkit-scrollbar-track
{
border-radius: 10px;
background-color: #F5F5F5;
}

.dropdown-content::-webkit-scrollbar
{
    width: 6px;
    background-color: #F5F5F5;
}

.dropdown-content::-webkit-scrollbar-thumb
{
border-radius: 6px;
-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
background-color: $mainGreen;
}

.dropdown-content:hover ~ .dropdown  {
    span {
        background-color: $mainGreen;
        border: 1px solid $mainGreen;
        border-radius: 10px;
        color: white; 
    }
}
.dropdown:hover ~ .dropdown-content {
  display: block;
}
$boder-list-color: rgba(0, 0, 0, 0.12);
.dropdown {
    .v-list {
        padding-bottom: 0 !important;
        .v-list-item {
            border-left: 1px solid $boder-list-color;
            border-right: 1px solid $boder-list-color;
        }
        &:last-child {
            border-bottom: 1px solid $boder-list-color

        }
    }
}
.cont-mob-list {
    // padding: 0 20px !important;
}
</style>