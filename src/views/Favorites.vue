<template>
    <div class="favorites">
        <v-container style="overflow: hidden">
            <h2>
            Favorites
            </h2>
            <v-row justify="space-between" v-bind:class="{'scroll-fav' : $vuetify.breakpoint.mobile}">
            <button
                @click="brand = 'Ford'"
                @mouseenter="favs.fav0 = 'hover/0'"
                @mouseleave="favs.fav0 = 'standard/0'"
                class="custom-btn"
            >
                <img :src="require(`@/assets/favorites/${favs.fav0}.svg`)" alt="">
            </button>

            <button
                @click="brand = 'Nissan (EU)'"
                @mouseenter="favs.fav1 = 'hover/1'"
                @mouseleave="favs.fav1 = 'standard/1'"
                class="custom-btn"
            >
                <img :src="require(`@/assets/favorites/${favs.fav1}.svg`)" alt="">
            </button>
            <button
                @click="brand = 'Opel'"
                @mouseenter="favs.fav2 = 'hover/2'"
                @mouseleave="favs.fav2 = 'standard/2'"
                class="custom-btn"
            >
                <img :src="require(`@/assets/favorites/${favs.fav2}.svg`)" alt="">
            </button>
            <button
                @click="brand = 'Renault'"
                @mouseenter="favs.fav3 = 'hover/3'"
                @mouseleave="favs.fav3 = 'standard/3'"
                class="custom-btn"
            >
                <img :src="require(`@/assets/favorites/${favs.fav3}.svg`)" alt="">
            </button>
            <button
                @click="brand = 'Skoda'"
                @mouseenter="favs.fav4 = 'hover/4'"
                @mouseleave="favs.fav4 = 'standard/4'"
                class="custom-btn"
            >
                <img :src="require(`@/assets/favorites/${favs.fav4}.svg`)" alt="">
            </button>
            </v-row>
        </v-container>
    </div>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    methods: {
        setBrand(item: string) {
            this.$data.brand = item;
            this.$emit('setbrand', this.$data.brand)
        },
    },
    watch: {
        brand: function(val) {
            this.setBrand(val)
        }
    },
    data: ()=>({
        brand:'',
        favs: {
            fav0: 'standard/0',
            fav1: 'standard/1',
            fav2: 'standard/2',
            fav3: 'standard/3',
            fav4: 'standard/4',
        },
    }),
})
</script>