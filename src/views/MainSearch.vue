<template>
    <v-container>
        <v-row v-bind:class="{'hide-footer': (step > 1 && !mobile)}" > 
            <v-col :cols="activeMobileInput && mobile ? 12 : 10" class="my-auto d-none-c" id="div-search" :class="{'d-block-c' : (activeMobileInput || !mobile)}">
                <div class="d-flex">
                    <v-btn
                        tile
                        color="white"
                        :class="mobile ? 'd-block' : 'd-none'"
                        @click="search()"
                    >
                        <v-icon>mdi-magnify</v-icon>
                    </v-btn>
                        <input type="text" name="" :id="mobile ? 'main-search-mobile' : 'main-search'" :placeholder="mobile ? ' General search (3 letters min)' : ' Search by name (enter al lest 3 letters)'" class="input-search">
                    <v-btn 
                        tile 
                        @click="activeMobileInput = !activeMobileInput" 
                        color="white"
                        :class="mobile ? 'd-block' : 'd-none'"
                    >
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </div>
            </v-col>
            <v-col cols=2>
                <v-btn
                    :color="mobile ? 'white' : 'success'"
                    width="100%"
                    :icon="mobile"
                    @click="mobile ? activeMobileInput = !activeMobileInput : search()"
                >
                    <v-icon>mdi-magnify</v-icon>
                </v-btn>
            </v-col>
        </v-row>
    </v-container>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    props: {
        step: Number,
        mobile: Boolean,
    },
    data: ()=>({
        activeMobileInput: false,
    }),
    methods: {
        search() {
            console.log('search')
        }
    }
})
</script>
<style lang="scss">
 
@keyframes fadeOut {
    0% { opacity: 1; }
    50% { opacity: 0.5;}
    100% { opacity: 0; transform: translateX(-15px);}
}
.d-none-c{
    display: block;
    -webkit-animation: fadeOut 0.5s;
    animation: fadeOut 0.5s;
    animation-fill-mode: forwards;
}

@keyframes fadeIn {
    0% { opacity: 0; transform: translateX(-15px)}
    50% { opacity: 0.5; }
    100% { opacity: 1; transform: translateX(0px)}
}

.d-block-c{
    display: block;
    -webkit-animation: fadeIn 0.5s;
    animation: fadeIn 0.5s;
    animation-fill-mode: forwards;
    .v-btn--contained {
        box-shadow: none !important;
    }
}

#div-search {
    // transition: all 0.0s;
}

#main-search-mobile {
    
    border: unset !important;
    border-radius: unset !important;
    background-color: white;
    &::placeholder {
        color: gray;
    }
}
</style>