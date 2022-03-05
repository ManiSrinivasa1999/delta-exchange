<template>
  <v-app>
    <!-- <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar> -->

    <v-main>
      <v-data-table
        :headers="headers"
        :items="products"
        :items-per-page="10"
        class="elevation-1"
      ></v-data-table>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  name: "App",

  components: {},

  data: () => ({
    products: [],
    headers: [
      {
        text: "Symbol",
        align: "start",
        sortable: false,
        value: "symbol",
      },
      { text: "Description", value: "description" },
      { text: "Underlying Asset", value: "underlying_asset.symbol" },
      // { text: "Market Price", value: "carbs" },
    ],
  }),
  mounted() {
    this.fetchDataFromApi();
  },
  methods: {
    async fetchDataFromApi() {
      try {
        let data = await axios.get("https://api.delta.exchange/v2/products");
        this.products = data.data["result"];
        console.log(this.products);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
