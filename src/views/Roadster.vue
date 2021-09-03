<template>
  <v-row justify="space-around">
    <v-col cols="auto">
      <v-dialog transition="dialog-bottom-transition" max-width="600">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="primary" v-bind="attrs" v-on="on">WHO AM I?</v-btn>
        </template>
        <template v-slot:default="dialog">
          <v-card>
            <v-toolbar color="primary" dark>{{ roadster.name }}</v-toolbar>
            <v-card-text>
              <div class="text-h6 pa-6">{{ roadster.details }}</div>
            </v-card-text>
            <v-card-actions class="justify-end">
              <v-btn text @click="dialog.value = false">Close</v-btn>
            </v-card-actions>
          </v-card>
        </template>
      </v-dialog>
    </v-col>

    <v-col cols="auto">
      <v-dialog transition="dialog-top-transition" max-width="600">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="primary" v-bind="attrs" v-on="on">Distance/Speed</v-btn>
        </template>
        <template v-slot:default="dialog">
          <v-card>
            <v-toolbar color="primary" dark
              >Some shit about how far I've travelled</v-toolbar
            >
            <v-card-text>
              <div class="pa-12">
                The Actual SPEED I'm flying: {{ roadster.speed_kph }} km/h.
                <br />
                How far I flew from you guys:
                {{ roadster.earth_distance_km }} km. <br />
                Distance from THE "RED PLANET":
                {{ roadster.mars_distance_km }}km.
              </div>
            </v-card-text>

            <v-card-actions class="justify-end">
              <v-btn text @click="dialog.value = false">Close</v-btn>
            </v-card-actions>
          </v-card>
        </template>
      </v-dialog>
    </v-col>
  </v-row>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    roadster: [],
    reveal: false,
  }),

  async created() {
    const { data } = await axios.get("https://api.spacexdata.com/v3/roadster");

    this.roadster = data;
    console.log(this.roadster);
  },
};
</script>
