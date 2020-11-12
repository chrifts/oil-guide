<template>
    <v-expansion-panels class="mt-2">
        <v-expansion-panel>
            <v-expansion-panel-header>
                <img :src="require(`@/assets/step5/${info.icon}`)" width="65" height="50" alt="engine" class="ico-exp">
                {{info.title}}
                <template v-slot:actions>
                <v-icon color="white">
                    $expand
                </v-icon>
                </template>
            </v-expansion-panel-header>
            <v-expansion-panel-content class="exp-panel-cont">
                <v-simple-table >
                    <template v-slot:default >
                        <thead>
                        <tr>
                            <th class="text-left green--text text-h6" >
                            Capacities / intervals
                            </th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr class="strip">
                            <td>Capacity 4,1 litre / Filter capacity 0,2 litre Change 7500 km/ 3 months**</td>
                        </tr>
                        <tr>
                            <td>Please follow OEM recommendation</td>
                        </tr>
                        </tbody>
                    </template>
                </v-simple-table>
                <v-simple-table :class="{'scrollTable' : info.isScroll}">
                    <template v-slot:default>
                        <thead :style="info.isScroll ? 'display: block; width: 100%' : ''" style="border-bottom: thin solid rgba(0, 0, 0, 0.12)">
                            <tr>
                                <th class="text-left green--text text-h6">Products</th>
                            </tr>
                        </thead>
                        <tbody v-if="!info.isScroll && info.specialProduct">
                            <tr class="strip">
                                <td>
                                    <div class="row">
                                        <v-col :cols="$vuetify.breakpoint.mobile ? 7 : 8">
                                            <h4 class="text-left">{{info.specialProduct ? 'Special product' : 'BIZOL Technology 5W-30 C2'}}</h4>
                                            <h5 class="text-left">{{info.specialProduct ? 'Please contact us' : 'Sizes 1 L / 4 L / 200 L'}}</h5>
                                        </v-col>
                                        <v-col :cols="$vuetify.breakpoint.mobile ? 5 : 4">
                                            <v-row style="justify-content: flex-end;">
                                                <v-col v-for="(item, index) in info.buttons" :key="index" cols="12" class="pt-0 px-1">
                                                    <a  color="success" class="btn-sdspds">{{item.title}}</a>
                                                </v-col>
                                            </v-row>
                                        </v-col>
                                    </div>
                                </td>
                                
                            </tr>
                        </tbody>
                        <tbody v-if="!info.isScroll && !info.specialProduct">
                            <tr class="strip">
                                <td>
                                    <div class="row">
                                        <v-col :cols="$vuetify.breakpoint.mobile ? 7 : 8">
                                            <h4 class="text-left">{{info.specialProduct ? 'Special product' : 'BIZOL Technology 5W-30 C2'}}</h4>
                                            <h5 class="text-left">{{info.specialProduct ? 'Please contact us' : 'Sizes 1 L / 4 L / 200 L'}}</h5>
                                        </v-col>
                                        <v-col :cols="$vuetify.breakpoint.mobile ? 5 : 4">
                                            <v-row>
                                                <v-col v-for="(item, index) in info.buttons" :key="index" cols="6" class="pt-0 px-1">
                                                    <a  color="success" class="btn-sdspds">{{item.title}}</a>
                                                </v-col>
                                            </v-row>
                                        </v-col>
                                    </div>
                                </td>
                            </tr>
                            <tr class="strip">
                                <td>
                                    <div class="row">
                                        <v-col cols="12">
                                            <h4 class="text-left">{{info.specialProduct ? 'Special product' : 'BIZOL Technology 5W-30 C2'}}</h4>
                                            <h5 class="text-left">{{info.specialProduct ? 'Please contact us' : 'Sizes 1 L / 4 L / 200 L'}}</h5>
                                        </v-col>
                                        <v-col cols="12">
                                            <v-row class="justify-content: center;">
                                                <a v-for="(item, index) in info.buttons" :key="index" color="success" style="width: 48%;">{{item.title}}</a>
                                            </v-row>
                                        </v-col>
                                    </div>
                                </td>
                            </tr>
                        </tbody>
                        <div v-if="info.isScroll" class="scrollableDiv">
                            <div>
                                <div class="d-flex">
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                    <button>
                                        <img src="../../src/assets/mobile/oil.svg" alt="">
                                    </button>
                                </div>
                            </div>
                        </div>
                    </template>
                </v-simple-table>
            </v-expansion-panel-content>
        </v-expansion-panel>
    </v-expansion-panels>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    props: {
        info: {},
    }
})
</script>
<style lang="scss">
$mainGreen: #0c9d30;
.v-application .green--text {
    color: $mainGreen !important;
    caret-color: $mainGreen !important;
}
.scrollTable {
    .v-data-table__wrapper {
        overflow-x: unset !important;
        overflow-y: unset !important;
        table {
            display: block;
            width: 100% !important;
        }
    }
}
.scrollableDiv {
    overflow-x: auto; 
    padding-left: 6px;
    button {
        padding: 0 5px;
        margin-top: 5px;
    }
}

.scrollableDiv::-webkit-scrollbar-track
{
    height: 8px;
    border-radius: 10px;
    background-color: #F5F5F5;
}

.scrollableDiv::-webkit-scrollbar
{
    height: 8px;
    background-color: #F5F5F5;
    &:hover {
        height: 8px;
    }
}

.scrollableDiv::-webkit-scrollbar-thumb
{
    height: 8px;
    border-radius: 6px;
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
    background-color: $mainGreen;
}

.border-0 {
    border: none !important;
}

.strip {
    background-color: #e5e5e5;
}
.btn-sdspds {
    display: block;
    width: 100%;
    max-width: unset;
}

</style>