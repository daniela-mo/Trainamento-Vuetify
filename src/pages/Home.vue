<template>
  <v-card color="#white" flat height="200px" tile>
    <v-toolbar dense>
      <v-tollbar-title>Edtech</v-tollbar-title>
    </v-toolbar>
    <v-card>
      <ListSeries />
    </v-card>
  </v-card>
</template>

<script>
import ListSeries from "@/components/ListSeries";
export default {
  components: {
    ListSeries,
  },
};
</script>
