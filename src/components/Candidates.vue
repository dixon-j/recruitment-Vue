<template>
  <v-container class="pa-0">
     <v-text-field
      class="px-1 pt-3"
        dense
        clearable
        v-model="search"
        append-icon="mdi-magnify"
        label="Candidates"
      ></v-text-field>
      <v-tabs fixed-tabs>
        <v-tab>Outbound</v-tab>
        <v-tab>Inbound</v-tab>
        <v-tab-item>
          <v-tabs fixed-tabs>
              <v-tab>Active</v-tab>
              <v-tab>Inactive</v-tab>
              <v-tab>Complete</v-tab>
            <v-tab-item>
              <CandidatesTab :search="search" type="outbound" state="active"/>
            </v-tab-item>
            <v-tab-item>
              <CandidatesTab :search="search" type="outbound" state="inactive"/>
            </v-tab-item>
            <v-tab-item>
              <CandidatesTab :search="search" type="outbound" state="complete"/>
            </v-tab-item>
          </v-tabs>
        </v-tab-item>
        <v-tab-item>
          <v-tabs fixed-tabs>
              <v-tab>Active</v-tab>
              <v-tab>Inactive</v-tab>
              <v-tab>Complete</v-tab>
            <v-tab-item>
              <CandidatesTab :search="search" type="inbound" state="active"/>
            </v-tab-item>
            <v-tab-item>
              <CandidatesTab :search="search" type="inbound" state="inactive"/>
            </v-tab-item>
            <v-tab-item>
              <CandidatesTab :search="search" type="inbound" state="complete"/>
            </v-tab-item>
          </v-tabs>
        </v-tab-item>
      </v-tabs>
  </v-container>
</template>

<script>
import CandidatesTab from '@/components/CandidatesTab.vue'
export default {
  components: {
    CandidatesTab
  },
  data: () => ({
    search: null
  })
}
</script>
