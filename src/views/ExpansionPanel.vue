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
        <v-expansion-panel-content>
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
            <v-simple-table :class="{'scrollTable' : isScroll}">
            <template v-slot:default>
                <thead :style="isScroll ? 'display: block; width: 100%' : ''">
                    <tr v-if="!isScroll">
                        <th class="text-left green--text text-h6">Products</th>
                        <th class="text-left green--text text-h6">Sizes</th>
                        <th class="text-left"></th>
                    </tr>
                    <tr v-else>
                        <th class="text-left green--text text-h6">Products</th>
                    </tr>
                </thead>
                <tbody v-if="!isScroll">
                    <tr >
                        <td>BIZOL Technology 5W-30 C2</td>
                        <td>1 L / 4 L / 200 L</td>
                        <td class="text-right"><v-btn color="success">Go</v-btn></td>
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
        isScroll: Boolean,
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
    overflow-x: scroll; 
    padding-left: 6px;
    button {
        padding: 0 5px;
        margin-top: 5px;
    }
}
</style>