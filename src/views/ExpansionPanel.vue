<template>
    <v-expansion-panels class="mt-2">
        <v-expansion-panel>
        <v-expansion-panel-header>
            <img src="@/assets/standard/cars.svg" width="75" height="50" alt="engine" class="ico-exp">
            Engine (SVQ20DE) - severe
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
                    <th></th>
                </tr>
                </thead>
                <tbody>
                <tr>
                    <td>Capacity 4,1 litre / Filter capacity 0,2 litre</td>
                    <td class="text-right">Change 7500 km/ 3 months** Please follow OEM recommendation</td>
                </tr>
                </tbody>
            </template>
            </v-simple-table>
            <v-simple-table :class="{'scrollTable' : info.isScroll}">
            <template v-slot:default>
                <thead :style="info.isScroll ? 'display: block; width: 100%' : ''" style="border-bottom: thin solid rgba(0, 0, 0, 0.12)">
                    <tr v-if="!info.isScroll">
                        <th class="text-left green--text text-h6">Products</th>
                        <th class="text-left green--text text-h6">Sizes</th>
                        <th class="text-left"></th>
                    </tr>
                    <tr v-else>
                        <th class="text-left green--text text-h6 border-0">Products</th>
                    </tr>
                </thead>
                <tbody v-if="!info.isScroll">
                    <tr >
                        <td>BIZOL Technology 5W-30 C2</td>
                        <td>1 L / 4 L / 200 L</td>
                        <td class="text-right">
                            <a v-for="(item, index) in info.buttons" :key="index" color="success" class="">{{item.title}}</a>
                        </td>
                    </tr>
                </tbody>
                <div v-else class="scrollableDiv">
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

</style>