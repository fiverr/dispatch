<template>
  <v-dialog v-model="display" max-width="600px">
    <template v-slot:activator="{ on }">
      <v-badge :value="numFilters" bordered overlap color="info" :content="numFilters">
        <v-btn color="secondary" v-on="on"> Filter </v-btn>
      </v-badge>
    </template>
    <v-card>
      <v-card-title>
        <span class="headline">Column Filters</span>
      </v-card-title>
      <v-list dense>
        <v-list-item>
          <v-list-item-content>
            <incident-combobox v-model="incident" />
          </v-list-item-content>
        </v-list-item>
        <v-list-item>
          <v-list-item-content>
            <project-combobox v-model="project" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-card>
  </v-dialog>
</template>

<script>
import { sum } from "lodash"
import { mapFields } from "vuex-map-fields"
import IncidentCombobox from "@/incident/IncidentCombobox.vue"
import ProjectCombobox from "@/project/ProjectCombobox.vue"

export default {
  name: "FeedbackTableFilterDialog",

  components: {
    IncidentCombobox,
    ProjectCombobox,
  },

  data() {
    return {
      display: false,
    }
  },

  computed: {
    ...mapFields("feedback", ["table.options.filters.incident", "table.options.filters.project"]),
    numFilters: function () {
      return sum([this.incident.length, this.project.length])
    },
  },
}
</script>
