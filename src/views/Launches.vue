<template>
  <v-app>
    <v-content>
      <v-container>
        <v-timeline v-if="launches.length > 0">
          <LaunchTimelineItem
            v-for="launch in launches"
            :key="launch.flight_number"
            :launch="launch"
          />
        </v-timeline>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from "axios";
import LaunchTimelineItem from "../components/LaunchTimelineItem";
export default {
  data: () => ({
    launches: [],
  }),
  components: {
    LaunchTimelineItem,
  },
  async created() {
    const { data } = await axios.get("https://api.spacexdata.com/v3/launches");

    data.forEach((launch) => {
      this.launches.push(launch);
    });

    console.log(this.launches);
  },
};
</script>
