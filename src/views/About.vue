<template>
  <v-card class="mx-auto" max-width="700"  shaped elevation-13>
    <v-card-text>
      <div>{{ info.founder  }}</div>
      <p class="text-h4 text--primary">
        {{ info.name }}
      </p>
      <p>Founded: {{info.founded}}</p>
      <div class="text--primary">
        {{info.summary}}
      </div>
    </v-card-text>
    <v-card-actions>
      <v-btn text color="teal accent-4" @click="reveal = true">
        Learn More
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <v-card
        v-if="reveal"
        class="transition-fast-in-fast-out v-card--reveal"
        style="height: 100%"
      >
        <v-card-text class="pb-0">
          <p class="text-h4 text--primary">{{info.info}}</p>
          <p>
            Get the fuck out of here!
          </p>
        </v-card-text>
        <v-card-actions class="pt-0">
          <v-btn text color="teal accent-4" @click="reveal = false">
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-expand-transition>
  </v-card>
</template>
<script>
import axios from "axios";

export default {
  data: () => ({
    info: [],
    reveal: false,
  }),

  async created() {
    const { data } = await axios.get("https://api.spacexdata.com/v3/info");

    this.info = data;
    console.log(this.info);
  },
};
</script>

<style scoped>
.v-card--reveal {
  bottom: 0;
  opacity: 1 !important;
  position: absolute;
  width: 100%;
}
</style>
