<template>
  <div>
    <v-stepper>
      <v-stepper-header>
        <v-stepper-step step="1">
          Select campaign settings
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step step="2">
          Create an ad group
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step step="3">
          Create an ad
        </v-stepper-step>
      </v-stepper-header>
    </v-stepper>

    <v-stepper
      value="2"
      class="mt-12"
    >
      <v-stepper-header>
        <v-stepper-step
          step="1"
          complete
        >
          Select campaign settings
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step step="2">
          Create an ad group
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step step="3">
          Create an ad
        </v-stepper-step>
      </v-stepper-header>
    </v-stepper>

    <v-stepper
      value="3"
      class="mt-12"
    >
      <v-stepper-header>
        <v-stepper-step
          step="1"
          complete
        >
          Select campaign settings
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step
          step="2"
          complete
        >
          Create an ad group
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step step="3">
          Create an ad
        </v-stepper-step>
      </v-stepper-header>
    </v-stepper>
  </div>
</template>


<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "HelloWorld",

  data: () => ({
    ecosystem: [
      {
        text: "vuetify-loader",
        href: "https://github.com/vuetifyjs/vuetify-loader"
      },
      {
        text: "github",
        href: "https://github.com/vuetifyjs/vuetify"
      },
      {
        text: "awesome-vuetify",
        href: "https://github.com/vuetifyjs/awesome-vuetify"
      }
    ],
    importantLinks: [
      {
        text: "Documentation",
        href: "https://vuetifyjs.com"
      },
      {
        text: "Chat",
        href: "https://community.vuetifyjs.com"
      },
      {
        text: "Made with Vuetify",
        href: "https://madewithvuejs.com/vuetify"
      },
      {
        text: "Twitter",
        href: "https://twitter.com/vuetifyjs"
      },
      {
        text: "Articles",
        href: "https://medium.com/vuetify"
      }
    ],
    whatsNext: [
      {
        text: "Explore components",
        href: "https://vuetifyjs.com/components/api-explorer"
      },
      {
        text: "Select a layout",
        href: "https://vuetifyjs.com/getting-started/pre-made-layouts"
      },
      {
        text: "Frequently Asked Questions",
        href: "https://vuetifyjs.com/getting-started/frequently-asked-questions"
      }
    ]
  })
});
</script>
