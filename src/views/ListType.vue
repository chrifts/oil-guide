<template>
    <v-container>
        <v-row>
            <div class="list-model">
                <!-- <ul v-if="this.model != ''">
                    
                    <li v-for="(item, index) in types[this.model]"
                        v-bind:item="item"
                        v-bind:index="index"
                        v-bind:key="index"
                        @click="setType(item)"
                    >
                        {{item}}
                    </li>
                </ul> -->
                <v-row>
                    <v-list-item
                        v-bind:class="'col-'+cols()"
                        v-for="(item, index) in types[this.model]"
                        v-bind:item="item"
                        v-bind:index="index"
                        v-bind:key="index"
                        @click="setType(item)"
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
    name: "ListType",  
    methods: {
        setType(item: string) {
            this.$data.type = item;
            this.$emit('settype', this.$data.type)
        },
        cols() {
            let cols = '12';
            if(!this.$vuetify.breakpoint.mobile) {
                this.$data.types[this.model].length <= 3 ? cols = ((12 / this.$data.types[this.model].length)).toString() : cols = '3';
            }
            return cols;
        },
    },
    props: {
        model: String,
    },
    data: () => ({
        type:"",
        types: {
            "Navara, D40 (2005 - 2015)": [
                "Navara 2.5 dCi (2005 - 2007)", "Navara 2.5 dCi (140 kW) (2010 - 2015)", "Navara 2.5 dCi (140 kW) AWD (2010) - 2015)",
                "Navara 2.5 dCi (140 kW) DPF (2010 - 2015)", "Navara 2.5 dCi (140 kW) DPF AWD (2010 - 2015)", "Navara 2.5 dCi DPF (2007 - 2010)",
                "Navara 3.0 dCi V6 2WD (2010 - 2015)", "Navara 3.0 dCi V6 4WD (2010 - 2015)"
            ]
        }
    })
});
</script>

<style lang="scss">

</style>