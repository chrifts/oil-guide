<template>
    <v-container>
        <v-row>
            <div class="list-model">
                
                <!-- <ul v-if="this.brand != ''">
                    
                    <li v-for="(item, index) in models[this.brand]"
                        v-bind:item="item"
                        v-bind:index="index"
                        v-bind:key="index"
                        @click="setModel(item)"
                        
                    >
                        <span style="color: green;" v-if="item == 'Navara, D40 (2005 - 2015)'">{{item}}</span>
                        <span style="color: black;" v-else>{{item}}</span>
                    </li>
                </ul> -->
                <v-row>
                    <v-list-item
                            v-bind:class="'col-'+cols()"
                            v-for="(item, index) in models[this.brand]"
                            v-bind:item="item"
                            v-bind:index="index"
                            v-bind:key="index"
                            @click="setModel(item)"
                    >
                        <v-list-item-content>
                            <v-list-item-title>{{item}}</v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-row>
            </div>
        </v-row>
        
    </v-container>
</template>

<script lang='ts'>
import Vue from "vue";

export default Vue.extend({
    name: "ListModel",  
    methods: {
        setModel(item: string) {
            
            this.$data.model = item;
            this.$emit('setmodel', this.$data.model)
        },
        cols() {
            let cols = '12';
            if(!this.$vuetify.breakpoint.mobile) {
                this.$data.models[this.brand].length <= 3 ? cols = ((12 / this.$data.models[this.brand].length)).toString() : cols = '3';
            }
            return cols;
        },
    },
    props: {
        brand: String,
    },
    data: () => ({
        model: "",
        models: {
            "Abrath": ["595", "695", "124 Spider"],
            "Audi": ["A3", "A5", "Q3", "Q5"],
            "Bmw": ["M3", "X5", "i3", "X4"],
            "Nissan (EU)": [
                "100 NX (1991 - 1995)", "200 SX (1989 - 1999)", "300 ZX (1984 - 1991)", "350Z, Z33 (2003 - 2009)", 
                "350Z, Z33 (2003 - 2009)", "Juke, F16 (2019 - )", "Laurel (1986 - 1989)", "Leaf, ZE1 (2017 - )",
                "Leaf, ZE0 (2010 - 2017)", "Leaf, ZE0 (2010 - 2017)", "Navara, D40 (2005 - 2015)", "Note, E11 (2006 - 2013)",
                "Note, E12 (2013 - 2017)", "Pathfinder, R51 (2005 - 2014)", "Pathfinder / Terrano (1986 - 2005)", "Qashqai, J11 (2014 - )",
                "Qashqai, J10 (2007 - 2014)", "Serena, C23 (1992 - 2000)", "Skyline, R31/R32/R33/R34 (1985 - 2002)", "Stanza (1982 - 1986)"
            ]
        },
    })
});
</script>

<style lang="scss">

</style>